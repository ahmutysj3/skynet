# Plan 04: Agent-Generated Digital Products

## Summary

An agent pipeline produces finished digital goods, such as workbooks, study guides,
question banks, lesson plans, spreadsheet models, checklists, and planners. They are sold
on marketplaces like Gumroad, Etsy, Amazon KDP, or Teachers Pay Teachers. After the
pipeline is built, the work is choosing what to make next and reviewing output before
listing.

## Why it is close to passive

- Each product sells indefinitely with no per-sale effort.
- Marketplaces handle payment, delivery, and most discovery.
- The agent does drafting, formatting, and variant generation.
- Running cost is only the LLM spend to generate a product.

## The quality constraint

Marketplaces are flooded with low-effort AI products and buyers have learned to spot them.
Products that sell have a clear audience, a specific problem, a professional layout, and
content that is correct. The agent produces the draft. You own the standard.

## Candidate product lines

| Line | Audience | Marketplace | Repeatability |
|------|----------|-------------|---------------|
| Exam question banks with worked answers | Students, tutors | Own site, Gumroad | High, one per exam or chapter |
| Lesson plans and worksheets for one subject and grade | Teachers | Teachers Pay Teachers | High |
| Spreadsheet models and trackers | Small business, personal finance | Gumroad, Etsy | Medium |
| Checklists and SOP packs for one trade | Small business owners | Gumroad, own site | High |
| Study guides and flashcard decks | Certification candidates | Own site, Gumroad | High |
| Planners and journals with themed prompts | Consumers | Etsy, KDP | High, low price |
| Niche reference ebooks | Hobbyists, professionals | KDP, Gumroad | Medium |

Pick a line where you can judge correctness. A wrong answer in a question bank gets a
refund and a one-star review.

## Agent architecture

```
 demand agent ----> product backlog
 (marketplace search
  volumes, review gaps,
  seasonal timing)
        |
        v
 outline agent ----> product spec (audience, scope, sections, length, format)
        |
        v
 content agent ----> draft content (structured JSON, one call per section)
        |
        v
 review agent ----> pass / revise / reject
 (correctness, duplication,
  tone, audience fit)
        |
        v
 layout pipeline ----> PDF / XLSX / DOCX / EPUB (templates, no agent)
        |
        v
 listing agent ----> title, description, tags, preview images
        |
        v
 human review ----> publish
```

Design notes:

- **Separate content from layout.** Content is structured data. Layout is a template. This
  lets you re-skin a product line and generate variants cheaply.
- **Review agent is adversarial.** It tries to find errors, not to approve. Track its
  reject rate as a health metric.
- **Human review is mandatory before publish.** Fifteen minutes per product. Skip this and
  the reviews will do it for you.
- **Variants.** One pipeline run can produce several related products: by grade level,
  by region, by difficulty. Variants are where the leverage is.

## Revenue model

- Low to mid price per product, many products.
- Bundles once a line has five or more items.
- Seasonal products priced higher during the window.
- Later: a subscription to the full library.

## Cost model

- LLM spend per product. Set a budget per product and reject runs that exceed it.
- Marketplace fees per sale.
- Template design: one-off, can be bought.

## Minimum viable version

1. Pick one product line and one specific first product.
2. Make the first product partly by hand to learn what good looks like.
3. Build the content agent and layout template to reproduce that product.
4. Generate three siblings. Review all three with the same care as the first.
5. List all four. Use the marketplace's own analytics for a month.
6. Double down on whichever listing gets views. Generate variants of it.

## Risks

- **Marketplace AI policies.** Some marketplaces restrict or label AI-generated goods.
  Read the policy for each marketplace before building for it.
- **Copyright.** Do not generate derivative works of copyrighted curricula or exams.
  Use public standards and your own framing.
- **Refunds and reviews.** One bad product hurts the whole store. Human review is the
  control.
- **Saturation.** Pick narrow audiences and update products so they stay current.

## Open questions to expand

- Which product line, and what is the single first product?
- Which marketplace, and what does its AI policy say?
- What is the per-product LLM budget?
- Who does the human review step, and how long is acceptable per product?
