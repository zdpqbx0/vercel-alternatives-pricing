# vercel alternatives: how Netlify, Cloudflare, Render and Railway compare on price, and when a $10 VPS makes more sense

Most people searching for Vercel alternatives aren't unhappy with the deployment experience. Git push, preview URLs, a site live globally in under a minute — that part works fine. The frustration sits in three specific places: the Hobby plan only covers personal, non-commercial projects; Pro starts at $20 per user per month and then meters CPU time, image transformations and ISR reads separately; and there's no real backend, so databases, queues and background workers all become extra subscriptions on other platforms.

The alternatives fall into three camps, and it helps to know which one you're shopping for:

1. **Frontend clouds** (Netlify, Cloudflare Pages/Workers) — closest to the Vercel workflow, different pricing meters.
2. **Managed full-stack PaaS** (Render, Railway, Fly.io) — containers, databases and workers in one place, still someone else's infrastructure.
3. **Self-hosting an open-source deploy tool** (Coolify, Dokploy) on a VPS — flat cost, root access, your whole stack in one place.

Most comparison posts covering this keyword handle the first two camps well, then gesture at the third with "bring your own VPS" — without ever telling you what the VPS costs, which size you actually need, or how the math works out over a year. That gap is what this article fills, using Vultr as the worked example.

> **Quick picks**
> - Want Vercel's workflow with a different bill? Netlify's credit plans and Cloudflare's $5/mo Workers plan are the closest matches.
> - Want managed full-stack without touching a server? Render from $7/mo per service, Railway from $5/mo plus usage.
> - Want a flat bill, Docker, and your database in the same place? Run Coolify on a Vultr VPS — realistic setups land between $10 and $20/month. 👉 [check today's Vultr cloud compute pricing](https://www.vultr.com/pricing/?ref=7268283)

## Why teams actually leave Vercel

The Hobby tier is free but restricted to personal, non-commercial use — the moment a side project makes money or belongs to a company, you're on Pro. Pro starts at $20 per user per month, and the usage meters stack on top of that: Fluid compute CPU at $0.128 per hour, image transformations at $0.05 per 1,000, ISR reads at $0.40 per 1 million. Each meter runs on its own, so costs grow with traffic and are genuinely hard to predict in advance.

The backend gap matters just as much. Vercel runs serverless functions with limits on execution time, payload size and cold starts. The moment your app needs a real database, a queue or a 10-minute background job, you're assembling a second stack — a hosted Postgres here, a Redis provider there, a cron service on top — and each piece arrives with its own invoice.

There's also a group that shouldn't leave. If you host a Next.js content or marketing site that leans hard on the global edge network, and your bill has been stable, Vercel does that job well. Switching platforms to trim a modest bill while taking on server maintenance is rarely worth it.

## The main alternatives at a glance

Here's the field, with Vercel as the baseline row.

| Platform | Pricing model | Free tier | Backend included | Best for |
| --- | --- | --- | --- | --- |
| Vercel | Pro $20/user/mo + separate usage meters | Hobby is free, non-commercial only | No — external SaaS only | Next.js sites that lean on the global edge |
| Netlify | Credit-based: free 300 credits, Personal $9/mo (1,000), Pro $20/mo (3,000); a production deploy costs 15 credits, bandwidth 20 credits/GB | Yes | No — external SaaS only | Jamstack and marketing sites wanting Vercel-like DX |
| Cloudflare Workers/Pages | $5/mo with 10M requests and 30M CPU-ms included, no bandwidth charges | Yes — 100K req/day free | Yes — D1, KV, Durable Objects, Queues, R2 | Cost-sensitive teams OK with a non-Node runtime |
| Render | Per-service from $7/mo; managed Postgres from $6/mo, Redis from $10/mo | Yes — free services sleep after 15 min | Yes — Postgres, Redis, workers, cron | Heroku-style managed full-stack |
| Railway | Usage-based (per vCPU/GB-second); Hobby $5/mo, Pro $20/mo + usage | One-time $5 trial credit | Yes — database templates | Fast multi-service prototypes |
| Fly.io | Usage-based VMs placed near your users; support plans from $29/mo | — | Partial — volumes and integrations | Global low-latency container apps |
| Coolify / Dokploy (self-hosted) | Software free and open source; Coolify Cloud from $5/mo + $3 per connected server | Self-hosted is free | Anything Docker runs | Full control at the lowest flat cost |

Notice the last row. Nearly every article that recommends self-hosting quotes the software price and then goes quiet about the server, which is the number that decides whether the approach is actually cheap. Next section fixes that.

## The self-hosting route most lists skip — and what it runs on

The cheapest genuinely full-stack Vercel alternative is an open-source deploy platform on a VPS you rent. Coolify and Dokploy both give you Git-based deploys, preview environments and one-click databases on hardware with a flat monthly price. Vultr is one of the infrastructure providers this works well on, and it's worth being clear about what you're renting:

- **Shared-CPU cloud compute from $2.50/mo (512 MB) up through $80/mo (16 GB)**, billed hourly — destroy and redeploy whenever you like.
- **Roughly 30 regions** across North America, Europe, Asia, South America and Oceania, so you can put the server near your users even without an edge network.
- **A Marketplace with one-click images.** Coolify is available there; Dokploy installs on any fresh server with a single script; plain Docker is there too if you'd rather bring nothing opinionated.
- **Managed PostgreSQL from $15/mo** if you'd rather not run the database yourself — MySQL, Kafka and a Redis-compatible cache are also managed options — plus S3-compatible object storage at $6/mo for 1 TB.
- **Managed Kubernetes with no control-plane fee**, if a project outgrows a single box.

New accounts get $250 in credits valid for 30 days, which is enough to run a realistic setup for a month and find out whether self-hosting suits you before any real money is spent. 👉 [open a Vultr account and start with the $250 credit](https://bit.ly/VulTR)

## Vultr's cloud compute plans and current pricing

For replacing a Vercel workload, the shared-CPU "Regular Performance" line is the relevant one. Entry sits at $2.50/mo, a comfortable floor for a real app with its own database is $10/mo, and $20/mo gives you room for the app, the database and a background worker together.

| Plan (RAM) | vCPU | Storage | Included transfer | Price/mo | Deploy |
| --- | --- | --- | --- | --- | --- |
| 512 MB | 1 | 10 GB SSD | 0.5 TB | $2.50 | [ Get started](https://www.vultr.com/pricing/?ref=7268283) |
| 1 GB | 1 | 25 GB SSD | 1 TB | $5 | [ Get started](https://www.vultr.com/pricing/?ref=7268283) |
| 2 GB | 1 | 55 GB SSD | 2 TB | $10 | [ Get started](https://www.vultr.com/pricing/?ref=7268283) |
| 4 GB | 2 | 80 GB SSD | 3 TB | $20 | [ Get started](https://www.vultr.com/pricing/?ref=7268283) |
| 8 GB | 2 | 160 GB SSD | 4 TB | $40 | [ Get started](https://www.vultr.com/pricing/?ref=7268283) |
| 16 GB | 4 | 320 GB SSD | 5 TB | $80 | [ Get started](https://www.vultr.com/pricing/?ref=7268283) |

A few details the price list won't jump out at you:

- The $2.50 512 MB plan is IPv6-only; with an IPv4 address it's $3.50/mo.
- NVMe-backed High Performance and High Frequency lines start at $6/mo for 1 GB RAM if disk I/O matters to your app.
- Every plan bills hourly, so a test server that lives for two days costs cents. You pay only for the hours it runs.
- These are all shared-vCPU plans; dedicated vCPU, bare metal and GPU lines exist at higher price points.

## What a Vercel exit actually costs per year

For most setups the answer is a flat $10–$25/month. Here are three worked scenarios, with assumptions stated so you can adjust them.

**Solo developer, one app.** A $10/mo Vultr box (1 vCPU, 2 GB) runs Coolify, the Next.js app and a Postgres container: about **$120/year, flat**. The Vercel equivalent is a single Pro seat at $240/year before a single usage meter ticks. The $10 size is the realistic floor — 1 GB works for a demo, but app + database + build processes get tight.

**Small team, app + database + worker.** One $20/mo box (2 vCPU, 4 GB) handles all three comfortably: **$240/year**. Split it instead — $10/mo for the app plus $15/mo for managed Postgres — and you're at $25/month, or $300/year. Three developers on Vercel Pro cost $720/year, before any usage.

**Media-heavy app.** Vercel bills image transformations at $0.05 per 1,000. On your own server, image processing runs on CPU you've already paid for; the $20 box absorbs it.

One honest caveat: if you're sitting on Vercel's free Hobby tier and staying there, switching saves nothing. The move pays off once you're on Pro, hitting usage meters, or paying for separate backend services.

## What you give up when you self-host

You become the ops team, and that's the entire trade. Worth spelling out before you commit:

- **One region per server.** A dashboard, SaaS app or API won't notice the difference. A content site competing on global load times will — a CDN in front helps, but if edge performance is the product, Cloudflare's network fits better than any single-region VPS.
- **Updates, patches, disk space and backups are your job.** Coolify and Dokploy automate deploys and previews; neither of them watches the server at 3 a.m. when the disk fills up.
- **You'll open a terminal occasionally.** Anyone allergic to SSH will be happier on a managed platform.

Who shouldn't bother: hobby projects on the free tier, purely static sites (a free static host does the job with zero maintenance), and teams that want zero infrastructure decisions — Render or Railway remove more ops work than any VPS ever will.

## Migrating a Next.js app from Vercel in six steps

For most Next.js apps this is an afternoon of work, and the order matters more than the tools.

1. Create the Vultr account and decide the region first — pick wherever most of your users are, because a single-region server rewards proximity.
2. Deploy Coolify from the Vultr Marketplace (or install Dokploy with its script, or plain Docker if you want nothing opinionated).
3. Connect your Git repository. The deploy tool detects Next.js and runs a standard Node build — your app becomes a long-running process, so no 120-second function ceiling and no cold starts.
4. Add a database: a Postgres container on the same box for small apps, or Vultr's managed Postgres from $15/mo when you'd rather not own backup and upgrade chores.
5. Copy environment variables over from Vercel, migrate data with a `pg_dump` and restore, then test everything through a preview deployment.
6. Lower your DNS TTL a day ahead of the switch, then point the domain. Keep the Vercel project paused rather than deleted for a week — rollback is one DNS change.

👉 [compare server sizes and current prices before you deploy](https://www.vultr.com/pricing/?ref=7268283)

## FAQ

**Is Vultr a Vercel alternative?**
It's the infrastructure half of one. Paired with Coolify or Dokploy, it replaces Vercel's hosting, functions and deployment workflow; the frontend framework stays yours. If you want a frontend cloud with zero setup, a managed PaaS fits better — if you want Docker, root access and a flat bill, this combination is the one.

**Does Vultr have a free tier?**
No permanent free tier. New accounts get $250 in credits valid for 30 days, and every instance bills hourly, so short-lived test servers cost almost nothing.

**What's the cheapest Vercel alternative overall?**
For a purely static site, free static hosting wins outright. For anything full-stack, a $5/mo Vultr instance running Coolify is the cheapest serious option — plan on $10/mo once a database joins the setup.

**Can I run Kubernetes on Vultr?**
Yes. Vultr's managed Kubernetes has no control-plane fee; you pay only for worker nodes at the same compute prices listed above.

**How much bandwidth do Vultr plans include?**
Transfer scales with the plan — 0.5 TB/mo on the $2.50 instance up to 5 TB/mo at $80, included in the price.

## The short version

- Pure static or marketing site → free static hosting; pay for nothing.
- Want Vercel-like DX with more predictable costs → Cloudflare's $5/mo plan or Netlify's credit tiers.
- Want managed full-stack with zero ops → Render or Railway.
- Want the lowest flat bill with app, database, workers and queues in one place, and don't mind owning a server → Coolify or Dokploy on Vultr. Start at $10/mo, move to $20 when the box gets crowded, add managed Postgres when backups become your problem instead of a line item.

Before you deploy: enable automatic backups (they add 20% to the instance price — cheap insurance), take a snapshot before major upgrades, and leave the old Vercel project in place until DNS has settled everywhere.

Ready to try it with zero upfront cost? 👉 [start on Vultr with $250 in credits](https://bit.ly/VulTR)
