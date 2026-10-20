# Plan 01: Niche Data Products

## Summary

An agent collects, cleans, and normalises data from public sources on a schedule, and the
resulting dataset is sold as a subscription. Customers pay for not having to do the
collection themselves. Once the pipeline is stable, the ongoing work is fixing scrapers
when a source changes and answering the occasional support email.

## Why it is close to passive

- Collection runs unattended on a cron schedule.
- Revenue is recurring and does not scale with your time.
- The agent handles the messy part: sources with inconsistent formats, free-text fields,
  and layout changes that break traditional scrapers.
- Customers rarely churn if the data saves them hours each week.

## Candidate niches

Choose one. Good niches have a clear buyer with budget, data that is public but scattered,
and a reason to want it fresh.

| Niche | Buyer | Freshness need | Notes |
|-------|-------|----------------|-------|
| Local building permits and planning applications | Contractors, suppliers, realtors | Daily | Hundreds of council sites, all different |
| Government tenders and RFPs in one sector | Small vendors, consultants | Daily | Portals are fragmented and searchable only by hand |
| Grant and funding deadlines | Nonprofits, researchers, startups | Weekly | Low volume, high value per lead |
| Used industrial equipment listings | Buyers, brokers | Daily | Price trends are a second product |
| Regulatory changes in one industry | Compliance teams | Daily | Summaries matter more than raw text |
| Job postings matching a narrow profile | Recruiters, job seekers | Daily | Crowded, differentiate by niche |
| Event and conference listings in one field | Marketers, speakers | Weekly | Easy to start, modest pricing |
| Franchise and business-for-sale listings | Buyers, brokers | Daily | Aggregators exist, go narrower |

## Product shapes

Pick one to launch, add others later.

1. **Weekly or daily email digest.** Cheapest to build. Good for low-volume niches.
2. **CSV or spreadsheet download.** Behind a login, refreshed on schedule.
3. **REST API.** For technical buyers. Highest price, most support burden.
4. **Hosted searchable table.** A simple web UI over the dataset with filters and export.
5. **Alerts.** Customer defines filters, gets notified on new matches. Pairs well with 1.

## Agent architecture

```
 scheduler (cron)
     |
     v
 source registry ----> fetcher agent ----> raw store (object storage)
 (list of sources,       (per source,
  cadence, last run)     handles pagination,
                         detects layout changes)
                                |
                                v
                         extraction agent ----> normalised store (SQLite/Postgres)
                         (structured output,
                          schema per niche,
                          dedup, entity matching)
                                |
                                v
                         quality agent ----> review queue (only on anomaly)
                         (row counts, nulls,
                          drift vs. yesterday)
                                |
                                v
                         publisher ----> email / CSV / API / UI
```

Design notes:

- **Fetcher agent.** Use plain HTTP and parsing where the source is stable. Fall back to an
  agent with browser tooling only for sources that need it. The agent's job is to notice
  when a page layout changed and either adapt or flag it, not to do every fetch.
- **Extraction agent.** One structured-output call per raw record with a fixed JSON schema.
  Cache aggressively. Most records do not change day to day.
- **Quality agent.** Compares today's run against a rolling baseline. Flags large drops in
  row count, spikes in nulls, or new values in enum fields. Only anomalies reach you.
- **Publisher.** Boring code. No agent needed.

## Revenue model

- Subscription tiers by freshness and volume. Example: weekly digest at a low tier,
  daily plus API at a higher tier, custom filters at the top.
- Annual plans with a discount to reduce churn and smooth cash flow.
- Later: sell historical archives and trend reports as one-off purchases.

## Cost model

- Compute: a small VPS or free-tier cron runner.
- LLM spend: dominated by extraction. Cache by content hash so unchanged records cost
  nothing. Budget a hard daily cap.
- Storage: negligible at niche scale.
- Payments: Stripe fees.

Target: infrastructure and LLM spend under a single customer's monthly subscription.

## Minimum viable version

1. Pick a niche and list ten to twenty sources.
2. Write the normalised schema. Keep it under fifteen fields.
3. Build the fetcher for the three easiest sources. Hand-code them, no agent yet.
4. Build the extraction step with structured output.
5. Publish a weekly email to yourself for two weeks. Fix what breaks.
6. Put up a landing page with a Stripe checkout and the sample email as proof.
7. Charge from the first customer. Add sources as paying customers ask.

## Risks

- **Source terms of service.** Some sites prohibit scraping. Prefer government and public
  record sources, and check robots.txt and terms before adding a source.
- **Layout churn.** Mitigated by the quality agent and by keeping the source count small
  until revenue justifies more.
- **Competition from free aggregators.** Go narrower, add normalisation and alerts the
  aggregator lacks.
- **Personal data.** Avoid niches where records contain personal information unless you
  have a clear lawful basis.

## Open questions to expand

- Which niche, and who are the first three people you would email about it?
- Which product shape launches first?
- Monthly LLM spend cap?
- Will you need browser automation for any launch sources, or can all be fetched plainly?
