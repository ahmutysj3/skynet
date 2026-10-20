# Plan 03: Marketplace Templates and Skills

Researched 2026-10-20. Figures are taken from the sources listed at the end. Where a
number is an estimate it is labelled as one and the assumption is stated.

## Summary

Package agent capabilities as artifacts other people install and run themselves: Claude
Code skills and plugins, MCP servers, n8n and Zapier and Make templates, Notion and
Airtable automations, prompt libraries, and ChatGPT-style apps. You sell once or by
subscription, and the customer pays the compute. There is no pipeline to keep running.

The research changes one assumption in the original plan. Most of the platforms in this
space do not sell artifacts for you. Anthropic's directory, the official MCP registry, the
n8n library, Zapier, and Make all list free artifacts and do not process payments. Notion
Marketplace is the only first-party store in the list with built-in paid checkout. So the
realistic shape of this business is: free listing on the platform for discovery, paid
checkout on Gumroad or Lemon Squeezy, and the paid layer is either a private repo, a
license key, a bigger pack, or a hosted tier.

## Why it is the most passive option

- Zero running cost. Customers run the agent on their own accounts and API keys.
- No data to keep fresh and no sources to break, unless the artifact wraps a third-party
  API (then the API is the thing that breaks).
- Platforms handle discovery and delivery. Payment is handled by a merchant-of-record
  checkout (Lemon Squeezy, Gumroad, Notion) that collects VAT and sales tax for you.
- Support is mostly answering the same five questions, which a README can do.
- Updates are a git push. Claude Code marketplaces, the Anthropic directory, and the MCP
  registry all pick up new versions from a tracked branch or a new package version.

## Why it is also the most crowded

Low barrier means many sellers. Glama alone indexes tens of thousands of open-source MCP
servers (reported figures range from 21,000 to 50,000 depending on date). Community skill
registries index thousands of SKILL.md files.

Buyers are also sceptical of thin AI-generated listings. Notion Marketplace reviewers
reject "AI-generated content that fails to count as a true template" (reported by course
sites, not confirmed in Notion's own text). Etsy banned standalone AI prompt packs in 2025.
Gumroad's prohibited list reportedly bars selling access to AI tools and chatbots (claim
from a competitor, not verified against Gumroad's own terms). Differentiation comes from
depth in one workflow, evals that prove it works, documentation, and trust. A single
excellent artifact outsells twenty mediocre ones.

## Candidate artifact types

| Artifact | Where it sells | Price shape | Build effort | Paid listing on platform? |
|----------|----------------|-------------|--------------|---------------------------|
| Claude Code skill or plugin | Own marketplace repo, Anthropic directory, Agensi / Agent37 / SkillHQ, Gumroad | One-off pack, or subscription on third-party stores | Low | No on Anthropic surfaces. Yes on third-party skill stores |
| MCP server for a niche API or data source | Official MCP registry, Glama, Smithery, PulseMCP, Anthropic directory as a connector | Free server with paid hosted tier, per-call via ATXP or Apify | Medium | No on registries. Yes on Apify (80/20) |
| n8n workflow template | n8n template library and Creator Hub, Gumroad | One-off, often bundles | Low | Creator program still in progress, details may change |
| Make or Zapier template | Platform galleries (free), Gumroad | One-off | Low | No. Zapier templates require a partner integration |
| Notion or Airtable system with AI steps | Notion Marketplace, Gumroad | One-off | Low | Yes. Notion processes payment and tax |
| Prompt and agent config pack for one profession | Gumroad, Lemon Squeezy, own site | One-off | Very low | Not applicable |
| GPT-style app or custom assistant | OpenAI app directory | Revenue share promised, not confirmed | Low | No digital goods sales inside ChatGPT at launch |

### Channel by channel

**Claude Code plugins and skills.** A plugin is a directory with an optional
`.claude-plugin/plugin.json` manifest and component folders (`skills/`, `commands/`,
`agents/`, `hooks/`, `.mcp.json`). Distribution is a git repo containing a
`.claude-plugin/marketplace.json` with `name`, `owner`, and a `plugins` array. Users run
`claude plugin marketplace add owner/repo` then `claude plugin install name@marketplace`.
There is no submission form for your own marketplace, and a private repo is a private
marketplace: anyone who can clone it can install from it. That is the mechanism for a paid
plugin. Sell access to the private repo, or ship a zip that users load with
`--plugin-dir`. Auto-update is off by default on the user's side.

Anthropic's directory (claude.ai/directory) is the public catalogue for claude.ai, Cowork,
and Claude Code. Anyone on a paid plan can submit, there is no partner program, and every
version gets automated validation, a security scan, and a human review for a new listing.
The repository must be public before the listing goes live, so a directory listing is a
free product by definition. The directory policy requires a privacy policy, verified
support contact, documentation, a test account, and three working example prompts. It
prohibits software that moves money, generates images, video, or audio, or serves ads.
It says nothing about paid tiers or external purchase links. Plugin names starting with
`claude-`, `anthropic-`, or `cc-plugin-` fail validation. Submission limit is 10 per
organisation per 24 hours.

Paid skill marketplaces exist but are small and third party. Stated terms: Agent37 pays
creators 80% of subscription revenue; Agensi takes 30% and reports most skills priced at
$5 to $15 one-off; SkillHQ takes 15% with skills priced from 2 to 50 euros. All three have
a commercial stake in those claims.

**MCP servers.** The official registry (registry.modelcontextprotocol.io) is in preview,
announced 2025-09-08, with the v0.1 API frozen since 2025-10-24. It stores metadata only.
You publish the package to npm or PyPI first, then run `mcp-publisher init`,
`mcp-publisher login github`, and `mcp-publisher publish`. GitHub-authenticated names use
the `io.github.<user>/` prefix; domain names need a DNS or HTTP challenge. An npm package
must carry an `mcpName` field matching `server.json`. Directories such as Glama, Smithery,
and PulseMCP crawl GitHub and the registry, rank what they find, and let you claim your
listing. Glama reportedly checks for a README, a valid license, and known vulnerabilities.
None of these process payments. Remote servers can be submitted to Anthropic's directory as
an MCP connector, listed as Community by default and escalated to Verified at Anthropic's
discretion; desktop extension (MCPB) listings are deprecated there.

Paid MCP options are early. Apify Store lets an Actor charge pay-per-event with creators
keeping 80% minus platform costs; rental pricing is retired as of 2026-10-01. ATXP offers
pay-per-call billing where the agent's wallet pays before the tool runs. One developer
reported shipping an MCP tool on Apify at $0.07 per call and having no paying users two
weeks later. The Serena project reports that GitHub Sponsors is its only income.

**n8n.** The docs say n8n is "working on a creator program, and developing a marketplace
of templates" and that details are likely to change. Submission is through the Creator Hub.
A community forum report says the Creator Hub requires three free workflows before a
creator can sell anything; this is a user report, not an official rule. Creators sell n8n
JSON on Gumroad in the meantime. Observed listings: a bundle at $19.99 showing 194 sales, a
25-template pack showing 6 sales, and one creator reporting $174 of Gumroad revenue in a
month after three months of YouTube and Medium posts.

**Zapier.** Zap templates can only be built by an integration that is in beta or launched
in the Integration Partner Program, so an independent creator cannot list them. Zapier
Agents can be shared as template links and there is a curated agent template gallery, but
no documented public submission route or payment.

**Make.** A team template can be submitted for the public library with "Request approval"
and a Make admin reviews it. There is no creator payment. Make's affiliate program pays 35%
on referred paid accounts for 12 months, paid once you reach $100 and three paying users. That is a side income from
template READMEs, not a template sale.

**Notion Marketplace.** Join a waitlist, get approved, and onboard with Stripe. Notion's
English help page lists a 10% fee plus $0.40 per transaction; the en-GB page lists 8% plus
$0.40. Treat the rate as 8 to 10% until confirmed. Funds are held 14 days, payouts run
biweekly on Thursdays with a $20 minimum, non-US creators pay an extra 1% FX fee, and
buyers can refund within 14 days. Notion handles VAT and sales tax. Guidelines require
original work with "unique value compared to existing content". Review can take up to two
weeks per third-party reports. Titles may not contain "Notion" or "template".

**Gumroad.** Direct sales are 10% plus $0.50 per sale with no monthly fee. Sales that
come through Gumroad Discover are a flat 30%. Third-party sources disagree on whether card
processing (about 2.9% plus $0.30) is inside or on top of the 10%; the official pricing
page wording is "10% + 50¢" so budget for processing on top. Gumroad is a merchant of
record for tax purposes.

**Lemon Squeezy.** 5% plus $0.50 per transaction, plus 1.5% for non-US transactions, 1.5%
for PayPal, and small surcharges for subscriptions and affiliate referrals. It is a merchant
of record, so it files VAT and sales tax, and it issues license keys, which matters for a
paid plugin. One third-party listing shows a 3.5% plus $0.30 tier; the official docs show one
rate.

**GitHub Sponsors.** Zero fee on sponsorships from personal accounts. Organisation-funded
sponsorships pay up to 6% (3% card processing, 3% service fee). A `FUNDING.yml` adds the
sponsor button. Sponsor-only tiers can gate a private repo, which is a workable paid layer
for an open-source MCP server.

**OpenAI GPT Store and app directory.** The GPT Store launched January 2024 with a promise
of an engagement-based revenue programme for US builders. No source confirms that
programme paid out at scale or what it pays now. The successor surface is the Apps SDK and
app directory (public submissions since December 2025). At launch, apps could link out for
physical goods only; digital goods, subscriptions, and in-app purchases were not allowed
and OpenAI had announced no revenue share. Treat this channel as a free distribution
experiment, not a revenue line, until OpenAI publishes terms.

### What sells, with evidence

| Evidence | Figure | Reliability |
|----------|--------|-------------|
| Notion template business listed for sale, June 2025 | $28,371 ARR, 1,000 customers, 26 templates (14 paid) over two years | Listing on a marketplace for small businesses, self-reported |
| Smaller Notion template platform, October 2025 | $1,200 annual revenue, 150 customers | Same |
| Solo Notion creator blog post | $250 total, first $50 after months of zero | Self-reported |
| Easlo, Thomas Frank (Notion) | $500,000 and higher claimed | Promotional, unverified |
| Claude skill pack, one creator | "over $10,000 passively since March", one-off purchase | Self-reported, sells a course |
| n8n creator on Gumroad | $174 in July 2025, third month of revenue | Self-reported |
| n8n bundle on Gumroad | 194 sales shown at $19.99 | Seller-displayed count |
| Apify MCP tool at $0.07 per call | Zero paying users after two weeks | Self-reported |

Typical price points from the same sources: n8n JSON templates $19 to $79; Notion
templates $19 to $79 with simple ones at $5 to $15 and bundles at $50 to $150; skills on
third-party stores $5 to $15 one-off. Nobody in the evidence set got rich from a single
listing. The one creator who reported five figures from a skill pack says distribution
mattered more than the skill.

What top sellers have in common across sources:

- A narrow niche with a named buyer ("indie hacker startup system", not "productivity").
- A walkthrough video. One automation-template guide calls it the top conversion driver.
- A free version that proves competence, then a paid pack or bundle.
- An email list or audience built before launch.
- Four to eight distinct workflows in one pack rather than hundreds of near-duplicates.

## Picking the first artifact

Ask three questions:

1. What have you built for yourself that saved real time?
2. Which profession or role would pay to skip the setup?
3. Which marketplace already has buyers searching for it?

The intersection is the first product. Build one, not a catalogue.

Given the channel research, two shapes score best for a solo operator today:

- **A Claude Code plugin with a free core and a paid pack.** The free plugin goes in your
  own marketplace repo and the Anthropic directory. The paid pack (extra skills, evals,
  reference files) is a private repo sold through Lemon Squeezy with a license key. Low
  build cost, zero hosting, direct customer relationship.
- **A Notion system with AI steps.** Notion is the only platform here with first-party
  paid checkout, tax handling, and a review process that filters out junk. Build cost is
  low. The 8 to 10% fee is cheaper than Gumroad and comparable to Lemon Squeezy.

MCP servers are the most defensible long term but the paid path is immature. Build one if
the free version also feeds a data product (plan 01). Zapier and Make are discovery only.

## Agent architecture

This plan does not need a running agent of its own. The agent is the product. The
development loop benefits from automation though:

```
 idea backlog ----> prototype (build the skill, server, or workflow)
                        |
                        v
                   eval agent ----> claude plugin eval / skill-creator evals /
                   (CI, gated)       MCP Inspector smoke tests; scores output,
                        |            compares against no-plugin baseline
                        v
                   docs agent ----> README, install guide, FAQ, demo transcript,
                        |            2-minute video script
                        v
                   packaging ----> marketplace.json / server.json / Notion listing,
                        |           screenshots, license key product on checkout
                        v
                   release ----> tag, bump version, push tracked branch
                        |         (directory and marketplaces pick it up)
                        v
                   feedback monitor ----> GitHub issues, store reviews, support
                   (weekly digest)         inbox, directory usage tab
```

Design notes:

- **Evals are the moat.** `claude plugin eval` runs each case three times with the plugin
  and three times without, and reports the difference. A positive delta is proof the
  artifact does something Claude would not do alone. Ship the eval suite with the free
  version. Every run costs real model calls on your account, so gate CI on a small smoke
  subset and run the full suite before a release.
- **Documentation is the support team.** The Anthropic directory requires docs, a support
  contact, and three working example prompts anyway. Write them once and reuse them in
  the listing.
- **Version carefully.** If `plugin.json` sets `version` and you push without bumping it,
  users on `claude plugin update` stay on the old copy. Never rename a published plugin;
  use the marketplace `renames` map if you must. Pin model IDs in skills that depend on
  specific behaviour. For MCP servers keep `server.json` version in sync with the npm or
  PyPI version.

### Build tooling

**Skill (SKILL.md).** A skill is a folder with `SKILL.md` and optional `scripts/`,
`references/`, and `assets/`. Frontmatter needs `name` (max 64 chars, lowercase, digits,
hyphens) and `description` (max 1024 chars, non-empty) under the Agent Skills open
standard. Claude Code adds fields such as `allowed-tools`, `disable-model-invocation`,
`context: fork`, and `argument-hint`; outside Claude Code only `name`, `description`,
`license`, `compatibility`, `metadata`, and `allowed-tools` are accepted, so keep the
portable subset in the free version. Keep `SKILL.md` under 500 lines and move long
reference material into linked files. The name and description sit in context every turn,
so the description decides whether the skill triggers. Validate with `skills-ref validate
./my-skill` (reference library) and `claude plugin validate --strict ./my-plugin`.

**Plugin layout.**

```
my-plugin/
├── .claude-plugin/plugin.json    # name (required), version, description, author,
│                                 # homepage, repository, license, keywords, userConfig
├── skills/<name>/SKILL.md
├── agents/*.md
├── hooks/hooks.json
├── .mcp.json                     # bundled MCP servers, ${CLAUDE_PLUGIN_ROOT} paths
├── evals/<case>/prompt.md        # + graders/*.md
└── README.md
```

`userConfig` lets the plugin prompt for an API key and store it in the secure credential
store, which is how a paid hosted tier gets its key without the user editing settings.

**Evals.** `claude plugin eval init` interviews you and writes cases. Each case is a
`prompt.md` plus graders of type `regex`, `tool_used`, `tool_order`, `file_exists`, `llm`,
or `baseline`. Mock MCP servers live under `evals/mocks/<server>/<tool>.md` so the suite
runs without real credentials. The skill-creator plugin has a separate `evals/evals.json`
format and a description-tuning script; the two tools do not read each other's files.
Pick one.

**MCP server scaffolding.**

| Language | Package | Minimal shape | Local test |
|----------|---------|---------------|------------|
| TypeScript | `@modelcontextprotocol/server` (v2; v1 is `@modelcontextprotocol/sdk`) | `new McpServer({name, version})`, `server.registerTool(name, {description, inputSchema: z.object({...})}, handler)`, `server.connect(new StdioServerTransport())` | MCP Inspector, or a client script |
| Python | `mcp[cli]` on PyPI, Python 3.11+ | `@mcp.tool()` on a typed function; docstring becomes the schema | `uv run mcp dev server.py` opens the Inspector |

Both support stdio and Streamable HTTP. Ship stdio for local installs and Streamable HTTP
for a hosted tier. Put a `README`, a license file, and `mcpName` in `package.json` before
publishing so Glama and the registry accept it.

**Licensing options for a paid, source-visible artifact.**

| License | What it does | Fit |
|---------|--------------|-----|
| MIT or Apache-2.0 | Fully open. Anthropic's example skills are Apache-2.0 | Free core, directory listings |
| Functional Source License (FSL) | Source available, bars competing commercial use, converts to Apache-2.0 or MIT after two years | Free MCP server where you want to stop resellers but not users |
| Business Source License (BSL) | Same idea, four-year default, custom Additional Use Grant | Overkill for a solo seller |
| PolyForm Noncommercial / Small Business | Free for non-commercial or small companies, paid license above a threshold | Paid pack sold to companies, free to hobbyists |
| Plain proprietary EULA, per-seat | What Gumroad and Lemon Squeezy sellers use by default | Paid skill packs and templates |

None of the source-available licenses stop copying by a buyer; they give you standing, not
enforcement. Compete on updates and evals. This is not legal advice.

## Revenue model

- One-off purchase for templates and packs. $19 to $49 is the observed band.
- Free tier plus paid tier for MCP servers and skills: free server on the registry, paid
  hosted endpoint, bigger limits, or extra tools, billed by subscription on Lemon Squeezy.
- Sponsorship or licensing for open-source artifacts used commercially. GitHub Sponsors
  takes 0% from individual sponsors.
- Bundles once there are three or more related artifacts. Bundles at $50 to $150 are
  common on Notion and n8n listings.

Fee comparison at a $29 one-off sale, US buyer, card payment:

| Checkout | Fee rule | Fee | Net to you | Estimate note |
|----------|----------|-----|------------|---------------|
| Lemon Squeezy | 5% + $0.50 | $1.95 | $27.05 | Add $0.44 for a non-US buyer |
| Notion Marketplace | 8 to 10% + $0.40 | $2.72 to $3.30 | $25.70 to $26.28 | Minus 1% FX if non-US creator |
| Gumroad direct | 10% + $0.50, processing on top | $3.40 + about $1.14 | about $24.46 | Processing assumed 2.9% + $0.30 |
| Gumroad Discover | 30% flat | $8.70 | $20.30 | Only on Discover-sourced sales |
| Agensi | 30% | $8.70 | $20.30 | Platform-stated |
| SkillHQ | 15% | $4.35 | $24.65 | Platform-stated |
| Agent37 | creator keeps 80% | $5.80 | $23.20 | Subscription only |
| Apify PPE | creator keeps 80% minus platform costs | $5.80 + compute | under $23.20 | Per-event, not one-off |

## Cost model

- Near zero ongoing. Marketplace fees on sales. A hosted MCP tier adds a small VPS or
  serverless bill, which the paid tier must cover.
- Eval runs cost model calls. Budget about $0.40 per case per full run based on the cost
  figure in Anthropic's own example output; a 20-case suite at three runs per arm is in the
  low tens of dollars per release. Estimate.
- Your time for the first build and for updates when platforms change.

### Unit economics (estimate)

Assumptions: one Claude Code plugin with a free core and a $29 paid pack sold on Lemon
Squeezy; 40 hours to build, test, and document; 4 hours per month of maintenance and
support; launch in two communities plus the directory; no paid ads.

| Scenario | Paid sales per month | Net per sale | Monthly net | Hours per month | Hourly after month 1 |
|----------|---------------------|--------------|-------------|-----------------|----------------------|
| Low | 5 | $27 | $135 | 4 | $34 |
| Base | 20 | $27 | $540 | 4 | $135 |
| High | 60 | $27 | $1,620 | 6 | $270 |

Payback on the 40-hour build at an opportunity cost of $75 per hour ($3,000): 22 months in
the low case, 6 months in the base case, 2 months in the high case. The base case is in
line with the self-reported n8n and Notion figures above; the high case matches the single
reported $10,000-in-seven-months skill pack. Three artifacts in a bundle at $59 with the
same conversion roughly doubles the base case. None of this holds without the launch
work in the next section.

## Minimum viable version

1. Pick one artifact from the table above and one target role.
2. Build it to solve one complete workflow end to end. No half features.
3. Write ten eval cases and make them pass with a positive delta against the no-plugin
   baseline. Commit the suite with the free version.
4. Record a two-minute demo and write a README that covers install, use, and the three most
   likely failures. The README doubles as the directory listing.
5. List the free version on one platform (own marketplace repo plus Anthropic directory,
   or Notion Marketplace) and put the paid version on Lemon Squeezy with a license key or
   private repo access.
6. Post it in one community where the target role gathers. Once. Lead with the demo and the
   eval numbers, not the price.
7. Iterate on the feedback for a month before starting the second artifact.

### Go-to-market

Channels that the launch research supports, in order:

| Channel | Norm | Notes |
|---------|------|-------|
| Platform directory (Anthropic, MCP registry, Glama, Notion) | Complete listing, screenshots, three example prompts | This is where buyers search. Claim your Glama and PulseMCP listings |
| Subreddit for the target tool (r/ClaudeAI, r/n8n, r/Notion) | Build-in-public post or lesson learned, not a bare link; r/ClaudeAI reportedly uses a Showcase tag | Check sidebar rules first; they were not retrievable in this research |
| Tool community forum (n8n community, Make community) | Share the free template, answer questions | Required anyway for n8n Creator Hub standing |
| DevHunt, Product Hunt | Weekly developer-tool launches; 24-hour vote window on PH | Pair with other channels |
| Show HN | Working demo, plain language, no marketing copy | Save for last; one clean shot |
| YouTube or Medium walkthrough | Long-form demo | The one n8n creator with recurring revenue credits this |

Docs and demo norms: install in three commands, a two-minute video, a "what it does not
do" section, the eval table, and a support email and privacy note (the directory review
asks for both).

## Risks

- **Platform changes.** The MCP registry is in preview and warns of possible data resets.
  n8n's creator program is explicitly unfinished. OpenAI has changed its builder surface
  once already. Keep the artifact portable (Agent Skills standard, stdio MCP) and own the
  customer email list through your checkout.
- **Policy rejection.** The Anthropic directory bans money-moving, media-generating, and
  ad-serving software and requires a public repo. Notion rejects thin AI-generated
  templates. Gumroad may restrict AI-tool access products. Read the policy before building.
- **Copying.** Templates are easy to clone and licenses do not stop it. Compete on evals,
  docs, and updates.
- **Support creep.** Set expectations in the listing. Charge for custom work.

## Decisions still open

These need the owner's input. Everything else above has a researched default.

1. **Which workflow and which role.** The research cannot pick this. It must be something
   you have already built for yourself.
2. **Plugin-plus-paid-pack or Notion system first.** Both score well. Plugin suits a
   developer audience and keeps the customer list; Notion suits a non-developer audience
   and handles checkout and tax for you.
3. **Public repo or not.** A directory listing requires a public repo for the free core.
   Decide whether the paid pack is a private repo (sold via license key) or a bigger
   bundle on the same checkout.
4. **Checkout provider.** Lemon Squeezy is cheaper and issues license keys; Gumroad has
   Discover traffic at a 30% cost. Pick one and do not split the customer list.
5. **License for the free core.** Apache-2.0 for maximum adoption, or FSL to block
   resellers. This is a values call as much as a business one.

## Sources

Claude Code plugins, skills, directory
- https://code.claude.com/docs/en/plugins/create-marketplace (marketplace.json, commands, private repos)
- https://code.claude.com/docs/en/plugins/publish (distribution routes, versioning, directory submission, name rules)
- https://code.claude.com/docs/en/plugins-reference (plugin.json fields, layout, userConfig, reserved names)
- https://code.claude.com/docs/en/skills (SKILL.md frontmatter, 500-line guidance, portable field subset)
- https://code.claude.com/docs/en/plugin-evals (eval layout, graders, baseline, cost example)
- https://claude.com/docs/directory/publish (who can submit, review, Community vs Verified, MCPB deprecation)
- https://claude.com/docs/plugins/submit (public repo requirement, tracked branch, 10 per 24h limit)
- https://support.claude.com/en/articles/13145358-anthropic-software-directory-policy (requirements, prohibited categories)
- https://claude.com/blog/improving-skill-creator-test-measure-and-refine-agent-skills (skill-creator evals)
- https://ryandoser.com/claude-skills-marketplace/ (third-party paid skill marketplaces)
- https://ryandoser.com/make-money-with-claude/ (self-reported $10k skill pack)
- https://www.agent37.com/creators (80% creator share)
- https://www.agensi.io/learn/how-to-monetize-skill-md-skills-developer-guide-2026 (30% fee, $5 to $15 prices)
- https://peerpush.com/p/skillhq (15% fee, 2 to 50 euro prices)

Agent Skills standard
- https://agentskills.io/specification (name 64 chars, description 1024 chars)
- https://github.com/agentskills/agentskills (layout, skills-ref)

MCP
- https://github.com/modelcontextprotocol/registry (preview status, namespace auth, API freeze)
- https://modelcontextprotocol.io/registry/quickstart (mcp-publisher workflow, mcpName)
- https://github.com/modelcontextprotocol/typescript-sdk (v2 packages, registerTool)
- https://github.com/modelcontextprotocol/python-sdk (mcp[cli], mcp dev, transports)
- https://tallyfy.com/how-to-list-mcp-server-registry-smithery-glama-pulsemcp/ (directories, claiming)
- https://www.descope.com/blog/post/mcp-directories (Glama checks, directory counts)
- https://docs.atxp.ai/developers/monetize (pay-per-call)
- https://godberrystudios.com/posts/how-to-monetize-mcp-servers-2026/ ($0.07 per call, zero buyers)
- https://docs.apify.com/actors/publishing/monetize/pay-per-event (80/20 split, rental retirement)
- https://glama.ai/mcp/servers/@oraios/serena/blob/855818da6357ab37fe1d413f5451f1b7027a99e6/docs/01-about/050_acknowledgements.md (sponsors as only income)

n8n, Zapier, Make
- https://docs.n8n.io/workflows/templates/ (creator program in progress)
- https://community.n8n.io/t/where-can-i-sell-my-n8n-workflow-i-am-looking-for-marketplaces-not-the-creator-hub/212963 (three free workflows report)
- https://learnwithhasan.com/digital-product-ideas/n8n-workflow-templates/ ($19 to $79 pricing, pack structure, video)
- https://peerlist.io/aristides/articles/july-2025-gumroad-revenue ($174 month)
- https://usamaakrm.gumroad.com/l/n8n-templates and https://automatewithbishal.gumroad.com/l/25High-Impactn8nAutomationPowerPack (listing sales counts)
- https://docs.zapier.com/platform/publish/zap-templates (partner integration requirement)
- https://help.zapier.com/hc/en-us/articles/29102395009037 (agent template links)
- https://help.make.com/scenario-templates (request approval for public templates)
- https://developers.make.com/custom-apps-documentation/community-apps/how-does-it-work (no templates for community apps)
- https://help.make.com/affiliate-program (35% for 12 months, $100 and three users)

Notion
- https://www.notion.com/help/selling-on-marketplace (10% + $0.40, hold, payouts, FX, refunds)
- https://www.notion.com/en-gb/help/selling-on-marketplace (8% + $0.40)
- https://www.notion.com/help/template-gallery-guidelines-and-terms (quality and originality)
- https://miamoore.net/help/notion-academy/lesson/listing-a-template (rejection reasons, two-week review)
- https://www.microns.io/startup-listings/platform-selling-templates-for-notion ($28,371 ARR listing)
- https://www.microns.io/startup-listings/platform-selling-notion-templates-and-systems ($1,200 listing)
- https://themindfulplanner.substack.com/p/how-i-made-250-selling-notion-templates ($250 creator)
- https://kajabi.com/blog/can-you-make-money-selling-notion-templates (Easlo, Lafferty claims)
- https://fungies.io/how-to-sell-notion-templates-online-3/ (price bands)

Checkout and sponsorship
- https://gumroad.com/pricing (10% + 50¢ direct, 30% Discover)
- https://help.gumroad.com/article/79-gumroad-discover (Discover fee only on Discover-sourced sales)
- https://checkoutpage.com/blog/gumroad-fees (processing on top, third party)
- https://fungies.io/alternatives/gumroad (claim that Gumroad bars AI-tool access products; competitor source)
- https://docs.lemonsqueezy.com/help/getting-started/fees (5% + 50¢, 1.5% international, 1.5% PayPal)
- https://www.lemonsqueezy.com/pricing (merchant of record, license keys)
- https://docs.github.com/en/sponsors/receiving-sponsorships-through-github-sponsors/about-github-sponsors-for-open-source-contributors (0% personal, up to 6% organisation)

OpenAI
- https://venturebeat.com/ai/openai-launches-gpt-store-but-revenue-sharing-is-still-to-come (2024 launch, revenue programme promised)
- https://venturebeat.com/technology/openai-now-accepting-chatgpt-app-submissions-from-third-party-devs-launches (app directory, physical goods only)
- https://community.openai.com/t/chatgpt-app-monetization-apps-sdk/1372343.md (no documented monetization pattern, January 2026)

Licensing
- https://blog.sentry.io/introducing-the-functional-source-license-freedom-without-free-riding (FSL two-year conversion)
- https://mariadb.com/bsl-faq-mariadb/ (BSL Additional Use Grant)
- https://spdx.org/licenses/PolyForm-Small-Business-1.0.0.html (PolyForm Small Business text)

Go-to-market
- https://dev.to/lightningdev123/beyond-product-hunt-a-technical-launch-guide-for-2026-i2j (Show HN norms, sequencing)
- https://daily.dev/blog/best-developer-discovery-platforms-2026/ (DevHunt, directories as stores)
- https://www.claudelog.com/faqs/what-is-claude-ai-reddit/ (r/ClaudeAI Showcase tag, third party)
