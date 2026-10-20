# Plan 04: Agent-Generated Digital Products

Last researched: 2026-10-20. Policies and fees below change often. Every number
is cited in the Sources section; estimates are labelled as such.

## Summary

An agent pipeline produces finished digital goods, such as workbooks, study guides,
question banks, lesson plans, spreadsheet models, checklists, and planners. They are sold
on marketplaces like Gumroad, Etsy, Amazon KDP, Payhip, or Lemon Squeezy. After the
pipeline is built, the work is choosing what to make next and reviewing output before
listing.

Two things changed the shape of this plan in 2025 and 2026. Teachers Pay Teachers
announced in October 2026 that it will ban AI-generated text and images and told sellers
to replace AI content in existing products, so TPT is no longer a target. Every other
major marketplace either requires disclosure (Etsy, Amazon KDP, Creative Market) or has
no AI-specific rule but an "own work, you are responsible" standard (Gumroad, Payhip,
Lemon Squeezy). So: disclose everywhere, build for Etsy plus one direct store, treat KDP
paperbacks as a secondary channel, and leave TPT alone.

## Why it is close to passive

- Each product sells indefinitely with no per-sale effort. Marketplaces deliver the file.
- Marketplaces handle payment, tax collection in most cases, and most discovery. Gumroad
  became merchant of record on 1 January 2025 and handles sales tax and VAT; Lemon
  Squeezy and Payhip also handle tax as merchant of record or via built-in tools.
- The agent does drafting, formatting, variant generation, and listing copy.
- Running cost is the LLM spend to generate a product, which is low (see Cost model),
  plus listing fees that are cents per item.

Not passive: the first ten products, human review before each publish, and quarterly
policy checks.

## The quality constraint

Marketplaces are flooded with low-effort AI products and buyers have learned to spot them.
Chalkbeat's August 2026 investigation of TPT found AI worksheets with an alphabet missing
the letter F, a Black inventors poster with the wrong image, and a presidents poster
illustrated with an asteroid. Those products sold for $1.50 to $1.99 and triggered the
ban two months later. That is the failure mode to design against.

Products that sell have a clear audience, a specific problem, a professional layout, and
content that is correct. The agent produces the draft. You own the standard.

Quality bar for every product: every claim, formula, answer key entry, and date is
checked by a second agent pass and spot-checked by you; no filler pages; layout is a
designed template; the listing states audience, contents, page count, format, and the
AI disclosure where the marketplace asks for it.

## Marketplace policies and fees (as of 2026-10-20)

This is the section to re-check every quarter. Where I could not reach the official page
directly, the row says so.

### AI content policy by marketplace

| Marketplace | AI-generated content allowed? | Disclosure | Enforcement | Notes |
|---|---|---|---|---|
| Etsy | Yes, under Creativity Standards as "Designed by a seller" when generated from the seller's own prompts | Must be stated in the listing description; seller is listed as the designer | Automated flagging plus member reports; listings removed, repeat shops suspended; sellers report limited appeals | Selling AI prompt bundles on their own is prohibited |
| Amazon KDP | Yes | Required for "AI-generated" (text, images, translations created by an AI tool, even if heavily edited). Not required for "AI-assisted" (you wrote it, AI edited or brainstormed) | Private declaration on the Content page at publish; no public badge; non-disclosure can lead to removal | Daily cap of three new titles per account since 2023 |
| Teachers Pay Teachers | No. Ban announced 8 October 2026 at a seller town hall, reported 15 October | Not applicable | New reporting tools, monitoring, sellers told to replace AI content in existing listings, no deadline given | Line between "generated" and "assisted" not yet defined by TPT |
| Creative Market | Yes | Yes/no "AI label" question at upload when the product or a key feature was primarily made with generative AI | Buyers can report "Missing AI Label"; outcomes range from listing edits to removal | Buyer-facing filters planned once catalog is classified |
| Gumroad | No AI-specific rule found. Prohibited list bans selling access to AI services, not AI-made products | None found | Own-work rule: no plagiarism, no content that is not your own work | Verify on Gumroad's prohibited products page; I could not fetch it |
| Lemon Squeezy | No AI-specific rule found | None found | Standard acceptable-use terms | Verify on the live terms page |
| Payhip | No AI-specific rule found | None found | Standard terms | Verify on the live terms page |

Practical reading: on Etsy and KDP, this pipeline produces "AI-generated" content by
their definitions, even after human review and edits. Disclose it. Do not try to argue
that review makes it "AI-assisted". KDP's definition is explicit that substantial edits do
not change the classification.

### Fees by marketplace

US seller, single digital product, figures from official pages where available.

| Marketplace | Per-listing | Per-sale | Payment processing | Other |
|---|---|---|---|---|
| Etsy | $0.20 per listing, renews every 4 months or on sale | 6.5% of order total | 3% + $0.25 (US) | Offsite Ads 15% on attributed orders (12% and mandatory once shop passes $10,000 in any 365 days), capped at $100 per order. Opt-out allowed below the threshold |
| Gumroad | None | 10% + $0.50 on direct sales; 30% flat on Discover marketplace sales | Card processing added on direct sales (roughly 2.9% + $0.30); included in the 30% Discover fee | Merchant of record since 1 Jan 2025. Fees are not refunded when you refund a sale (secondhand) |
| Payhip | None | Free plan 5%; Plus $29/month at 2%; Pro $99/month at 0% | Stripe or PayPal fees on top | Same features on all plans |
| Lemon Squeezy | None | 5% + $0.50 | Included | +1.5% international cards, +1.5% PayPal, +0.5% subscriptions; $15 per chargeback; merchant of record |
| Creative Market | None | Shop keeps 50% of list price by default; rates vary by shop | Included | A fixed per-order platform fee is charged to buyers; refunds only via CM support within a 3-day window |
| Amazon KDP ebook | None | 70% royalty for $2.99 to $12.99 list (band raised from $9.99 on 7 July 2026) minus delivery cost of $0.15 per MB on Amazon.com; 35% outside the band or outside the 70% territories | Included | Public domain content gets 35% only |
| Amazon KDP paperback | None | 60% of list at $9.99 and above, 50% below (since 10 June 2025), minus printing cost. Example from KDP: 250 pages black and white, regular trim: (250 × $0.012) + $1.00 = $4.00 | Included | Low-content books (journals, planners) cannot use Expanded Distribution, cannot form a series, and reviews can take 3 to 4 weeks |
| Teachers Pay Teachers | Basic: $29 one-time; Exclusive: $59.95 per year | Basic keeps 55%, $0.30 per resource; Exclusive keeps 77.5%, $0.15 per resource on orders under $3 and must sell only on TPT | Included | Premium tier retired 1 October 2026. Listed for completeness only; see AI ban |

Worked example at a $6.99 list price, one sale, US buyer, no ads:

| Channel | Fees | Net to you | Net % |
|---|---|---|---|
| Etsy (organic) | $0.20 + $0.45 + $0.46 | $5.88 | 84% |
| Etsy (Offsite Ad attributed, 15%) | above + $1.05 | $4.83 | 69% |
| Gumroad direct | $1.20 + ~$0.50 card | $5.29 | 76% |
| Gumroad Discover | $2.10 | $4.89 | 70% |
| Payhip free plan | $0.35 + ~$0.50 Stripe | $6.14 | 88% |
| Lemon Squeezy | $0.85 | $6.14 | 88% |
| Creative Market | 50% | $3.50 | 50% |

The Etsy listing fee is charged fully to one sale here, which is pessimistic.

### Refund rules and norms

- Etsy: digital listings cannot be returned or cancelled by default and sellers cannot
  set a return policy on them. Buyers can still open a case under Purchase Protection
  for "not as described" or non-delivery, after downloading and after contacting the
  seller and waiting 48 hours. Etsy decides eligibility. Cases count against your
  search ranking (case rate over the past three months is a ranking input).
- Creative Market: refunds and exchanges only through CM support, within 3 days.
- Gumroad: you can refund; a secondhand source says Gumroad keeps its fees on refunds.
- Benchmarks: I found no published refund-rate data for Etsy or Gumroad digital goods.
  One unsourced industry page calls under 2% strong and 2% to 5% average. Treat 3% as a
  working ceiling (estimate) and investigate any product above it.

## Candidate product lines

| Line | Audience | Marketplace | Repeatability | Risk notes |
|---|---|---|---|---|
| Exam-style question banks with worked answers | Students, tutors | Own store (Gumroad or Payhip), Etsy | High, one per topic or chapter | Must be original questions. Never reuse AP, SAT, ACT, or board exam items (see Copyright) |
| Worksheets and lesson plans for one subject and grade | Teachers, homeschool parents | Etsy, own store | High | Align to public standards with attribution. Teacher buyers are the most alert to AI errors |
| Spreadsheet models and trackers (XLSX, plus a Google Sheets copy; verify formula compatibility) | Small business, personal finance | Etsy, Gumroad, Payhip | Medium | Formulas must be tested. Gumroad "Business" and "Education" categories carry higher average prices |
| Checklists and SOP packs for one trade | Small business owners | Gumroad, own store | High | Needs real domain review; regulations differ by region |
| Study guides and flashcard decks | Certification candidates | Own store, Gumroad | High | Do not reproduce certification body objectives verbatim without checking their terms |
| Planners and journals with themed prompts | Consumers | Etsy (PDF), KDP (paperback) | High, low price | Etsy's top category and the most crowded. Keep designs undated so they do not expire in January |
| Niche reference ebooks | Hobbyists, professionals | KDP, Gumroad | Medium | KDP 70% band now to $12.99; delivery fee rewards small files |

### Evidence of what sells

Hard data is scarce; marketplaces do not publish category sales. What can be supported:

- Etsy: planners and printables dominate the digital best-seller pages. Case studies:
  a new printables shop reached $1,000 per month in about four months ($6,161 total);
  another went from about £100 per month with 18 listings to £680 at month nine with 78
  listings and long-tail titles. Both are self-reported.
- Gumroad: a third-party scrape of 146,000 products puts the highest average prices in
  Education ($235 average, but low volume) and Software Development; bundles and courses
  earn the most per product (median about $209 for bundles, $35 for ebooks). The median
  creator is reported at about $72 per month. About 840,000 products were published on
  Gumroad in 2025 alone, which is the saturation signal.
- Seasonality: planner sellers report December and January as roughly 35% of annual
  planner sales with a smaller August to September spike. Teacher buying collapses in
  June and July and turns up in August. One analysis estimates Etsy-wide January sales
  drop 40% to 60% from the December peak while digital planners hold up. All of this is
  self-reported seller data.

Pick a line where you can judge correctness. A wrong answer in a question bank gets a
refund and a one-star review, and on Etsy the case lowers every listing's rank.

## Copyright and quality constraints

### What you can build on

- Common Core State Standards: the public license allows copying, publishing, and
  displaying the standards in whole or in excerpts, with the notice "© Copyright 2010.
  National Governors Association Center for Best Practices and Council of Chief State
  School Officers. All rights reserved." It covers the standards, not the examples, and
  does not allow recasting the text. Quote the code and text, write your own material.
- NGSS: copyright held by the National Academies Press, "NGSS" a trademark of WestEd.
  Commercial use carries restrictions (secondhand; I could not reach the official page).
  Read it before claiming "NGSS-aligned" on a paid product.
- State standards vary. Check each state's terms before using its name in a title.

### What you cannot copy

- AP, SAT, and PSAT questions need written College Board permission (four to six
  weeks), and the form says permission is not granted for use with generative AI. One
  SAT test-prep suit settled for $1 million. Write original questions in the exam's
  style and say "not affiliated with" in the listing.
- Textbooks and commercial curricula: do not mirror chapter structure, problem sets, or
  wording. Use the public standard as the skeleton.
- Trademarks: Etsy flags brand and character names. Check trademark guidelines before
  using an app or publisher name as a keyword.

### Your own copyright is weak

The US Copyright Office's January 2025 report concludes that AI output without sufficient
human authorship is not copyrightable, prompts alone do not qualify, and only the human
parts of a mixed work are protected. Expect copycats: the defensible assets are the
brand, reviews, human-made template design, email list, and iteration speed. Keep a
per-product record of human contributions (outline edits, corrections, layout).

## Agent architecture

```
 demand agent ----> product backlog
 (marketplace search
  suggestions, review
  gaps, seasonal calendar)
        |
        v
 outline agent ----> product spec (audience, scope, sections, length, format,
        |             standards to cite, disclosure text, price band)
        v
 content agent ----> draft content (structured JSON, one call per section,
        |             batch API, schema-validated)
        v
 review agent ----> pass / revise / reject
 (correctness, duplication,
  tone, audience fit,
  policy and IP checks)
        |
        v
 layout pipeline ----> PDF / XLSX / DOCX / EPUB (templates, no agent)
        |
        v
 render check ----> page count, overflow, broken formulas, fonts embedded
        |
        v
 listing agent ----> title, description with AI disclosure, tags, preview images
        |
        v
 human review ----> publish (per marketplace adapter)
        |
        v
 post-publish ----> reviews, cases, refunds, policy changes -> backlog
```

Design notes:

- **Separate content from layout.** Content is structured data (JSON validated against a
  schema per product type). Layout is a template. This lets you re-skin a product line
  and generate variants cheaply, and it keeps the model out of the typesetting.
- **Review agent is adversarial.** It tries to find errors, not to approve. Give it the
  answer key separately from the questions and make it re-derive answers. Track its
  reject rate as a health metric. A reject rate near zero means it is not looking.
- **Policy and IP gate inside review.** The review prompt carries the marketplace's
  prohibited terms, the trademark list, and a known-exam-item check.
- **Render check is code, not a model.** Page count in spec, no overflow, every XLSX
  formula evaluates, fonts embedded, file size under your KDP delivery-fee threshold.
- **Human review is mandatory before publish.** Fifteen to thirty minutes per product.
  Skip this and the reviews will do it for you.
- **Variants.** One run can produce several related products: by grade, region,
  difficulty, undated versus dated. Variants are the leverage; each still gets reviewed.
- **Resumable.** Every stage writes to storage keyed by product id and stage. A failed
  run resumes; it never regenerates paid-for content.

## Production tooling

### Content generation with Claude

Model choice, from the current price list (per million tokens, standard tier):

| Role | Model | Input | Output | Why |
|---|---|---|---|---|
| Outline and section drafting | Claude Sonnet 5.5 | $2 | $10 | Good structure at low cost; use structured outputs so JSON validates |
| Adversarial review and answer re-derivation | Claude Opus 5.5 | $4 | $20 | Correctness is the product; pay for it here |
| Listing copy, tags, alt text | Claude Haiku 5.5 | $0.10 | $0.50 | Cheap, short outputs |

Use the Message Batches API for drafting and review: 50% off input and output, results
within 24 hours, which suits a pipeline nobody is waiting on. Prompt caching stacks with
batch pricing; put the stable style guide and schema first in the prompt.

Rough cost per product (estimate, assumptions stated):

- 40-page workbook: 1 outline, 12 section, 1 consolidation call on Sonnet 5.5, about
  100k input and 60k output tokens. Standard $0.20 + $0.60 = $0.80; batch about $0.40.
- Review on Opus 5.5: 80k input, 10k output. Standard $0.52; batch about $0.26.
- One revise loop on average adds 50% of drafting cost. Listing copy on Haiku: < $0.02.
- Total: about $1.50 to $2.00 per product standard, $0.75 to $1.00 batch, roughly double
  if everything runs on Opus 5.5. Hard cap $5 per product; reject runs that exceed it.

A 10-variant run costs under $20 in tokens. Review time is the constraint, not tokens.

### Layout pipelines

| Output | Tool | Fit | Notes |
|---|---|---|---|
| PDF (worksheets, workbooks, planners) | Typst | Best for data-driven generation. Pass JSON via `--input` and parse with `json(bytes(sys.inputs.data))`; loop in Typst, not in Python string templates | Fast compiles, readable templates, single binary. Typst's own guidance: do logic in Typst, do not generate markup from scripts |
| PDF (brand-heavy, CSS-skilled) | WeasyPrint | HTML and CSS to PDF with `@page`, margin boxes, page counters | Jinja2 templates plus a stylesheet. Slower than Typst but web skills transfer |
| PDF (academic) | LaTeX | Mature math typesetting | Slow and heavy for automation; use only if a line needs it |
| XLSX | openpyxl | Write cells, formulas, named styles, data validation | Formulas are not evaluated by openpyxl; evaluate with LibreOffice headless in the render check |
| DOCX | python-docx or pandoc | Editable deliverables (lesson plans teachers will adapt) | Build from a styled reference .docx so headings and tables inherit your design |
| EPUB | pandoc | Markdown to EPUB with metadata file and CSS | Keep images small; KDP charges per MB on the 70% plan |

### Preview images and mockups

- Render pages to PNG with `pdftoppm` (poppler) or PyMuPDF, then compose with Pillow
  into a cover image, a "what is inside" grid, and a page close-up. Check the
  marketplace's current image size rules before fixing the template.
- Canva Connect API can autofill brand templates and export PNG or PDF, but autofill is
  documented for Canva Enterprise. Pillow over a hand-designed background is enough.
- Generate alt text with Haiku; Etsy reads the first photo as part of query matching.

### Listing copy

- Etsy: 140-character title, all 13 tags as phrases not single words, every relevant
  attribute, most specific category. Word order in the title does not affect ranking
  but affects clicks. Description must include the AI disclosure sentence.
- Gumroad and Payhip: long description with a table of contents, page count, file
  formats, and a sample page image. Both support pay-what-you-want and discount codes.
- KDP: fill the AI-generated declaration on the Content page; do not stuff titles with
  "journal" or "notebook" repeats (KDP warns against it).

## Go-to-market

### Marketplace SEO

Etsy's own handbook describes search as matching then ranking. Matching reads title,
tags, attributes, category, description, first photo, and reviews. Ranking uses
relevancy, listing engagement (views that convert), customer service (rating, response
rate, case rate over three months), recency (small, temporary), and shopper habits.
Etsy Plus, ads, and Star Seller do not change organic rank. Implications:

- Long-tail titles and all 13 tags, generated per variant, are the cheapest lever.
- Conversion matters, so previews and the opening of the description beat listing volume.
- One case or one bad review hits every listing. Review is not optional.

Gumroad Discover costs 30% and is new-customer only; treat it as paid acquisition.

### External traffic

- Pinterest is the main external channel for printables. Evidence is anecdotal (one
  seller attributes 20% of traffic to it) but pins persist, which fits a passive model.
  Automate one pin per product variant from the preview image.

### Bundles

- Once a line has five or more items, list a bundle at 60% to 70% of the summed price
  (estimate; test). Gumroad data shows bundles earning the highest median per product.
- Seasonal bundles (back-to-school in late July, new-year planners in early December)
  listed at least four weeks before the window.

### Email list

- Etsy prohibits adding buyers to a mailing list without express consent and bans
  promotional Convos. Do not scrape Etsy buyer emails.
- Build the list on your direct store instead: a free sample product on Gumroad or
  Payhip collects consented emails, and both let you email your own buyers from the
  platform. Put the store link and the freebie on every PDF's last page.

## Revenue model

- Low to mid price per product, many products. Price bands from the evidence above:
  $3 to $9 for single printables, $8 to $15 for planners and templates, $15 to $30 for
  question banks and study guides with worked answers, $9.99 to $14.99 for KDP
  paperbacks (the 60% tier starts at $9.99).
- Bundles once a line has five or more items.
- Seasonal products priced higher during the window, undated versions year-round.
- Later: a subscription to the full library on Payhip or Lemon Squeezy (both support
  memberships; Lemon Squeezy adds 0.5% on subscriptions).

Scenario, not a forecast (estimate): 40 live products at 3 sales per month each, $6.99
blended price, $5.50 net, is $660 per month, for 20 hours of review plus setup. Base
rates are sobering: third-party estimates put the median TPT seller near $27 per month
and the median Gumroad creator near $72. The case studies above show the top of the
distribution after six to nine months and 60 to 100 listings.

## Cost model

- LLM spend: $1 to $2 per product (estimate above). Budget cap $5 per product, enforced
  in code.
- Marketplace fees: 12% to 24% of gross on Etsy depending on ads, 10% plus card fees on
  Gumroad, 5% plus card fees on Payhip free, 5% + $0.50 on Lemon Squeezy, 50% on
  Creative Market.
- Listing fees: $0.20 per Etsy listing per four months; 40 listings is $8 per cycle.
- Template design: one-off. Hand-build two or three Typst templates or buy a
  commercially licensed template and port it.
- Tooling (Typst, WeasyPrint, pandoc, poppler, openpyxl, python-docx, LibreOffice): free.
- Optional: Payhip Plus at $29 per month pays off above about $967 monthly sales
  (third-party calculation).

## Minimum viable version

1. Pick one product line and one specific first product. Prefer a line where you can
   verify every answer yourself in under an hour.
2. Make the first product partly by hand to learn what good looks like. Save the
   outline, the JSON schema, and the template; they become the pipeline's fixtures.
3. Build the content agent and layout template to reproduce that product from the
   schema. Add the render check.
4. Generate three siblings. Review all three with the same care as the first. Record
   the review agent's findings versus yours to calibrate it.
5. List all four on Etsy with the AI disclosure in the description, and on one direct
   store (Payhip free plan or Gumroad). Use the marketplaces' own analytics for a month.
6. Double down on whichever listing gets views. Generate variants of it. Do not add a
   second product line until the first has ten reviewed products.

## Risks

- **Marketplace AI policies.** TPT banned AI content in October 2026 with no defined
  line between generated and assisted. Etsy and KDP require disclosure and enforce by
  automation. Assume any marketplace can follow TPT: keep the direct store as home base,
  keep listings exportable, re-read policies quarterly.
- **Copyright.** Do not generate derivative works of copyrighted curricula or exams.
  Use public standards with the required attribution and your own framing. Your own
  output has weak copyright protection, so do not plan on it as a moat.
- **Refunds and reviews.** One bad product hurts the whole store, and on Etsy the case
  rate is a ranking input. Human review is the control.
- **Saturation.** Over 840,000 products landed on Gumroad in 2025 alone and planners
  are Etsy's most crowded digital category. Pick narrow audiences, update products so
  they stay current, and compete on correctness and layout.
- **Account risk.** Etsy sellers report automated takedowns with limited appeal. Keep
  spend and inventory small on any single marketplace until it has a track record.
- **Offsite Ads lock-in.** Once an Etsy shop passes $10,000 in a 365-day window,
  Offsite Ads become mandatory at 12% for the life of the shop. Factor that into
  pricing before you get there.

## Decisions still open

These need the owner's input; everything else above has a default.

1. Which product line, and what is the single first product? The recommendation is a
   line you can personally fact-check. The plan cannot choose your domain.
2. Direct store: Payhip (5%, cheapest, memberships built in) or Gumroad (10% + $0.50,
   larger audience, Discover marketplace). Lemon Squeezy if you expect international
   buyers and want merchant-of-record VAT handling from day one.
3. Whether to list on KDP at all. Paperback planners add a physical channel at $2 to $4
   net per book and a 3 to 4 week review queue, and the three-titles-per-day cap limits
   batch publishing.
4. Brand name and shop persona. The AI disclosure is non-negotiable; whether to name a
   human reviewer on the product is a choice. It helps trust and the copyright record;
   it also ties your name to every product.
5. Per-product LLM budget cap. Default $5. Raise it only for products priced above $20.
6. Who does the human review, and how long is acceptable per product. Default is you,
   30 minutes, and no publish without it. If you want to delegate, name the reviewer and
   the checklist they sign.
7. Template design: build in Typst yourself, or buy a licensed template and port it.

## Sources

Marketplace AI policies

- Etsy Creativity Standards: https://www.etsy.com/legal/creativity
- Etsy Seller Policy (AI disclosure): https://www.etsy.com/legal/sellers/
- Etsy, "What is Etsy's stance on AI creations?" (prompt bundles prohibited): https://www.etsy.com/seller-handbook/article/1275449912004
- Etsy Help, "What Can I Sell on Etsy?": https://help.etsy.com/hc/en-us/articles/360024112614-What-Can-I-Sell-on-Etsy
- Etsy seller reports of automated Creativity Standards takedowns: https://www.valueaddedresource.net/etsy-creativity-standards-takedowns-no-appeal/
- Amazon KDP Content Guidelines (AI-generated vs AI-assisted definitions): https://kdp.amazon.com/en_US/help/topic/G200672390
- KDP daily limit of three new titles (Authors Guild): https://authorsguild.org/news/amazon-adds-to-kdp-generative-ai-policy-caps-daily-self-publishing-uploads/
- Chalkbeat, TPT to ban AI-generated resources (15 Oct 2026): https://www.chalkbeat.org/2026/10/15/teachers-pay-teachers-to-ban-ai-generated-teaching-resources/
- Chalkbeat, AI slop on TPT (3 Aug 2026): https://www.chalkbeat.org/2026/08/03/ai-slop-on-teachers-curriculum-marketplace/
- Mike Lane, TPT AI policy and existing listings: https://mikellane.com/tpt-ai-policy/
- Creative Market, "Navigating Our New AI Label": https://support.creativemarket.com/hc/en-us/articles/26926388691099-Navigating-Our-New-AI-Label
- Creative Market, reporting a product (Missing AI Label): https://support.creativemarket.com/hc/en-us/articles/41301796575259-Reporting-a-Product-on-Creative-Market
- Gumroad prohibited products summary (secondhand; AI services only): https://www.inkfluenceai.com/learn/can-you-sell-ai-generated-books

Fees

- Etsy Fees and Payments Policy: https://www.etsy.com/legal/fees/
- Etsy Offsite Ads (15% / 12%, $10,000 threshold, $100 cap): https://help.etsy.com/hc/en-us/articles/360000338367-How-Etsy-s-Offsite-Ads-Work
- Gumroad pricing (10% + $0.50 direct, 30% Discover, merchant of record from 1 Jan 2025): https://gumroad.com/pricing
- Gumroad fees help article: https://help.gumroad.com/article/66-gumroads-fees
- Lemon Squeezy pricing: https://www.lemonsqueezy.com/pricing
- Lemon Squeezy fee docs (surcharges): https://docs.lemonsqueezy.com/help/getting-started/fees
- Payhip FAQ (plans and fees): https://payhip.com/faq
- Payhip Plus break-even calculation (third party): https://sellfy.com/blog/payhip-pricing/
- Creative Market shop sales (50% default): https://support.creativemarket.com/hc/en-us/articles/201193714-All-About-Shop-Sales-Analytics
- KDP eBook list price requirements ($2.99 to $12.99 band from 7 July 2026): https://kdp.amazon.com/en_US/help/topic/G200634560
- KDP digital book pricing (70% formula, $0.15/MB delivery): https://kdp.amazon.com/en_US/help/topic/G200634500
- KDP earnings page (paperback printing cost example): https://kdp.amazon.com/earn
- KDP paperback royalty change 10 June 2025: https://kdp.amazon.com/help/topic/G201834330
- KDP low-content books: https://kdp.amazon.com/en_US/help/topic/GGE5T76TWKA85DJM
- KDP Expanded Distribution (not for low-content): https://kdp.amazon.com/en_US/help/topic/GQTT4W3T5AYK7L45
- TPT Become a Seller (Basic and Exclusive terms): https://www.teacherspayteachers.com/become-a-seller
- TPT membership types (Premium retired 1 Oct 2026): https://help.teacherspayteachers.com/hc/en-us/articles/360040842852-What-membership-types-are-available

Refunds

- Etsy, downloading digital items (no returns on digital): https://help.etsy.com/hc/en-us/articles/115013328108-How-to-Download-a-Digital-Item
- Etsy Cases Policy: https://www.etsy.com/legal/policy/cases-policy/243306189901
- Creative Market refund and exchange policy (3-day window): https://support.creativemarket.com/hc/en-us/articles/236189908-Refund-Exchange-Policy
- Digital product refund benchmark (unsourced, treat as rough): https://taglab.net/?p=21775

Demand evidence and seasonality

- Etsy best-selling digital products page: https://www.etsy.com/market/best_selling_digital_products_2025
- Printables shop case study, $6,161 in four months: https://www.makingsenseofcents.com/2025/03/how-i-made-6161-in-just-4-months-with-a-new-etsy-printables-shop.html
- Printables honest math, £80 to £680 per month: https://www.lilachbullock.com/selling-printables-passive-income-honest-math/
- Gumroad category data, 146k products: https://insightraider.com/answers/what-digital-products-sell-best-on-gumroad
- Gumroad per-format medians, 840k products in 2025: https://profitable.app/gumroad/stats
- TPT seller income distribution (third-party estimate): https://seolumina.com/blog/how-much-do-tpt-sellers-make-in-2026-real-data-income-breakdown
- TPT summer slump and August recovery: https://www.rhodadesignstudio.com/summer-sales/
- Planner seasonality (December and January about 35%): https://www.promptlesspress.com/sell-planners-on-etsy
- Etsy January slump estimate: https://www.insightagent.app/guides/etsy-sales-january-post-holiday-slump
- Pinterest share of one seller's traffic: https://digitalbizplr.com/blogs/learn/pinterest-etsy-traffic-strategy

Copyright and standards

- Common Core public license: https://www.thecorestandards.org/public-license/
- Common Core commercial license: https://thecorestandards.org/commercial-license/
- NGSS copyright and trademark summary (secondhand): https://raw.githubusercontent.com/withmarbleapp/os-taxonomy/master/PROVENANCE.md
- College Board permission form and generative AI restriction: https://privacy.collegeboard.org/request-form/instructions
- College Board test-prep settlement, $1 million: https://www.nbcnews.com/news/amp/wbna23262842
- US Copyright Office, Copyrightability report (Jan 2025), summary: https://www.skadden.com/insights/publications/2025/02/copyright-office-publishes-report
- Etsy buyer email consent rules (EcommerceBytes): https://www.ecommercebytes.com/2024/01/07/etsy-cracks-down-on-marketing-to-buyers/

Marketplace SEO

- Etsy, How Etsy Search Works: https://www.etsy.com/seller-handbook/article/how-etsy-search-works/375461474487

Tooling and pricing

- Claude pricing (models, batch 50% discount, caching): https://docs.anthropic.com/en/docs/about-claude/pricing
- Claude batch processing: https://docs.anthropic.com/en/docs/build-with-claude/batch-processing
- Typst, automated document generation: https://typst.app/blog/2025/automated-generation
- typst-py (Python bindings, sys_inputs example): https://typst-py.readthedocs.io/en/latest/
- WeasyPrint documentation: https://doc.courtbouillon.org/weasyprint/stable/
- pandoc manual (EPUB, DOCX reference documents): https://pandoc.org/MANUAL.html
- python-docx and openpyxl: https://python-docx.readthedocs.io/ and https://openpyxl.readthedocs.io/
- Canva Connect API autofill (Enterprise) via n8n: https://www.canva.dev/blog/developers/automate-canva-with-n8n/
