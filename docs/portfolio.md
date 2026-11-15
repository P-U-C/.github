# P-U-C portfolio map

Every public repository in the organization has exactly one lifecycle state. States here were proposed in the front-door pull request; merging that pull request is the decision. Facts were checked against live GitHub, DNS, and public URLs on **2026-11-15 (UTC)**. Workflow run status was not checked and is not claimed.

Repositories not listed here or in the [archive index](archive.md) are under review.

## States

| State | Meaning |
| --- | --- |
| **Core** | The organization's own front door, and infrastructure other work depends on. |
| **Product** | A named user, a public URL or install path, and current proof that it works. |
| **Incubating** | In active development, but not yet proven with users or still behind a gate. |
| **Paused** | No meaningful change in 60+ days. Kept unarchived because a live surface or a plausible restart exists. Each one gets a keep-or-retire decision by **2026-12-15**. |
| **Archived** | Finished or retired. Read-only, listed in the [archive index](archive.md). |
| **Fork retention** | A fork kept on purpose, with the reason written down. |

## Active

| Repository | State | What it is | Public URL | Proof, 2026-11-15 UTC |
| --- | --- | --- | --- | --- |
| [.github](https://github.com/P-U-C/.github) | Core | Org profile, this map, archive index | [github.com/P-U-C](https://github.com/P-U-C) | Profile status block updated 2026-11-14 |
| [permanentupperclass.com](https://github.com/P-U-C/permanentupperclass.com) | Core | Brand site source, GitHub Pages | [permanentupperclass.com](https://permanentupperclass.com) | **Down: HTTP 526.** See [incident](#incident-permanentupperclasscom-returns-526) |
| [pft-validator](https://github.com/P-U-C/pft-validator) | Core | Post Fiat validator front desk: domain attestation, lens, herald | [pft.permanentupperclass.com](https://pft.permanentupperclass.com) | Site serving; feed commits at 04:29 and 05:29 UTC |
| [pf-scout-bot](https://github.com/P-U-C/pf-scout-bot) | Core | Scout bot, and the hourly pipeline that publishes pft-validator feeds | — | Pipeline output landing hourly; code last changed 2026-08-25 |
| [aftermath-maker](https://github.com/P-U-C/aftermath-maker) | Product | Maker: self-hosted market making on Aftermath perps (Sui) | [maker.permanentupperclass.com](https://maker.permanentupperclass.com) | Hosted dashboard serving, engine shown as stopped; 2026-10-27 audit remediation ledger in repo |
| [Capable](https://github.com/P-U-C/Capable) | Product | capable: swipeable lessons on building a community that lasts | [p-u-c.github.io/Capable](https://p-u-c.github.io/Capable/) | App serving 5 lessons and 4 traits; last commit 2026-11-14 |
| [farcaster-disciples](https://github.com/P-U-C/farcaster-disciples) | Product | The Disciples: onchain ledger of Farcaster OG pledge signers | [disciples.permanentupperclass.com](https://disciples.permanentupperclass.com) | Site serving; ledger refresh commit 2026-11-14 |
| [farcaster-in-three](https://github.com/P-U-C/farcaster-in-three) | Product | In Three: self-hosted Snapchain node and client in three commands | [farcaster.permanentupperclass.com](https://farcaster.permanentupperclass.com/) | Site serving; npm `farcaster-in-three@0.1.25` published 2026-10-23 |
| [awesome-technocore](https://github.com/P-U-C/awesome-technocore) | Product | Daily index of Technocore agent work for FLOP participation | repo | Index generated 2026-11-14T23:56Z |
| [trend-corpus](https://github.com/P-U-C/trend-corpus) | Incubating | Sector decision-corpus template and live corpora | repo | Daily aggregate commits, latest 2026-11-14 |
| [puc-trading](https://github.com/P-U-C/puc-trading) | Incubating | Convergence options scanner and paper journal | repo | Scanner refresh 2026-11-14; paper only until the 30-trade / 30-day gate |

### Core and Product contracts

Owner for every entry is [@0xzoz](https://github.com/0xzoz). Automation that commits on its own is named under *Depends on*.

**.github**, Core
- Audience: anyone landing on github.com/P-U-C.
- Proof: profile renders; status block is written by the status job.
- Depends on: the status job that rewrites the `STATUS` block.
- Next milestone: this map and the archive index merged and linked from the profile.
- Stop condition: if the status job can't stay accurate, remove the status line rather than show a stale state.

**permanentupperclass.com**, Core
- Audience: people who hear the name and type the domain.
- Proof: none today. The site is down (526).
- Depends on: Cloudflare DNS for the zone, GitHub Pages.
- Next milestone: apex and `www` return 200 over HTTPS, then the page is cut down to a single front door that matches this profile.
- Stop condition: if the site can't be kept current, it becomes a redirect to github.com/P-U-C.

**pft-validator**, Core
- Audience: Post Fiat network participants and anyone verifying the validator's domain.
- Proof: pft.permanentupperclass.com serving; hourly feed commits.
- Depends on: the pf-scout-bot hourly pipeline, GitHub Pages, Cloudflare DNS.
- Next milestone: README matches reality (DNS record type, public status of pf-scout-bot).
- Stop condition: if the validator is retired, archive with a final snapshot.

**pf-scout-bot**, Core
- Audience: operators of the Post Fiat validator surfaces; Task Node users who message the bot.
- Proof: its pipeline's output in pft-validator, hourly.
- Depends on: the Post Fiat chain index and Task Node.
- Next milestone: confirm the conversational bot is still answering, or split it from the pipeline and pause the bot.
- Stop condition: stops with pft-validator.

**aftermath-maker** (Maker), Product
- Audience: Aftermath perpetuals traders who want bounded, self-hosted market making with local signing.
- Proof: hosted dashboard serving; public audit remediation ledger.
- Depends on: Aftermath on Sui, Sui RPC, the hosting box, Cloudflare.
- Next milestone: independent retest of the 2026-10-27 audit findings, then a live-test-ready Aftermath MVP.
- Stop condition: any unresolved critical finding on retest keeps live trading off.

**Capable** (capable), Product
- Audience: people who want to start a community that lasts, or be a good member of one.
- Proof: app serving; content refresh scheduled four times an hour.
- Depends on: GitHub Pages, crowdsourced lesson content, Base for trait stamps.
- Next milestone: one round of user testing, then a launch post.
- Stop condition: if new lessons can't be added without manual work, freeze at the current set.

**farcaster-disciples** (The Disciples), Product
- Audience: the Farcaster and Network School community.
- Proof: site serving; daily ledger refresh.
- Depends on: GitHub Pages, onchain data for the Farcaster OG collection.
- Next milestone: none required; keep the refresh green.
- Stop condition: when the pledge cohort closes, freeze the ledger with a final snapshot and archive.

**farcaster-in-three** (In Three), Product
- Audience: developers who want their own Farcaster node and client without a hosted API.
- Proof: site serving; npm package published.
- Depends on: upstream Snapchain releases, Docker.
- Next milestone: re-run the three commands against the current Snapchain release and update `docs/PROOF.md`.
- Stop condition: if an upstream change breaks install and stays broken for two weeks, mark Paused with a banner.

**awesome-technocore**, Product
- Audience: Technocore and FLOP participants.
- Proof: index regenerated daily.
- Depends on: Technocore rooms, the update workflow.
- Next milestone: none required.
- Stop condition: archive when FLOP participation ends.

## Paused

Decide keep-or-retire by 2026-12-15. A paused project with a live surface either gets a "paused" note on that surface or the surface comes down.

| Repository | What it is | Last change | Live surface |
| --- | --- | --- | --- |
| [b1e55ed](https://github.com/P-U-C/b1e55ed) | Trading intelligence engine, event-sourced | 2026-05-19 | [docs](https://docs.b1e55ed.permanentupperclass.com) and [site](https://b1e55ed.permanentupperclass.com) up |
| [b1e55ed-site](https://github.com/P-U-C/b1e55ed-site) | Landing site for b1e55ed | 2026-03-19 | b1e55ed.permanentupperclass.com |
| [b1e55ed-contracts](https://github.com/P-U-C/b1e55ed-contracts) | ERC-8004 reputation and validation registries | 2026-03-19 | Deployed on Base |
| [offchain-attestations](https://github.com/P-U-C/offchain-attestations) | EAS attestation registry for b1e55ed contributors | 2026-02-24 | Issues are the registry |
| [safetymd](https://github.com/P-U-C/safetymd) | safety.md: trust standard and API for agent payments | 2026-03-23 | API health endpoint returns ok; [docs](https://p-u-c.github.io/safetymd) up |
| [talent-engine](https://github.com/P-U-C/talent-engine) | Scores builders from public code activity | 2026-09-23 | Used by an external sponsorship programme |
| [city2](https://github.com/P-U-C/city2) | City control plane, replacing the OpenClaw-era workspace | 2026-08-06 | — |
| [swell-checker](https://github.com/P-U-C/swell-checker) | Trend-emergence detector, weekly digest | 2026-08-05 | — |
| [wellness-radar](https://github.com/P-U-C/wellness-radar) | Metro Vancouver wellness market-intelligence console | 2026-06-27 | — |
| [pf-monitor](https://github.com/P-U-C/pf-monitor) | Prometheus, Grafana and Alertmanager stack for Post Fiat validators | 2026-03-03 | — (promote to Core if the validator runs it) |

## Fork retention

| Fork | Reason kept |
| --- | --- |
| [pympp-1](https://github.com/P-U-C/pympp-1) | Carries P-U-C commits (Redis store, testnet utilities, 2026-08-17) not in upstream. |
| [eliza](https://github.com/P-U-C/eliza) | Carries the safety.md plugin commit (2026-08-17). Follows the safetymd decision. |

## Default-branch exceptions

The default is `main`. Declared exceptions:

| Repository | Branch | Note |
| --- | --- | --- |
| b1e55ed | `develop` | Git-flow; paused. |
| eliza | `develop` | Upstream's default; fork retention. |
| duplicate-task-suppression, outstanding-queue-reconciliation, reward-artifact-coverage-audit, langchain | `master` | Archived; not worth changing. |

## Incident: permanentupperclass.com returns 526

Checked 2026-11-15 UTC.

- The apex and `www` resolve to Cloudflare proxy addresses and fail to load. The apex was reported as Cloudflare 526 (origin certificate rejected).
- GitHub Pages is serving the repository with the custom domain set, but its redirect from `p-u-c.github.io/permanentupperclass.com/` goes to `http://permanentupperclass.com/`, plain HTTP. Healthy sites in this org redirect to `https://`. That means Pages has no valid certificate for the apex, so Cloudflare's strict origin check fails.
- `disciples.` is a plain DNS record to `p-u-c.github.io` and is healthy. `pft.`, `b1e55ed.` and `farcaster.` are Pages sites proxied like the apex. They work today, but they have the same exposure when their certificates next renew.

Fix, done by the domain owner, no code change:

1. Set the apex and `www` records to DNS only, pointed at GitHub Pages (`A` records to `185.199.108.153`, `.109`, `.110`, `.111`; `www` as `CNAME p-u-c.github.io`).
2. In the repository's Pages settings, re-save the custom domain so a certificate is issued, then turn on Enforce HTTPS.
3. Verify: the `github.io` redirect goes to `https://`, and the apex returns 200.
4. Move `pft.`, `b1e55ed.` and `farcaster.` to DNS only as well, so this doesn't repeat at renewal.

Not recommended: dropping the zone to non-strict TLS. It hides the error by no longer checking the origin, for every host in the zone.
