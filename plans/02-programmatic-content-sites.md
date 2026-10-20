# Plan 02: Programmatic Content Sites

## Summary

An agent generates and maintains a large set of long-tail reference pages in one narrow
domain, such as comparison pages, calculators, glossary entries, or how-to guides. The
site earns from display ads and affiliate links. Once the site has search traffic the
ongoing work is quarterly refreshes and reviewing a sample of pages for quality.

## Why it is close to passive

- Traffic from search compounds over months without further effort per page.
- Ads and affiliate programs pay without any customer support.
- The agent handles research, drafting, internal linking, and refreshes.

## Why it is the riskiest of the four

- Search engines actively demote thin or unhelpful AI-generated content. The site must be
  genuinely useful or it will earn nothing.
- Payback is slow. Expect six to twelve months before meaningful traffic.
- Ad and affiliate rates fluctuate and are outside your control.

Treat this as a long-term asset, not a quick win.

## Candidate site types

| Type | Example | Monetisation | Quality bar |
|------|---------|--------------|-------------|
| Comparison pages | "Tool A vs Tool B" for one software category | Affiliate | High, needs real differences |
| Calculators and converters | Niche unit, tax, or dosage calculators | Ads | Medium, correctness is everything |
| Glossary and reference | Terms in one technical field | Ads | Medium, cite sources |
| Data-backed pages | One page per city, product, or entity, fed by a dataset | Ads, affiliate | High, needs unique data |
| How-to guides | Step-by-step for one tool or hobby | Affiliate, ads | High, must be tested |

The strongest option is **data-backed pages fed by a dataset you already collect**. This
makes plan 01 and plan 02 the same pipeline with two outputs, and gives pages a reason to
exist that a competitor cannot copy by prompting a model.

## Agent architecture

```
 keyword and topic agent ----> page backlog (topics, intent, priority)
 (search data, competitor
  gaps, dataset coverage)
        |
        v
 research agent ----> source notes per page (with citations)
        |
        v
 drafting agent ----> page draft (template + structured sections)
        |
        v
 fact-check agent ----> pass / revise / reject
 (independent pass,
  checks claims against
  sources and dataset)
        |
        v
 publisher ----> static site (Astro, Hugo, Next) ----> CDN
        |
        v
 refresh agent (quarterly) ----> stale page queue
```

Design notes:

- **Templates, not free prose.** Every page type has a fixed structure. The agent fills
  sections. This keeps quality consistent and makes pages easy to refresh.
- **Fact-check agent runs with a different prompt and no access to the draft's reasoning.**
  It sees the claims and the sources only. Reject rate is a quality signal.
- **Unique value per page.** Every page should include at least one thing a model cannot
  produce from memory: a dataset value, a calculator result, a tested procedure, or a
  comparison table built from real specs.
- **Static site.** No server to maintain. Deploy to a CDN with free hosting.

## Revenue model

- Display ads once traffic qualifies for a premium network.
- Affiliate links where the page intent is commercial.
- Later: a paid tool or dataset download that the free pages funnel to.

## Cost model

- Generation: one-off LLM spend per page. Budget per page and do not exceed it.
- Hosting: near zero on a static CDN.
- Domain and ad network fees: small.
- The real cost is time to payback.

## Minimum viable version

1. Pick a domain where you can judge quality yourself.
2. Choose one page type. Write the template and one hand-crafted gold example.
3. Build the backlog agent and generate fifty topics. Prune by hand.
4. Generate twenty pages through the full pipeline. Read every one.
5. Publish, submit a sitemap, and wait eight weeks.
6. Expand only if pages are indexed and some rank. Otherwise fix the template first.

## Risks

- **Search engine policy changes.** Diversify traffic with an email list or a tool people
  bookmark.
- **Hallucinated facts.** Mitigated by the fact-check agent and by citing sources on page.
- **Affiliate program termination.** Do not depend on one program.
- **Legal.** Avoid medical, legal, and financial advice niches unless you can meet the
  expertise bar.

## Open questions to expand

- Which domain, and can it share a dataset with plan 01?
- Which page type first?
- Who reviews a sample of pages each month, and how large a sample?
- Ad network or affiliate first?
