# Plans

General plans for the "closest to passive" agentic business ideas. Each plan is a
starting point meant to be expanded, not a finished spec.

| Plan | Idea | Passivity | Upfront effort | Status |
|------|------|-----------|----------------|--------|
| [01-niche-data-products.md](01-niche-data-products.md) | Agent collects a niche dataset nightly, sold by subscription or API | High | Medium | **Active.** Revenue business |
| [02-programmatic-content-sites.md](02-programmatic-content-sites.md) | Agent generates and maintains long-tail reference pages, monetised with ads and affiliates | High | Medium to high | Parked. Free tier of plan 01 absorbs the viable part |
| [03-marketplace-templates-and-skills.md](03-marketplace-templates-and-skills.md) | Package agents as sellable skills, MCP servers, and automation templates | Very high | Low to medium | **Active.** Public repo as Steerwell marketing |
| [04-agent-generated-digital-products.md](04-agent-generated-digital-products.md) | Agent pipeline produces digital goods sold on marketplaces | Very high | Low | Parked. Marketplace AI policies tightening |

Decisions about which plans to pursue are recorded in [DECISIONS.md](DECISIONS.md).

## Shared principles

These apply to every plan and are not repeated in each file.

1. **Pick one narrow vertical you know.** The agent is a commodity. Domain knowledge,
   distribution, and knowing which errors matter are the moat.
2. **Charge from day one.** A small price validates demand before polish is worth it.
3. **Cap the spend.** Hard limits on tokens, tool calls, and crawl volume per run. One
   runaway loop should never cost more than a day's revenue.
4. **Design for your own absence.** Every pipeline needs a dead-letter queue, a daily
   health email, and a graceful failure message to customers.
5. **Quality over volume.** Thin AI output is penalised by search engines, rejected by
   marketplaces, and refunded by customers. Fewer, better artifacts win.

## Shared infrastructure

Candidates for a common base that all four plans can reuse. See each plan's
"Agent architecture" section for where it plugs in.

- Scheduler: GitHub Actions cron, or a small VPS with cron and systemd timers.
- Agent runtime: Claude API via the Agent SDK for multi-step work, or a single
  structured-output call where the task is simple.
- Storage: SQLite or Postgres for structured data, object storage for artifacts.
- Payments: Stripe for subscriptions, marketplace-native payouts where applicable.
- Observability: one daily digest email, error alerts via a webhook, a spend dashboard.

## Suggested order

Decided 2026-10-20. Build plan 03 first as a public Steerwell repository, since it costs
nothing to run and produces a visible artifact within two weeks. Use it to choose a niche
and to seed an audience. Then build plan 01 as the revenue product, with the plan 03 repo
and README as one of its lead channels. Plans 02 and 04 are parked; revisit only if the
conditions noted in DECISIONS.md change.
