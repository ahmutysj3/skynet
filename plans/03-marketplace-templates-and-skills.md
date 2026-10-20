# Plan 03: Marketplace Templates and Skills

## Summary

Package agent capabilities as artifacts other people install and run themselves: Claude
Code skills and plugins, MCP servers, n8n and Zapier and Make templates, Notion and
Airtable automations, and prompt libraries. You sell once or by subscription, and the
customer pays the compute. There is no pipeline to keep running.

## Why it is the most passive option

- Zero running cost. Customers run the agent on their own accounts.
- No data to keep fresh and no sources to break.
- Marketplaces handle discovery, payment, and delivery.
- Support is mostly answering the same five questions, which a README can do.

## Why it is also the most crowded

Low barrier means many sellers. Differentiation comes from depth in one workflow, polish,
documentation, and trust. A single excellent artifact outsells twenty mediocre ones.

## Candidate artifact types

| Artifact | Where it sells | Price shape | Build effort |
|----------|----------------|-------------|--------------|
| Claude Code skill or plugin | Plugin marketplaces, own site, GitHub sponsors | One-off or sponsor | Low |
| MCP server for a niche API or data source | MCP registries, own site | Free with paid tier | Medium |
| n8n / Make / Zapier workflow template | Platform template galleries, Gumroad | One-off | Low |
| Notion or Airtable system with AI steps | Notion marketplace, Gumroad | One-off | Low |
| Prompt and agent config pack for one profession | Gumroad, own site | One-off | Very low |
| GPT-style app or custom assistant | Platform stores | Revenue share | Low |

## Picking the first artifact

Ask three questions:

1. What have you built for yourself that saved real time?
2. Which profession or role would pay to skip the setup?
3. Which marketplace already has buyers searching for it?

The intersection is the first product. Build one, not a catalogue.

## Agent architecture

This plan does not need a running agent of its own. The agent is the product. The
development loop benefits from automation though:

```
 idea backlog ----> prototype (build the skill or workflow)
                        |
                        v
                   eval agent ----> runs the artifact against test cases,
                                     scores output, flags regressions
                        |
                        v
                   docs agent ----> README, install guide, FAQ, demo transcript
                        |
                        v
                   packaging ----> marketplace listing, screenshots, pricing
                        |
                        v
                   feedback monitor ----> issues, reviews, support emails
                   (weekly digest)
```

Design notes:

- **Evals are the moat.** A skill with a test suite that proves it works is worth far more
  than one with marketing copy. Ship the evals with the product where the platform allows.
- **Documentation is the support team.** Write it so that a first-time user never needs to
  email you.
- **Version carefully.** Breaking changes cost refunds. Pin dependencies and model IDs.

## Revenue model

- One-off purchase for templates and packs.
- Free tier plus paid tier for MCP servers and skills with hosted components.
- Sponsorship or licensing for open-source artifacts used commercially.
- Bundles once there are three or more related artifacts.

## Cost model

- Near zero ongoing. Marketplace fees on sales.
- Your time for the first build and for updates when platforms change.

## Minimum viable version

1. Pick one artifact from the table above and one target role.
2. Build it to solve one complete workflow end to end. No half features.
3. Write ten test cases and make them pass.
4. Record a two-minute demo and write a README that covers install, use, and the three most
   likely failures.
5. List it on one marketplace and one owned page with a checkout.
6. Post it in one community where the target role gathers. Once.
7. Iterate on the feedback for a month before starting the second artifact.

## Risks

- **Platform changes.** A marketplace can change terms or a platform can break your
  artifact. Keep the artifact portable and own the customer relationship where possible.
- **Copying.** Templates are easy to clone. Compete on evals, docs, and updates.
- **Support creep.** Set expectations in the listing. Charge for custom work.

## Open questions to expand

- Which artifact type and target role?
- Which marketplace first, and does it allow a link to an owned checkout?
- One-off or subscription?
- Will the first artifact be open source with a paid layer, or closed?
