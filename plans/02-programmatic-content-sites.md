# Plan 02: Programmatic Content Sites

Researched 2026-10-20. Figures marked "estimate" are the author's assumptions, not
sourced data. Everything else is cited in the Sources section.

## Summary

An agent generates and maintains a large set of long-tail reference pages in one narrow
domain, such as comparison pages, calculators, glossary entries, or how-to guides. The
site earns from display ads and affiliate links. Once the site has search traffic the
ongoing work is quarterly refreshes and reviewing a sample of pages for quality.

The 2026 version of this plan is narrower than the 2023 version. Pure informational pages
lose most of their clicks to AI Overviews, and Google now runs three named spam updates a
year with a policy written specifically for "scaled content abuse". What survives is a
site where each page carries something a model cannot produce from memory: a dataset
value, a working calculator, a tested procedure, or a live comparison table. The plan
below is built around that constraint.

## Why it is close to passive

- Traffic from search compounds over months without further effort per page.
- Ads and affiliate programs pay without any customer support.
- The agent handles research, drafting, internal linking, and refreshes.
- Static hosting has no server to patch. Cloudflare Pages does not meter bandwidth on its
  free tier, so a traffic spike costs nothing [1].

## Why it is the riskiest of the four

### Search policy in 2026

- Google's spam policies name **scaled content abuse**: "many pages" generated "primarily
  to manipulate search rankings and not help users", and the policy applies "no matter
  whether content is produced through automation, human efforts, or some combination" [2].
  Google's generative AI guidance adds that "using generative AI tools or other similar
  tools to generate many pages without adding value for users may violate" that policy [3].
- Google's position since February 2023 is that it rewards "quality content, however it is
  produced", and that automation has long produced useful pages (sports scores, weather,
  transcripts). Using automation "primarily to manipulate ranking" is spam [4].
- Google ran spam updates in March, June and August 2026, each rolled out globally in two
  days or less, and did not name a target for any of them [5] [6]. Core updates ran in
  March (27 March to 8 April) and May 2026. Vendor trackers reported that template-driven
  location pages, coupon sites and category listings dropped 28 to 35 percent in March,
  and that "AI content farms" lost around 75 percent of visibility. Those are vendor
  estimates, not Google data [7] [8].
- **Site reputation abuse** (third-party content on an established domain) is enforced by
  manual action outside the EEA. From 30 August 2026 manual actions do not apply to users
  inside the EEA after a European Commission mandate [9]. This matters only if you plan to
  host your pages on someone else's domain. Do not.

### AI Overviews and the click shortfall

- Ahrefs re-ran its 300,000 keyword study on December 2025 data. Position one CTR on
  informational keywords with an AI Overview fell from 7.3 percent in December 2023 to
  1.6 percent, a 58 percent drop. Position 10 fell 19 percent [10].
- Seer Interactive's Search Console study found organic CTR on informational queries with
  an AI Overview fell from 1.76 percent to 0.61 percent between June 2024 and September
  2025, and that the decline slowed in its 2026 update [11] [12].
- SparkToro's analysis of Similarweb's US panel for January to April 2026 found 68 percent
  of Google searches ended without a click, up from 60 percent in 2024. Roughly 276 clicks
  reach the open web per 1,000 searches [13].
- Chartbeat data reported by Reuters Institute showed Google search referrals to 2,500
  publishers down about a third in the year to November 2025. A March 2026 Chartbeat
  breakdown found small publishers down 60 percent, medium down 47 percent, large down 22
  percent [14] [15]. Small sites are hit hardest. That is us.
- AI chatbot referrals are growing but still under 1 percent of publisher page view
  referrals [14]. ChatGPT referral share went mostly to homepages after a May 2026 link
  format change [16]. Do not plan around LLM referral traffic as a revenue source.

### What this means for viability

The honest read: a site that answers questions in prose will not pay. Google itself
absorbs the answer. A site that gives the visitor something to **do** (run a calculation,
filter a dataset, compare live numbers) still gets the click, because the AI Overview
cannot execute it. Omni Calculator reports around 8 million monthly unique users and
Semrush estimates about half its traffic is Google organic and a third is direct, which
is the pattern to copy: tools people come back to [17] [18].

Payback is slow. Expect six to twelve months before meaningful traffic, longer on a new
domain. Ad and affiliate rates fluctuate and are outside your control. Treat this as a
long-term asset, not a quick win. The README's suggestion to do this plan last or
alongside plan 01 stands.

## Candidate site types

| Type | Example | Monetisation | Quality bar | 2026 outlook |
|------|---------|--------------|-------------|--------------|
| Comparison pages | "Tool A vs Tool B" for one software category | Affiliate | High, needs real differences | Viable if the table is built from live specs and pricing, not prose. Thin affiliate pages lost around half their visibility in March 2026 [8] |
| Calculators and converters | Niche unit, tax, or dosage calculators | Ads | Medium, correctness is everything | Strongest. Agency playbooks agree these work when demand exists and each variant differs meaningfully. Near-duplicate calculators with swapped numbers fail [19] |
| Glossary and reference | Terms in one technical field | Ads | Medium, cite sources | Weakest. This is exactly what an AI Overview answers inline |
| Data-backed pages | One page per city, product, or entity, fed by a dataset | Ads, affiliate | High, needs unique data | Viable if the dataset is yours. Template location pages built on public data dropped 28 to 35 percent in March 2026 [7] |
| How-to guides | Step-by-step for one tool or hobby | Affiliate, ads | High, must be tested | Marginal. HowTo rich results are gone and the steps get summarised in the Overview [20] |

The strongest option is **data-backed pages fed by a dataset you already collect**, with
a **calculator or filter on the page**. This makes plan 01 and plan 02 the same pipeline
with two outputs, and gives pages a reason to exist that a competitor cannot copy by
prompting a model.

### Patterns that still work

- **Dataset entity pages with a tool.** Wise's currency converter pages and Zapier's
  integration pages are the usual examples of template pages that survived, because the
  number or the integration is real and changes [21]. Scale is not the problem. Empty
  templates are.
- **Calculators with a reason to click.** The visitor needs to enter their own numbers.
  The Overview can state the formula but not run it for them.
- **Tools people bookmark.** Direct traffic is the hedge against every Google update.

### Patterns that got wiped out

- Location-swapped service pages ("best X in [city]") built on scraped or public data.
- Coupon and deal aggregators built programmatically [8].
- Prose glossaries and "what is X" pages. Answered inline.
- AI-written listicles with no first-hand testing. Google's quality rater guidance asks
  "who, how and why", and vendor post-mortems tie March 2026 losses to pages without
  authorship, first-hand experience or transparent sourcing [4] [8].

## Agent architecture

```
 keyword and topic agent ----> page backlog (topics, intent, priority, dataset coverage)
 (Search Console, Bing
  Webmaster keyword tool,
  competitor gaps)
        |
        v
 research agent ----> source notes per page (with URLs and dataset row IDs)
        |
        v
 drafting agent ----> page draft (template + structured sections + calculator config)
        |
        v
 fact-check agent ----> pass / revise / reject   (reject rate logged as a quality metric)
 (independent pass,
  sees claims and
  sources only)
        |
        v
 human sample review (10 percent of new pages, 100 percent of the first 50)
        |
        v
 publisher ----> static site (Hugo or Astro) ----> Cloudflare Pages
        |              |
        |              +----> sitemap to Google Search Console
        |              +----> IndexNow ping to Bing and others
        v
 monitor agent (weekly) ----> Search Console API: indexed count, clicks, pages
        |                      "Discovered, not indexed"; alert on drops over 30 percent
        v
 refresh agent (quarterly) ----> stale page queue (dataset changed, source changed,
                                 zero impressions in 90 days -> prune candidate)
```

Design notes:

- **Templates, not free prose.** Every page type has a fixed structure. The agent fills
  sections. This keeps quality consistent and makes pages easy to refresh.
- **Fact-check agent runs with a different prompt and no access to the draft's reasoning.**
  It sees the claims and the sources only. Reject rate is a quality signal. If the reject
  rate drops to zero, the checker is broken, not the drafter.
- **Unique value per page.** Every page should include at least one thing a model cannot
  produce from memory: a dataset value, a calculator result, a tested procedure, or a
  comparison table built from real specs.
- **Static site.** No server to maintain. Deploy to a CDN with free hosting.
- **Publish gradually.** One job-board post-mortem describes a new domain that was
  indexed and then almost entirely dropped after making thousands of pages indexable at
  once [22]. That is one anecdote, but Google's own crawl guidance says every site starts
  with a conservative crawl capacity that is raised only as demand appears [23]. Release
  in batches of 20 to 50 pages per week and watch the Page Indexing report.
- **Prune.** A page with zero impressions after 90 days is a liability under the scaled
  content policy. Noindex it or fold it into a parent page.
- **Kill switch.** The monitor agent must be able to halt publishing. It never
  auto-publishes after an alert.

### Making pages citable by AI search

- Google says no special file or markup is needed for AI Overviews or AI Mode. A page
  must be indexed and eligible for a snippet, and structured data should match the
  visible text [24] [25]. Search Console now has a Generative AI performance report [26].
- Google does not read `llms.txt`. John Mueller called it "purely speculative" and
  compared it to the keywords meta tag; Gary Illyes said Google has no plans to support
  it [27] [28]. Skip it unless an engine you care about documents support.
- ChatGPT uses Bing's index when it searches, so register in Bing Webmaster Tools and
  push URLs via IndexNow [29] [30].
- Write answer-first paragraphs with a sourced number in the first sentence. Vendor
  studies of LLM citations agree on this pattern even where their numbers disagree [29].
- Name an author, date the page, and show the data source. Google's gen-AI guidance says
  the review obligation extends to titles, descriptions, structured data and alt text,
  so the fact-check pass must cover metadata too [3].

## Revenue model

### Display ads

| Network | Entry bar (October 2026) | Revenue share | Notes |
|---------|--------------------------|---------------|-------|
| Google AdSense | Content that meets policy, owner 18+. No stated traffic minimum [31] | Not listed | Common rejection reason is "low value content". Vendor benchmarks put AdSense RPM around $2 to $6 [32]. Fine as a placeholder, not as a plan |
| Journey by Mediavine | 1,000 sessions in 30 days from premium markets (US, UK, CA, AU). Original content. Evaluated via Google Analytics [33] [34] | 70 percent per third-party reports, unverified | Moves to full Mediavine at $5,000 annual ad revenue [33] |
| Raptive | 25,000 pageviews in 30 days. 50 percent of traffic from US, UK, CA, NZ, AU under 100k pageviews, 40 percent above. Domain at least six months old. "Original, human-led content" [35] [36] | Not listed | Dropped from 100,000 in October 2025 |
| Ezoic | 250,000 monthly users for new publishers since 19 February 2026. Smaller sites go to the Incubator programme [37] [38] | Not listed | Out of reach for a new site |

RPM by niche is not published by any network. Third-party tables conflict with each
other. The ranges that recur are finance $20 to $45, food $8 to $28, travel $6 to $24
on Mediavine-class networks, with one publisher reporting a $14.50 median across a
sample of 200 blogs [39] [40]. Treat these as order-of-magnitude only. Two things are
consistent across every source: traffic geography and niche matter more than the
network, and Q4 pays more than Q1.

Raptive's "original, human-led content" requirement is a policy risk for this plan.
A reviewer who sees obviously templated pages may reject the site. The human sample
review and named authorship are there to clear this bar, not just Google's.

### Affiliate

| Programme type | Typical terms | Fit |
|----------------|---------------|-----|
| Amazon Associates | Most categories 1 to 4.5 percent, 24-hour cookie, three sales in 180 days to keep the account. Third-party reports of unannounced mid-2026 cuts; the official schedule could not be fetched [41] [42] | Only for physical-product comparison pages. Low margin |
| SaaS recurring | 20 to 30 percent recurring is the common band, often lifetime; some programmes cap at 12 to 24 months. One-time bounties $50 to $500 for cheaper products [43] | Best fit for software comparison pages |
| Networks (Impact, ShareASale, PartnerStack, CJ) | Free for publishers. Each merchant sets its own rate | Apply once traffic exists; approvals are per merchant |

Disclosure: the FTC Endorsement Guides require a clear affiliate disclosure near the
link. Compliance blogs also describe a 2026 expectation to disclose AI involvement in
endorsement content. That second point could not be verified against ftc.gov, so treat
it as likely and cheap to comply with: put a one-line "how this page was made" note on
every page [44].

### Alternative traffic (the hedge)

- **Email.** A weekly "what changed in the dataset" digest. Low volume, but owned.
  Needs traffic to build, so it does not replace search [45].
- **Pinterest.** Only for visual niches (food, home, craft). Vendor claims of 10k to
  200k monthly visits within a year are unaudited [46]. Not relevant for a calculator site.
- **Communities.** Reddit and niche forums are the top cited sources across LLM answer
  engines in one 10,000 citation sample [29]. Answering questions there with a link to
  the tool is the slow, honest route.
- **Direct and bookmark.** The real goal. Omni Calculator's roughly one third direct
  traffic is the target shape [18].
- **LLM citations.** Nice to have. Measure them in the Search Console gen-AI report and
  server logs, but do not model revenue from them.

### Later

A paid tool or dataset download that the free pages funnel to. This is where plan 01's
subscription product plugs in.

## Cost model

### Tooling

| Item | Choice | Cost | Why |
|------|--------|------|-----|
| Static site generator | Hugo (default) or Astro | Free | Hugo builds 10,000 pages in seconds as a single Go binary. Astro is slower at that scale (one unverified test: 31 seconds vs 0.4) but has a better component model if the calculators are JS-heavy [47] [48] |
| Hosting | Cloudflare Pages | Free | Unmetered bandwidth on the free tier, 500 builds a month. Vercel Hobby forbids commercial use and Netlify's free credits pause the site when exhausted [1] |
| Domain | .com via Cloudflare Registrar or Porkbun | About $10.50 to $11 per year, renewal the same. Verisign plans 7 percent annual wholesale rises from 2026 [49] | Do not use an expired domain with history. Expired domain abuse is a named spam policy [2] |
| Keyword data | Google Search Console API and Bing Webmaster Tools keyword tool | Free. Search Console API limited to 50k rows per day per property [50] [51] | Enough for a solo operator. Add Keywords Everywhere ($84 per year for 100k credits) if you need volume estimates [52]. Ahrefs Lite at $129 a month is not justified before revenue |
| Indexing | Sitemap in Search Console, IndexNow for Bing, Yandex, Naver, Seznam | Free. Cloudflare Crawler Hints can send IndexNow pings automatically [30] | Google's Indexing API is limited to JobPosting and BroadcastEvent pages, default quota 200 URLs. Using it for other content violates the terms [53] [54] |
| Structured data | JSON-LD per template: WebApplication or SoftwareApplication for calculators, Dataset for data pages, BreadcrumbList, Organization with a named author | Free | FAQ rich results stopped showing on 7 May 2026 and HowTo in 2023. Markup still helps Google understand the page but do not expect a visual result [20] [55] |
| Analytics | GA4 (required by Mediavine and Raptive for applications) [34] [36] | Free | Add a cookie banner if you have EU traffic |

### Generation cost per page

Model prices, Anthropic first-party API, October 2026 [56]:

| Model | Input $/M tokens | Output $/M tokens | Batch API (50 percent off) |
|-------|------------------|-------------------|----------------------------|
| Claude Haiku 5.5 | 0.10 | 0.50 | 0.05 / 0.25 |
| Claude Sonnet 5.5 | 2.00 | 10.00 | 1.00 / 5.00 |
| Claude Opus 5.5 | 4.00 | 20.00 | 2.00 / 10.00 |

Estimate for one templated page with an independent fact-check pass. Assumptions:
research step reads about 20k tokens of fetched sources, the draft prompt carries the
template, a gold example and the source notes (about 8k tokens), the fact-check prompt
carries claims plus sources (about 10k tokens), and the metadata step is trivial.

| Step | Model | Input tokens | Output tokens | Cost (sync) |
|------|-------|--------------|---------------|-------------|
| Research and source notes | Sonnet 5.5 | 20,000 | 3,000 | $0.07 |
| Draft | Sonnet 5.5 | 8,000 | 2,500 | $0.04 |
| Fact-check | Opus 5.5 | 10,000 | 2,000 | $0.08 |
| Metadata, schema, alt text | Haiku 5.5 | 4,000 | 800 | under $0.01 |
| **Total per accepted page** | | | | **about $0.20** |

Add 30 percent for revise loops and rejected drafts: **about $0.25 per page synchronous,
about $0.13 through the Batch API** (estimate). All-Opus is about $0.30 synchronous.
Prompt caching on the template and gold example cuts the draft step further; the cached
part is a fixed prefix so cache it and keep per-page content after the breakpoint.
Server-side web search and web fetch are billed separately per use; check the pricing
page before enabling them in the research step [56].

At 1,000 pages that is $130 to $300 in generation spend. Quarterly refresh of a third of
the site at the same unit cost is about $40 to $100 per quarter. Generation is not the
cost. Time to payback is.

### Running cost (estimate)

| Item | Monthly |
|------|---------|
| Hosting, DNS | $0 |
| Domain (amortised) | about $1 |
| LLM: 50 new pages plus refresh and monitor runs | $15 to $30 |
| Keyword tool (optional) | $7 |
| **Total** | **about $25 to $40** |

Set a hard monthly token cap in the pipeline at twice this figure.

## Unit economics and timeline

### Assumptions (all estimates, change them in the spreadsheet before trusting the result)

- 500 published pages by month 9, 1,000 by month 15.
- Average 40 pageviews per page per month at month 12 for a tool-backed page. This is
  the author's guess. The Ahrefs figure that only 1.74 percent of new pages reach the top
  10 within a year [57] means most pages will earn near zero and a few will carry the site.
- 60 percent of traffic from premium ad markets (needed for Journey and Raptive).
- 1.3 pageviews per session.
- RPM $8 on Journey, $15 on Raptive-class, blended across the year.
- Affiliate: 0.5 percent of sessions click an affiliate link, 3 percent of those convert,
  $40 average commission. Only on the 20 percent of pages with commercial intent.

### Three scenarios at month 12

| Scenario | Pages | Pageviews per month | Ad RPM | Ad revenue | Affiliate | Total per month |
|----------|-------|---------------------|--------|------------|-----------|-----------------|
| Weak | 500 | 5,000 | $5 (AdSense) | $25 | $10 | about $35 |
| Base | 700 | 28,000 | $8 (Journey) | $225 | $100 | about $325 |
| Strong | 1,000 | 90,000 | $15 (Raptive) | $1,350 | $400 | about $1,750 |

Cumulative spend to month 12 is roughly $600 to $900 (generation, domain, optional
tools). The base case pays that back around month 15 to 18. The weak case never does,
which is why the MVP has a stop condition.

### Timeline

| Month | Milestone | Gate to continue |
|-------|-----------|------------------|
| 0 to 1 | Domain, Hugo template, one gold page, calculator component, backlog of 50 topics | You can judge a page as right or wrong yourself |
| 1 to 2 | 20 pages through the full pipeline, every one read by you. Submit sitemap, register Bing, enable IndexNow | Fact-check reject rate between 5 and 25 percent |
| 2 to 4 | Wait. Watch Page Indexing report. Fix the template, not the volume | At least 15 of 20 pages indexed, some impressions |
| 4 to 7 | Release 30 to 50 pages a week. Add email capture. Apply to AdSense as a placeholder | Impressions growing week over week |
| 7 to 9 | Apply to Journey at 1,000 premium sessions | Accepted, RPM visible |
| 9 to 15 | Grow to 1,000 pages. Prune zero-impression pages. Domain passes six months for Raptive | 25,000 pageviews and 50 percent premium traffic |
| 15 onward | Raptive or full Mediavine. Quarterly refresh only. Launch the paid dataset from plan 01 | Monthly revenue covers monthly cost by 3x |

Stop condition: if fewer than half the first 50 pages are indexed by month 4, or
impressions are flat for eight weeks after that, do not add pages. Either the template is
wrong or the niche is already answered inline by AI Overviews. Try the other before
spending more.

## Minimum viable version

1. Pick a domain where you can judge quality yourself and where the page needs a number
   the visitor supplies or a dataset you own.
2. Choose one page type. Write the Hugo template and one hand-crafted gold example with
   a working calculator or data table.
3. Build the backlog agent from Search Console and Bing keyword data. Generate fifty
   topics. Prune by hand.
4. Generate twenty pages through the full pipeline, including the fact-check pass. Read
   every one. Log the reject rate.
5. Publish, submit a sitemap, register in Bing Webmaster Tools, and wait eight weeks.
6. Expand only if pages are indexed and some rank. Otherwise fix the template first.

## Risks

- **Search engine policy changes.** Three spam updates and two core updates in the
  first eight months of 2026 [5] [6] [7]. Mitigation: tools people bookmark, an email
  list, Bing and IndexNow, and a page count that stays below what you can sample-review.
- **AI Overviews absorb the niche.** Check before building: search ten target queries.
  If every one shows an Overview that fully answers it, pick a niche where the visitor
  must act on their own numbers.
- **Ad network rejection for templated content.** Raptive asks for "human-led" content
  [35]. Mitigation: named author, visible methodology, human sample review, and no
  page that exists only to rank.
- **Hallucinated facts.** Mitigated by the fact-check agent, by citing sources on page,
  and by extending the check to metadata as Google's guidance requires [3].
- **Affiliate program termination or rate cuts.** Amazon cut rates without announcement
  in 2026 per third-party reports [42]. Do not depend on one program.
- **Legal.** Avoid medical, legal, and financial advice niches unless you can meet the
  expertise bar. A dosage calculator is a medical device question in some jurisdictions.
- **Dataset licence.** If plan 01's data is scraped, confirm you may republish derived
  pages. The spam policies also name scraping as a scaled content pattern [2].
- **Disclosure.** Affiliate links and AI involvement both need a visible disclosure [44].

## Decisions still open

These need the owner's input. Everything else in this file has a default.

1. **Which niche.** It must satisfy three tests: you can judge a page's correctness
   yourself, the visitor has to supply their own inputs or use your dataset, and a sample
   of ten target queries is not fully answered by an AI Overview today. If plan 01 has a
   dataset, that decides it.
2. **Calculator-first or dataset-first.** Calculator pages need a front-end component and
   a test suite per formula. Dataset pages need plan 01's collector to be running first.
   Pick the one whose prerequisite you already have.
3. **Author identity.** Pages need a named author with a bio for ad network review and
   for Google's "who" question. Your real name, or a pen name with a real photo and
   verifiable background. Not a fabricated persona.
4. **Review budget.** How many pages per month will you personally read? That number caps
   the publishing rate. The plan assumes 100 percent of the first 50 and 10 percent after.
5. **Geography of the audience.** Journey and Raptive count only premium-market sessions.
   If the natural audience for the niche is outside the US, UK, Canada and Australia, the
   ad path changes to AdSense and affiliate only, and the revenue scenarios roughly halve.
6. **Stop loss.** Agree the month-4 and month-9 gates above before starting, so the
   decision to stop is mechanical.

## Sources

Policy and search landscape

1. Hosting free tiers compared, September 2026: https://flaviocopes.com/hosting-free-tiers/
2. Google spam policies (scaled content abuse, expired domain abuse, site reputation abuse): https://developers.google.com/search/docs/essentials/spam-policies
3. Google guidance on generative AI content: https://developers.google.com/search/docs/fundamentals/using-gen-ai-content
4. Google Search's guidance about AI-generated content (February 2023): https://developers.google.com/search/blog/2023/02/google-search-and-ai-content
5. Google Search Status Dashboard, March 2026 spam update: https://status.search.google.com/incidents/LEubPCm2octf2uMqCFKE
6. Search Engine Journal on the June 2026 spam update: https://www.searchenginejournal.com/google-spam-update-june-24-2026/580424/ and August 2026: https://www.techwyse.com/?p=77933
7. March 2026 core update vendor analysis (Loganix): https://loganix.com/?p=36438 and SE Ranking data via Truelogic: https://www.truelogic.com.ph/?p=91359
8. March 2026 core update winners and losers (on-page.ai): https://blog.on-page.ai/googles-march-2026-core-update-winners-losers-and-what-changed
9. Google, update to the site reputation policy (August 2026, EEA): https://developers.google.com/search/blog/2026/08/update-site-reputation-policy
10. Ahrefs, AI Overviews reduce clicks by 58 percent (February 2026): https://ahrefs.com/blog/ai-overviews-reduce-clicks-update/
11. Seer Interactive, AIO impact on CTR: https://seerinteractive.com/insights/ctr-aio
12. Seer Interactive, 2026 update: https://www.seerinteractive.com/blog/aio-impact-on-google-ctr-2026-update
13. SparkToro zero-click 2026 as reported: https://www.pravinkumar.co/blog/sparktoro-2026-zero-click-search-68-percent-2026
14. Press Gazette on Reuters Institute and Chartbeat data: https://pressgazette.co.uk/media-audience-and-business-data/google-traffic-down-2025-trends-report-2026/
15. Axios, small publishers hit hardest (March 2026): https://www.axios.com/2026/03/17/chartbeat-search-traffic-ai-chatbots
16. Similarweb AI search stats and ChatGPT referral change: https://aisearch.similarweb.com/blog/gen-ai-stats/ and https://searchenginejournal.com/ai-search-isnt-replacing-google-its-layering-on-top-similarweb-data/583378/

What still works

17. Omni Calculator, by the numbers: https://www.omnicalculator.com/omni-by-the-numbers
18. Semrush traffic estimate for omnicalculator.com: https://www.semrush.com/website/omnicalculator.com/overview/
19. Programmatic calculator pages playbook: https://seo.irpr.agency/programmatic-seo/calculator-pages/
20. FAQ rich results retired May 2026: https://www.techwyse.com/news/ai-search/google-faq-rich-results-deprecated-2026
21. Programmatic SEO in 2026, what survived: https://alexcloudstar.com/blog/programmatic-seo-2026-indie-hackers/
22. Job board indexed then dropped (anecdote): https://hackernoon.com/i-launched-two-similar-job-boards-google-indexed-one-and-rejected-the-other
23. Google crawl budget guide: https://developers.google.com/crawling/docs/crawl-budget and reported July 2026 change: https://www.pinmeto.com/news/google-crawl-budget-conservative-default-2026/

AI search citability

24. Google, AI features and your website: https://developers.google.com/search/docs/appearance/ai-features
25. Google, optimising for generative AI features: https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
26. Search Console generative AI performance reports: https://developers.google.com/search/blog/2026/06/gen-ai-performance-reports
27. Search Engine Journal, Google says llms.txt is speculative: https://www.searchenginejournal.com/google-says-llms-txt-is-purely-speculative-for-now/577576/
28. Search Engine Journal, llms.txt guidance depends on which product: https://www.searchenginejournal.com/googles-llms-txt-guidance-depends-on-which-product-you-ask/517651/
29. LLM citation sources (vendor): https://quickseo.ai/blog/llm-citation-sources-how-ai-chatbots-choose-what-to-cite-and-how-to-get-included and https://surferseo.com/blog/llm-citations
30. IndexNow via Cloudflare Crawler Hints: https://www.webnots.com/how-to-submit-pages-to-indexnow-with-cloudflare/ and overview: https://www.searchbloom.com/ai-seo/inclusion/indexnow/

Monetisation

31. AdSense eligibility as quoted: https://theguidex.com/google-adsense-approval/
32. AdSense RPM benchmark (vendor): https://newormedia.com/blog/best-adsense-alternatives/
33. Mediavine requirements: https://www.mediavine.com/mediavine-requirements/
34. Mediavine application process and GA4: https://www.mediavine.com/blog/mediavine-application-process-ga4/
35. Raptive eligibility: https://help.raptive.com/hc/en-us/articles/360032840891-Who-is-eligible-for-Raptive
36. Raptive, applying with Google Analytics: https://help.raptive.com/hc/en-us/articles/6681661647515-Applying-to-Raptive-with-Google-Analytics and the 25k change: https://raptive.com/blog/opening-the-door-to-more-creators-who-meet-raptive-quality-standards/
37. Ezoic 250k announcement (press release): https://aijourn.com/ezoic-raises-bar-to-250k-js-integration-for-full-revenue-platform-surges-in-popularity-with-web-builders/
38. Ezoic Incubator: https://www.ezoic.com/incubator
39. RPM by niche (vendor, conflicting): https://www.earnifyhub.com/blog/blogging/blog-display-ad-rpm-by-niche-2026
40. Mediavine vs Raptive vs Ezoic RPM (vendor sample): https://earnifyhub.com/blog/blogging/mediavine-vs-raptive-vs-ezoic-rpm
41. Amazon Associates rates 2026 (third party): https://getlasso.co/amazon-affiliate-commission-rate/
42. Reported Amazon commission cuts, May 2026: https://www.shopifreaks.com/amazon-quietly-slashed-associates-affiliate-commission-rates-by-up-to-50-across-publisher-ecosystem-and-gutted-reporting-tools/
43. SaaS affiliate commission benchmarks: https://www.track360.io/blog/saas-affiliate-commission-rates-benchmark-2026
44. Affiliate and AI disclosure (compliance blogs, unverified against ftc.gov): https://www.mattmcwilliams.com/affiliate-disclosure/ and https://track360.io/blog/ai-generated-affiliate-content-compliance-operator-guide-2026
45. Publishers and owned audiences: https://neilpatel.com/blog/referral-traffic-decline-publishers/ and https://digiday.com/media/media-briefing-publishers-turn-to-other-platforms-to-offset-losses-from-google-search/
46. Pinterest for bloggers (vendor): https://www.unilink.us/blog/pinterest-for-bloggers-2026

Tooling and costs

47. Astro vs Hugo, 2026: https://gautamkhorana.com/static-site-generators/compare/astro-vs-hugo/
48. 10,000 page build test (unverified method): https://markaicode.com/alternatives/astro-alternatives/
49. Domain costs: https://porkbun.com/about/domain-cost-calculator and https://instantdomainsearch.com/learn/guides/best-domain-registrars-2026
50. Search Console API pricing (free): https://developers.google.com/webmaster-tools/pricing
51. Search Console data limits: https://support.google.com/webmasters/answer/12919192
52. Keywords Everywhere pricing: https://www.capterra.com/p/10033977/Keywords-Everywhere/
53. Google Indexing API quota clarification: https://seroundtable.com/google-updates-indexing-api-quota-information-42316.html
54. Indexing API scope: https://ppc.land/google-clarifies-indexing-api-quota-and-usage-in-recent-documentation-update/
55. Structured data types retired 2025: https://www.relevantaudience.com/seo/google-removes-structured-data-2025-guide-for-websites/
56. Claude API pricing and batch processing: https://platform.claude.com/docs/en/about-claude/pricing and https://platform.claude.com/docs/en/build-with-claude/batch-processing
57. Ahrefs new page ranking study as cited: https://kolonell.com/en/blog/google-ranking-time-how-long-2026

Not verified directly: Mediavine Journey revenue share (70 percent is third party),
Amazon's official fee schedule, FTC AI-disclosure wording, the Astro build benchmark, and
all RPM ranges. Direct fetches of these pages were blocked in the research environment.
