# Plan 01: Niche Data Products

## Summary

An agent collects, cleans, and normalises data from public sources on a schedule, and the
resulting dataset is sold as a subscription. Customers pay for not having to do the
collection themselves. Once the pipeline is stable, the ongoing work is fixing scrapers
when a source changes and answering the occasional support email.

This version of the plan is researched as of 2026-10-20. Prices and limits below are
quoted from vendor pages or secondary sources listed under Sources. Anything marked
"estimate" is an assumption, not a quote.

The short version: start from government and public-record sources (lowest legal
exposure, free APIs); demand is proven in every niche below by incumbents charging $50 to
$2,000 a month and by pay-per-result scrapers on Apify selling the same records; the LLM
bill for nightly extraction on Claude Haiku 5.5 is single-digit dollars a month and
infrastructure is $5 to $40; the hard parts are choosing a niche the owner can sell into
and keeping fetchers alive, and the agent solves neither.

## Why it is close to passive

- Collection runs unattended on a cron schedule.
- Revenue is recurring and does not scale with your time.
- The agent handles the messy part: sources with inconsistent formats, free-text fields,
  and layout changes that break traditional scrapers.
- Customers rarely churn if the data saves them hours each week.
- Most candidate sources are official APIs or open-data portals. API-backed sources break
  far less often than scraped HTML, which is what keeps maintenance low.

Not passive, budget two to four hours a week once live: a few fetchers a month need
attention even with API sources, customers ask for fields you do not have, and the first
ten customers come from manual outreach rather than the landing page.

## Candidate niches

Choose one. Good niches have a clear buyer with budget, data that is public but scattered,
and a reason to want it fresh. The five below were checked for three things: paid
competitors (proof of demand), where buyers gather, and whether the sources are official
APIs or open data with permissive terms.

| Niche | Buyer | Freshness | Proof of demand | Source terms | Risk |
|-------|-------|-----------|-----------------|--------------|------|
| 1. Building permits, one metro or trade | Contractors, suppliers, solar and HVAC installers | Daily | ConstructConnect from $129/mo per market and seat; permit lead resellers at $50 to $300/mo (vendor claim) | US city open-data portals (Socrata SODA API); UK PlanIt aggregator | Low in US, medium in UK (Ordnance Survey derived fields) |
| 2. Tenders and RFPs, one sector | Small vendors, consultants | Daily | BidNet Direct $599 to $1,999/yr; GovTribe and BidPrime around $99 to $299/mo; SamSearch $49 to $299/mo | SAM.gov API (free key), TED API v3 (free), state and local portals (mixed) | Low |
| 3. Grants, one vertical or state | Nonprofits, grant writers, researchers | Weekly | Instrumentl $179 to $299/mo; Candid FDO $1,599 to $2,199/yr; GrantWatch $199/yr | grants.gov search2 API (free, no auth); state and foundation sites (mixed) | Low |
| 4. FDA enforcement: warning letters, recalls, 483s | QA and regulatory staff at device, pharma, food SMEs; consultants | Daily | Apify monitors at $79/mo plus per alert; enterprise regulatory intel is quote-only | openFDA API (free key, 120,000 req/day); FDA warning letter XML dataset | Low |
| 5. New business filings, one state | Insurance agents, payroll, merchant services, local B2B sellers | Daily | States sell the raw feed ($40/type/mo in ND; $35 to $9,500 in IN); resellers at $50 to $200/mo (vendor claim) | State Secretary of State bulk data; some free portals | Medium to high: records name individuals, data broker laws apply |

Notes per niche:

1. **Building permits.** Hundreds of US cities publish permits on Socrata portals with a
   free JSON API (Chicago dataset `ydr8-5enu`, San Francisco `i98e-djp9` updated nightly).
   Shovels sells a national permit API with 185M+ records and claims $250K MRR per a
   third-party profile, so the national play is taken. Go narrower: one metro, one trade
   (for example roofing permits in one county, with contractor names where the city
   publishes them). In the UK, PlanIt aggregates 424 of 425 planning authorities with a
   public JSON endpoint, but council data under OGL v3 often carries Ordnance Survey
   restrictions on coordinates and third-party copyright on documents.
2. **Tenders.** SAM.gov covers federal only and already has a crowded aggregator market.
   The gap is state, county, school district, and utility portals, which are fragmented
   and searchable only by hand. A sector-specific feed (for example "water and wastewater
   RFPs across six states") is defensible. SAM.gov's public API allows 10 requests per day
   for a non-federal user without a role and 1,000 per day with a role, so plan for a role
   on your entity before launch. TED's v3 API is free and documented.
3. **Grants.** grants.gov's search2 and fetchOpportunity endpoints need no authentication.
   The incumbents are expensive because they also cover foundations, which have no central
   source. A cheap feed for one vertical (for example arts and culture grants in one state,
   including state agency and community foundation deadlines) undercuts Instrumentl for
   buyers who only need that slice.
4. **FDA enforcement.** openFDA gives 240 requests per minute and 120,000 per day with a
   free key. Warning letters have a weekly XML index on data.gov plus an FDA datatables
   export. The product is the summary and the alert, not the raw letter: "which device
   makers got a 483 for design controls this week". Buyers are easy to find because they
   are listed on the letters.
5. **New business filings.** Demand is strong (states themselves sell the feed) but
   records contain owner names and addresses. In California, Texas, Oregon, and Vermont a
   business that sells personal data about people it has no relationship with may need to
   register as a data broker (fees reported at $6,600 in CA, $300 in TX, $600 in OR, $100
   in VT). Only pick this if you strip individual names or accept the registration cost.

## Product shapes

Pick one to launch, add others later.

1. **Weekly or daily email digest.** Cheapest to build. Good for low-volume niches.
   Grants and FDA enforcement fit this shape.
2. **CSV or spreadsheet download.** Behind a login, refreshed on schedule. Permits and
   filings fit this shape because buyers load them into a CRM or dialer.
3. **REST API.** For technical buyers. Highest price, most support burden. Only build it
   when a customer asks and will pay for it.
4. **Hosted searchable table.** A simple web UI over the dataset with filters and export.
   Datasette on a VPS gives this for free over SQLite.
5. **Alerts.** Customer defines filters, gets notified on new matches. Pairs well with 1.
   This is the shape incumbents charge the most for relative to effort.

Recommended launch shape for all five niches: email digest plus a CSV link, delivered
through a Stripe Payment Link. Add the API only when a customer asks for it.

## Agent architecture

```
 scheduler (systemd timer on VPS, or GitHub Actions cron as fallback)
     |
     v
 source registry ----> fetcher ----------> raw store (object storage or local disk)
 (list of sources,     (plain HTTP for APIs and open data,
  cadence, last run,    Playwright only where flagged,
  terms checked,        ETag / hash change detection,
  robots.txt status)    per-source rate limit)
                                |
                                v  (only new or changed raw records)
                         extraction agent ----> normalised store (SQLite/Postgres)
                         (Claude Haiku 5.5 structured output via Batch API,
                          fixed JSON schema per niche,
                          dedup by stable key, entity matching)
                                |
                                v
                         quality agent ----> review queue (only on anomaly)
                         (row counts, nulls,            |
                          drift vs. 7-day baseline,     v
                          new enum values)         fetcher repair agent
                                |                  (Claude Sonnet 5.5 with browser
                                v                   tools, proposes a selector or
                         publisher                  parser patch, never auto-merges)
                         (email / CSV / API / UI,
                          Stripe customer list as the ACL)
                                |
                                v
                         daily health email to owner + spend counter
```

Design notes:

- **Fetcher.** Plain HTTP and parsing where the source is stable. Fall back to an agent
  with browser tooling only for sources that need it. Store the raw payload with its
  content hash; the extraction step only runs on records whose hash changed. Send a
  descriptive User-Agent with a contact address and keep request rates low.
- **Extraction agent.** One structured-output call per raw record with a fixed JSON
  schema. Use the Batch API for the nightly run because latency does not matter and it
  halves the token price. Cache the system prompt and schema with prompt caching.
- **Quality agent.** Compares today's run against a rolling baseline. Flags large drops in
  row count, spikes in nulls, or new values in enum fields. Only anomalies reach you.
- **Fetcher repair agent.** When a source returns zero rows or the quality agent flags
  it, a Sonnet-class agent with a browser tool inspects the page, proposes a patch, and
  opens a pull request. The owner merges. This is the one place a capable model earns
  its cost.
- **Publisher.** Boring code. No agent needed.
- **Spend cap.** A hard token budget per run and per day, enforced in code before the
  API call. A runaway loop should cost less than one subscription.

### Scheduling options

| Option | Cost | Limits worth knowing | Fit |
|--------|------|----------------------|-----|
| GitHub Actions cron | Free in public repos; 2,000 min/mo free for private repos on GitHub Free | Minimum interval 5 minutes; runs can be delayed at busy times; in public repos the schedule is auto-disabled after 60 days without repository activity, with no notification | Fine for a daily job in a private repo. Keep the repo private (customer data) and the job under 60 minutes |
| Hetzner cloud VPS (CX23, 2 vCPU, 4 GB) | About EUR 3.99/mo plus EUR 0.50/mo for IPv4 after the April 2026 price rise (third-party reports); cost-optimised plans have had availability gaps | None that matter at this scale | Best default. systemd timers, SQLite, Playwright, and Datasette all on one box |
| Cloudflare Workers cron triggers | Free plan | 5 cron triggers per account on Free; 15 minute limit per cron run; 10 ms CPU per request on Free | Good for lightweight API polling and the health ping, not for extraction |

### Browser automation, only where required

| Option | Cost | Notes |
|--------|------|-------|
| Playwright on your VPS | $0 beyond the VPS | Default. Headless Chromium in Docker. Fine for a handful of JavaScript-heavy sources |
| Cloudflare Browser Rendering | Free: 10 min/day, 3 concurrent; Paid ($5/mo Workers plan): 10 hours/mo, overage $0.09/browser hour | Cheapest hosted option for a few minutes a day |
| Browserbase | Free: 1 browser hour; Developer $20/mo for 100 hours; proxy bandwidth billed separately (reported around $12/GB) | Only if you need stealth or residential proxies, which you should not for public-record sources |
| Apify | Free plan with $5/mo platform credit; Starter reported at $19 to $49/mo (sources conflict) | Also a sales channel: many competitors are Apify actors priced per 1,000 results |

Rule: if a public-record source needs CAPTCHA solving or proxy rotation, do not add it.
Find the underlying open-data endpoint or bulk export instead.

### Extraction with Claude

Prices from the Claude pricing page as of October 2026, per million tokens:

| Model | Input | Output | Cache read | Batch input | Batch output | Use |
|-------|-------|--------|------------|-------------|--------------|-----|
| Claude Haiku 5.5 (prompts up to 100K tokens) | $0.10 | $0.50 | $0.01 | $0.05 | $0.25 | Bulk extraction of every record |
| Claude Sonnet 5.5 | $2.00 | $10.00 | $0.10 | $1.00 | $5.00 | Fetcher repair, hard free-text sources, weekly summaries |

- Use structured outputs (`output_config.format` with a JSON schema, or the SDK's
  `messages.parse()` helper) so every record validates against the niche schema. Put the
  schema and instructions in a cached system prompt.
- Submit the nightly set as one Message Batch. Results arrive within hours, which is fine
  for a daily digest, and the discount is 50 percent on input and output.
- Keep the per-record prompt small: the raw record, not the whole page. A permit or
  tender record is usually under 1,500 tokens.
- Haiku's price doubles for prompts over 100,000 tokens. Never send a whole page listing.

### Change detection

- For APIs: store the last-modified or updated field per record and query by it.
- For HTML and PDFs: send `If-None-Match` and `If-Modified-Since`; hash the normalised
  text of each record; only changed hashes reach the extraction step.
- changedetection.io is free to self-host and can watch a few hundred index pages for
  "something changed" signals, with a hosted plan at $8.99/mo for 5,000 URLs. Visualping
  starts at $14/mo for 10 pages, which does not scale to this use.
- The quality agent's row-count baseline is the real change detector for breakage.

### Data hosting and delivery

| Layer | Default | Alternative |
|-------|---------|-------------|
| Database | SQLite on the VPS, nightly backup to object storage | Supabase Free (500 MB, 5 GB egress, pauses after 7 days idle) or Pro at $25/mo; Cloudflare D1 Free (5M rows read/day, 5 GB) or $5/mo Workers Paid |
| Searchable UI | Datasette over the SQLite file | Supabase auto-generated REST plus a small front end |
| API | A small FastAPI or Hono app with API keys stored next to the Stripe customer id | Zuplo as a gateway (free tier reported at 100K to 1M requests/mo, sources conflict; Builder $25/mo) |

### Payments

- Stripe standard pricing is 2.9% + 30 cents per successful domestic card charge, plus
  0.7% of billing volume for Stripe Billing on the pay-as-you-go tier. A $49 subscription
  nets about $47.
- Payment Links, the hosted pricing table, and the customer portal need no code. A
  webhook on `customer.subscription.created` and `.deleted` is the only integration:
  it adds or removes the email from the digest list and issues or revokes the API key.
- Annual plans with a discount reduce churn and give cash up front, but offer refunds
  for the unused months to keep disputes down.

## Revenue model

- Subscription tiers by freshness and volume. Example: weekly digest at a low tier,
  daily plus CSV at a middle tier, API plus custom filters at the top.
- Annual plans with a discount to reduce churn and smooth cash flow.
- Later: sell historical archives and trend reports as one-off purchases.

Price anchors from incumbents, per month unless noted:

| Niche | Low end | High end | Suggested launch price |
|-------|---------|----------|------------------------|
| Permits | Apify actors at $3 to $30 per 1,000 records; lead resellers $50 to $300 (vendor claim) | ConstructConnect $129 to $199 per market and seat; Dodge $6,000 to $12,000/yr | $49 digest, $149 CSV plus alerts |
| Tenders | SamSearch $49; BidNet free tier | BidNet $1,999/yr; GovTribe $299 | $39 digest, $99 daily plus CSV |
| Grants | GrantWatch $199/yr | Instrumentl $299 to $999; Candid FDO $2,199/yr | $29 digest, $79 with state and foundation sources |
| FDA enforcement | Apify monitor $79 plus per alert | Enterprise regulatory intel, quote only | $59 digest, $199 for API and multi-seat |
| New business filings | States sell raw feeds from $35 to $40 | Resellers $50 to $200 (vendor claim) | $49 digest, $129 CSV with enrichment |

Price below the incumbent but above the Apify actor. The Apify actor is a per-record
commodity; the subscription sells normalisation, dedup, summaries, and alerts.

### Go-to-market

1. **Landing page with a real sample.** Publish last week's digest in full, free, on the
   page. The current week is paid. Buyers can judge quality before paying.
2. **Free sample tier.** A monthly or delayed version at $0 builds a list to upsell. For
   alerts, free means "weekly batch", paid means "same day".
3. **Communities where buyers already are.** r/GovernmentContracting had roughly 44,000
   members in a 2025 snapshot. Grant writers gather around the Grant Professionals
   Association. Contractors are reachable through trade associations and supplier
   newsletters. Post the free sample, not the pitch.
4. **Cold outreach to proven buyers.** Incumbents' testimonial pages, Apify actor
   reviews, and FDA warning letter recipients are lists of people who already pay for or
   need this data. Twenty personal emails a week with the sample attached is the plan
   for the first fifty customers.
5. **The Steerwell public repo (plan 03).** Decided 2026-10-20. The open-source skills
   repo links to this product from its README and, where natural, from skill output.
   Shared tooling that is safe to publish lives there; this pipeline's sources, parsers,
   and schemas do not.
6. **Directories.** Datarade lists providers on a commission-only tier (a competitor
   report cites 30 percent; unverified on Datarade's site) and deals close off-platform.
   The Apify Store is a second channel: publish a cut-down actor that sells per-record
   and upsells to the subscription. Product Hunt and Hacker News work once, for the
   launch, and only if the sample is interesting on its own.

## Cost model

- Compute: a small VPS or free-tier cron runner.
- LLM spend: dominated by extraction. Cache by content hash so unchanged records cost
  nothing. Budget a hard daily cap.
- Storage: negligible at niche scale.
- Payments: Stripe fees.

Target: infrastructure and LLM spend under a single customer's monthly subscription.

### Worked example

Assumptions, all estimates unless marked:

- Niche: tenders in one sector across 25 state and local portals plus SAM.gov.
- Volume: 2,000 new or changed records per day on average, 30 days a month.
- Extraction prompt: 1,500 input tokens per record (record text plus cached schema),
  300 output tokens. Run on Claude Haiku 5.5 through the Batch API.
- Repairs: 5 source breakages a month, each a Sonnet 5.5 agent session of about
  150,000 input and 10,000 output tokens.
- Summaries: one Sonnet 5.5 call a day of 20,000 input and 2,000 output tokens.
- Infrastructure: Hetzner CX23 with IPv4, Supabase Free, transactional email.
- Stripe fees: 2.9% + $0.30 per charge plus 0.7% Billing (quoted).

| Line | Calculation | Monthly |
|------|-------------|---------|
| Haiku extraction, batch | 60,000 records x 1,500 in x $0.05/M + 60,000 x 300 out x $0.25/M | $4.50 + $4.50 = $9.00 |
| Same on Sonnet 5.5 batch, for comparison | 90M in x $1/M + 18M out x $5/M | $90 + $90 = $180 |
| Repair agent, Sonnet | 5 x (150K x $2/M + 10K x $10/M) | $2.00 |
| Daily summary, Sonnet | 30 x (20K x $2/M + 2K x $10/M) | $1.80 |
| VPS | EUR 4.49, about $4.90 | $5 |
| Database, email, domain | Supabase Free, email estimate, domain at about $1/mo | $15 |
| **Total cost** | | **about $33** |

Revenue scenarios at the suggested tender prices ($39 digest, $99 daily plus CSV):

| Scenario | Subscribers | Gross | Stripe fees (3.6% + $0.30 each) | Net after costs |
|----------|-------------|-------|---------------------------------|-----------------|
| First month after launch | 5 at $39 | $195 | $8.52 | $153 |
| Month 6 | 20 at $39, 5 at $99 | $1,275 | $53.40 | $1,189 |
| Month 12 | 40 at $39, 15 at $99 | $3,045 | $126.12 | $2,886 |

Cost barely moves with subscribers; the only variable is extraction volume, and even at
ten times the records Haiku extraction stays under $100 a month. Moving extraction to
Sonnet is the one decision that changes the economics, so test Haiku's accuracy on a
200-record sample first. Subscriber counts are targets, not forecasts; no independent
conversion data for indie data products was found.

## Minimum viable version

1. **Week 1: pick the niche, list sources.** Ten to twenty sources. For each, record
   the access method (API, bulk file, HTML), the terms-of-use URL, the robots.txt
   status, update cadence, and whether any field is personal data. Drop any source that
   fails the legal checklist below.
2. **Week 1: write the normalised schema.** Under fifteen fields. Include a stable
   external id, a source URL, first-seen and last-changed timestamps, and a confidence
   field from the extractor.
3. **Week 2: build the fetcher for the three easiest sources.** Hand-code them against
   the official API or bulk export. No agent yet. Store raw payloads with hashes.
4. **Week 2: build the extraction step.** One Haiku 5.5 structured-output call per
   record, submitted as a batch. Measure accuracy on 200 hand-checked records. Add
   Sonnet only for the sources Haiku gets wrong.
5. **Weeks 3 and 4: publish a weekly email to yourself.** Fix what breaks. Add the
   quality agent and the daily health email in this window.
6. **Week 5: landing page, Stripe Payment Link, free sample.** Put last week's full
   digest on the page. Set up the Stripe webhook that manages the subscriber list.
7. **Week 5 onwards: charge from the first customer.** Send twenty outreach emails a
   week with the sample. Add sources and fields only when a paying customer asks.

Expect roughly 60 to 80 hours of build before the first paid customer (estimate).

## Risks

- **Source terms of service.** Some sites prohibit scraping. Prefer government and public
  record sources, and check robots.txt and terms before adding a source.
- **Layout churn.** Mitigated by the quality agent and by keeping the source count small
  until revenue justifies more.
- **Competition from free aggregators.** Go narrower, add normalisation and alerts the
  aggregator lacks.
- **Personal data.** Avoid niches where records contain personal information unless you
  have a clear lawful basis.
- **API quota changes.** SAM.gov's tiered daily limits and openFDA's per-key limits can
  change. Keep a bulk-download fallback for every API source.

### Legal landscape, practical version

**United States.**

- The Computer Fraud and Abuse Act is a weak tool against scraping public pages. The
  Supreme Court in Van Buren (2021) read "exceeds authorized access" narrowly, and the
  Ninth Circuit on remand in hiQ v. LinkedIn (2022) held that scraping publicly
  accessible data likely does not violate the CFAA.
- Contract claims survive. The hiQ district court held in November 2022 that LinkedIn's
  anti-scraping terms were enforceable, and the case ended with a $500,000 judgment and an
  injunction against hiQ. The lesson is to never log in or accept terms on a source you
  scrape.
- Scraping without logging in is where defendants have won. In Meta v. Bright Data
  (January 2024) the court held Meta's terms did not cover logged-off scraping of public
  data, and Meta dropped the case. In X Corp. v. Bright Data (May 2024) the court
  dismissed X's claims and warned against "information monopolies" over public data,
  though X was later allowed to replead on server-strain grounds.
- The new front is DMCA section 1201. Google sued SerpApi in December 2025 claiming its
  bot-detection system is an access control and that evading it is circumvention, with
  statutory damages of $200 to $2,500 per violation. Reddit sued Perplexity and SerpApi
  on a similar theory in October 2025. Neither is decided. The practical rule is to never
  bypass a CAPTCHA, bot block, or rate limiter.
- Cloudflare has blocked known AI crawlers by default for new domains since July 2025.
  A fetcher that identifies itself honestly and hits a block should stop, not evade.
- robots.txt (RFC 9309) is advisory and is not a form of access authorisation in law,
  but courts and the EU regulators treat it as evidence of what the site owner expects.
  Follow it.
- US federal government works are public domain under 17 U.S.C. 105. This does not cover
  state and local governments, contractor-produced content, or third-party material
  embedded in a government document. Check each portal's terms; most open-data portals
  use permissive licences.
- Personal data: the CCPA's public-records exemption was widened in 2019, but a 2026
  analysis notes the exemption can be lost when records are aggregated or enhanced. Four
  states require data broker registration for businesses that sell personal data about
  people they have no relationship with (fees reported at CA $6,600, TX $300, OR $600,
  VT $100). Selling business-entity data without individual names avoids this.

**European Union and United Kingdom.**

- GDPR applies whenever records identify a person, public or not. The EDPB's draft
  Guidelines 03/2026 on web scraping (July 2026, consultation open until 30 October 2026)
  say public availability is not consent; the workable basis is legitimate interest,
  strengthened by excluding sensitive categories, collecting only freely accessible data,
  pseudonymising early, and respecting robots.txt, ai.txt, CAPTCHAs, and login walls as
  signals of reasonable expectations. A public privacy notice is still required.
- The Database Directive's sui generis right protects substantial investment in a
  database. The Open Data Directive says public bodies should not use that right to block
  reuse, so government portals are safe. Private aggregators are not: do not extract a
  substantial part of a private database.
- Text and data mining opt-outs under the DSM Directive must be machine-readable; the
  Hamburg appeals court (Kneschke v. LAION, December 2025) held natural-language terms
  are insufficient. The EU AI Act and the GPAI Code of Practice require robots.txt
  compliance from model providers. This targets training, but a scraper that reads
  robots.txt and TDMRep signals is on the right side either way.
- UK council data under the Open Government Licence v3 permits commercial reuse, but
  individual councils add restrictions, Ordnance Survey derived coordinates are
  excluded from commercial reuse, and planning documents often carry third-party
  copyright. Use PlanIt's aggregated fields and link to documents rather than copying them.

**Per-source checklist, applied before a source enters the registry.**

1. Is there an official API or bulk export? Use it, even if the HTML is easier.
2. Does reading the data require a login, accepting terms, or passing a bot check? If
   yes, skip the source.
3. Does robots.txt disallow the paths you need? If yes, skip or ask for permission.
4. Does the licence permit commercial reuse? Record the URL.
5. Does any field identify a natural person? Drop it, or document the lawful basis and
   registration obligations.
6. Rate limit at or below one request per second; send a User-Agent with contact address.

## Decisions still open

These need the owner's input. Everything else in this plan has a default.

1. **Which niche.** The five candidates differ mainly in who the owner can sell to. The
   plan recommends tenders or FDA enforcement for the lowest legal risk and the clearest
   buyer, but the owner's own network decides. Who are the first three people you would
   email the sample to?
2. **Geography.** US federal plus one or two states, or UK and EU sources? This fixes the
   legal checklist and the currency of the Stripe account.
3. **Haiku-only or mixed extraction.** The worked example assumes Haiku 5.5 for all
   records. If the 200-record accuracy test fails for some sources, the monthly LLM cost
   rises toward the Sonnet line. Decide the accuracy bar before the test.
4. **Monthly spend cap.** The plan proposes $50 for LLM and $40 for infrastructure until
   the fifth paying customer. Confirm or change.
5. **Public repo or private.** Decided private for the pipeline. Credibility comes from
   the public plan 03 repo instead, so this repo keeps its source list and parsers out of
   view. Still open: whether to run on a VPS or private GitHub Actions (free minutes, but
   cron auto-disables after 60 idle days).
6. **Whether to publish an Apify actor as a lead channel.** It generates sales but also
   signals the sources to competitors.

## Sources

Niche demand and pricing:

- ConstructConnect pricing guide (October 2026): https://constructionbids.ai/blog/constructconnect-pricing-guide-2026
- Dodge and construction lead pricing: https://pipelineon.com/blog/construction-leads-2026/
- Permit lead resale claims and per-record pricing on Apify: https://apify.com/lowlanddata/building-permit-monitor and https://apify.com/4l3c/building-permits-scraper
- Shovels permit API scale and MRR estimate: https://sacra.com/c/shovels/ and https://thegtmdirectory.com/tools/shovels
- Chicago and San Francisco permit dataset ids on Socrata: https://apify.com/moving_beacon-owner1/socrata-chicago-building-permits/api
- PlanIt coverage of UK planning authorities: https://directory.civictech.guide/listing/planit
- BidNet Direct supplier pricing: https://civiciq.com/blog/civic-iq-bidnet-direct-pricing and https://us.fitgap.com/products/bidnet
- GovTribe, BidPrime, DemandStar pricing: https://govcontractfinder.com/tools/government-contracting-software-pricing-guide and https://providers.apievangelist.com/providers/demandstar/
- SamSearch pricing: https://govcontractfinder.com/tools/government-contracting-software-pricing-guide and https://samsearch.co/blog/top-10-govwin-alternatives-complete-2025-guide
- Instrumentl, Candid FDO, GrantWatch pricing: https://www.grantwatch.com/grant-database-comparison.php , https://fundingforgood.org/comparing-grant-research-databases/ , https://onlinedegrees.sandiego.edu/nonprofit-grant-databases/
- FDA monitoring tools on Apify: https://apify.com/azureblue/fda-drug-approval-watch and https://apify.com/tagadanar/fda-warning-letters
- North Dakota new business records subscription: https://www.sos.nd.gov/node/3982
- Indiana bulk business entity data fees: https://www.in.gov/sos/business/files/Regulatory-Analysis-Business-Entity-Bulk-Data-Fees-LSA-25-155-OMB-2025-01R.pdf
- New business filing resellers on Apify: https://apify.com/scrapemint/new-business-registration-leads
- r/GovernmentContracting size (2025 snapshot): https://gummysearch.com/r/GovernmentContracting

Data sources and APIs:

- SAM.gov Get Opportunities public API: https://open.gsa.gov/api/get-opportunities-public-api/
- SAM.gov rate limit tiers (10/day without role, 1,000/day with role): https://open.gsa.gov/api/fh-public-api/ and https://open.gsa.gov/api/assistance-listings-api/
- TED API v3 developer docs: https://docs.ted.europa.eu/ and https://data.ted.europa.eu/
- grants.gov search2 and fetchOpportunity: https://grants.gov/api/common/search2 , https://www.grants.gov/api/common/fetchopportunity , https://grants.gov/api/api-guide
- openFDA rate limits and keys: https://open.fda.gov/apis/authentication
- FDA warning letters XML dataset on data.gov: https://catalog-beta.data.gov/dataset/warning-letters-79b61

Legal:

- hiQ v. LinkedIn history and settlement: https://www.polsinelli.com/publications/data-scraping-update-linkedin-v-hiq-answers-some-questions-but-leaves-many-more-open and https://www.natlawreview.com/article/linkedin-s-data-scraping-battle-hiq-labs-ends-proposed-judgment
- X Corp. v. Bright Data dismissal and revival, with Meta v. Bright Data outcome: https://www.cnbc.com/2024/05/10/elon-musks-x-loses-lawsuit-against-bright-data-over-data-scraping.html and https://www.mediapost.com/publications/article/401510/x-corp-can-revive-scraping-battle-with-bright-dat.html
- Google v. SerpApi (DMCA 1201): https://ipwatchdog.com/2025/12/26/google-sues-serpapi-parasitic-scraping-circumvention-protection-measures/ and https://www.searchenginejournal.com/google-files-dmca-suit-targeting-serpapis-serp-scraping/563847/
- Reddit v. Perplexity and SerpApi: https://techdirt.com/2025/12/24/google-built-its-empire-scraping-the-web-now-its-suing-to-stop-others-from-scraping-google
- Cloudflare default AI crawler blocking: https://engadget.com/ai/cloudflare-experiment-will-block-ai-bot-scrapers-unless-they-pay-a-fee-121523327.html
- RFC 9309 status and crawl-delay: https://www.searchengineworld.com/rfc9309-robots-txt-quietly-became-an-official-internet-standard and https://www.zyte.com/blog/robots-txt-overview/
- 17 U.S.C. 105 and its limits: https://law.counselstack.com/usc/17/105 and https://libanswers.snhu.edu/faq/363183
- CCPA public records exemption and 2026 analysis: https://www.mto.com/Templates/media/files/PDF/Munger-Tolles-DJ-Consumer-Privacy-Law-Amendments-9-19.pdf and https://www.jdsupra.com/legalnews/navigating-california-s-data-broker-1926867/
- State data broker registration fees: https://captaincompliance.com/education/state-data-broker-laws-compared-ct-ca-tx-vt-mt/ and https://www.monda.ai/blog/data-broker-registries-in-the-us
- EDPB draft Guidelines 03/2026 on web scraping: https://www.edpb.europa.eu/system/files/2026-07/edpb_guidelines_2020603_webscraping_v1_en_0.pdf and https://www.alstonprivacy.com/eu-regulators-outline-gdpr-requirements-for-ai-web-scraping/
- Database Directive and Open Data Directive interaction: https://www.ivir.nl/publicaties/download/IIC_2021.pdf and https://communia-association.org/2018/05/10/database-directive-study-options-neutralising-sui-generis-right/
- TDM opt-out, Kneschke v. LAION, AI Act Article 53: https://ipregistry.co/blog/eu-ai-act-crawler-enforcement and https://www.scrapingbee.com/blog/tdmrep-ai-txt-scraping-controls/
- UK OGL v3 in council practice and Ordnance Survey limits: https://www.thurrock.gov.uk/sites/default/files/assets/documents/policy-reuse-of-information-v05.pdf , https://www.bury.gov.uk/copyright/copyright-and-re-use-of-materials , https://ukauthority.com/articles/surrey-sets-up-open-planning-data-survey , https://opendata.camden.gov.uk/Environment/Gospel/m5tn-ufud

Tooling and infrastructure:

- GitHub Actions schedule event limits: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows
- GitHub Actions included minutes: https://docs.github.com/en/billing/reference/product-usage-included and https://docs.github.com/en/billing/concepts/product-billing/github-actions
- Hetzner 2026 price rise and CX23 pricing (third-party): https://findstack.com/resources/hetzner-price-increase-2026 and https://www.bitdoze.com/md/hetzner-cloud-cost-optimized-plans.md
- Cloudflare Workers limits (cron triggers, CPU): https://developers.cloudflare.com/workers/platform/limits
- Cloudflare Browser Rendering pricing: https://developers.cloudflare.com/changelog/post/2025-07-28-br-pricing/
- Cloudflare D1 pricing: https://developers.cloudflare.com/d1/platform/pricing/
- Browserbase pricing (third-party trackers): https://usagepricing.com/blueprint/browserbase and https://apicostcalc.com/browserbase.html
- Apify pricing (third-party, conflicting): https://automationatlas.io/answers/apify-pricing-explained-2026/ and https://www.capterra.com/p/150854/Apify/pricing/
- changedetection.io and Visualping pricing: https://visualping.io/changedetection-alternative and https://www.guideflow.com/blog/website-change-monitoring-software
- Supabase pricing: https://supabase.com/pricing.md
- Zuplo pricing: https://zuplo.com/pricing
- Claude model pricing, caching, and Batch API discount: https://platform.claude.com/docs/en/about-claude/pricing
- Claude structured outputs and batch processing docs: https://platform.claude.com/docs/en/build-with-claude/batch-processing
- Stripe card and Billing fees: https://stripe.com/pricing and https://stripe.com/billing/pricing
- Stripe no-code subscriptions (Payment Links, pricing table, customer portal): https://docs.stripe.com/no-code/get-started

Go-to-market:

- Datarade provider terms (commission reported by a competitor): https://providers.datarade.ai/apply and https://pipeline.zoominfo.com/sales/datarade-pricing
