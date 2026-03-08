# Cloud Infrastructure & DevOps for Israeli Startups — March 2026

Research date: 2026-03-07

---

## 1. AWS il-central-1 (Israel / Tel Aviv)

### Status: Generally Available (launched August 2023)
- **3 Availability Zones** (il-central-1a, il-central-1b, il-central-1c)
- AWS committed $7.2B investment in Israel by 2037

### Services Available
Core services available in il-central-1 include:
- **Compute**: EC2 (including M7i added Feb 2026), EC2 Auto Scaling, Lambda, Fargate, EKS, ECS, AWS Batch
- **Storage**: S3, EBS
- **Database**: RDS, Aurora, DynamoDB, ElastiCache, Amazon Redshift, OpenSearch Service
- **Networking**: ELB, API Gateway, Direct Connect, PrivateLink, Cloud Map
- **DevOps/Infra**: CloudFormation, CloudTrail, CloudWatch (Logs + Events), Config, EventBridge, IAM, KMS, ACM, AWS Health Dashboard
- **Data/Analytics**: Kinesis Streams, DMS, EMR
- **Marketplace**: Available
- **WorkSpaces Applications**: Added Nov 2025

### Services NOT yet in il-central-1 (notable gaps)
Many newer/specialized services (SageMaker full suite, Bedrock, AppRunner, etc.) may still be limited. Always verify at [AWS Regional Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

### Pricing vs eu-central-1 (Frankfurt)
- **~5-6% premium** over eu-west-1 (Ireland)
- Pricing is comparable to or slightly above Frankfurt (eu-central-1)
- For a bootstrapped startup running ~$50-100/mo in AWS, this premium is negligible (~$3-6/mo extra)
- **Latency benefit**: ~5-15ms from Israel vs ~50-80ms to Frankfurt — worth the small premium for user-facing services

### Sources
- [AWS Israel Region](https://aws.amazon.com/local/israel/)
- [AWS Regions and Availability Zones](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions.html)
- [EC2 M7i in Israel — Feb 2026](https://aws.amazon.com/about-aws/whats-new/2026/02/amazon-ec2-m7i-israel-tel-aviv-regions/)
- [DoiT Price Comparison](https://www.doit.com/blog/aws-region-in-tel-aviv-israel-price-comparison-versus-other-regions/)
- [CloudPrice AWS Regions](https://cloudprice.net/aws/regions)

---

## 2. Google Cloud Israel Region (me-west1)

### Status: Generally Available (launched October 2022)
- **Region**: me-west1 (Tel Aviv)
- **3 Availability Zones**: me-west1-a, me-west1-b, me-west1-c
- Full Compute Engine, GKE, Cloud Run, Cloud Functions, Cloud Storage, BigQuery, Cloud SQL available

### Pricing
- Follows standard GCP Middle East pricing tier
- GCP offers automatic **Sustained-Use Discounts** (no commitment required) — advantageous for variable workloads
- Generally comparable to AWS il-central-1 pricing

### Key Advantage
- **Automatic discounts** without upfront commitments — good for bootstrapped startups with unpredictable usage

### Sources
- [Google Cloud Locations](https://cloud.google.com/about/locations)
- [GCP Israel Region Announcement](https://cloud.google.com/blog/products/infrastructure/new-google-cloud-region-in-israel-is-now-open)
- [GCP Region Pricing Comparison](https://cloudprice.net/gcp/regions)

---

## 3. Azure Israel Region (Israel Central)

### Status: Generally Available (launched 2023)
- **Region**: Israel Central
- **Location**: Modi'in area (between Tel Aviv and Jerusalem)
- **3 Availability Zones**
- Data residency guaranteed in Israel

### Services Available
Full Azure service catalog including VMs, App Service, Azure SQL, Cosmos DB, AKS, Azure Functions, Storage, and more. Check [Azure Products by Region](https://azure.microsoft.com/en-us/explore/global-infrastructure/products-by-region/table) for current availability.

### Sources
- [Azure Israel Central](https://www.datacenters.com/microsoft-azure-israel-central)
- [Azure Regions List](https://learn.microsoft.com/en-us/azure/reliability/regions-list)
- [Azure Global Infrastructure](https://azure.microsoft.com/en-us/explore/global-infrastructure/geographies/)

---

## 4. Best Cloud for Israeli Bootstrapped Startup in 2026

### Recommendation: **AWS il-central-1** (for Emuni's stack)

| Factor | AWS | GCP | Azure |
|--------|-----|-----|-------|
| Israel region | il-central-1 (3 AZs) | me-west1 (3 AZs) | Israel Central (3 AZs) |
| Supabase compatibility | Yes (Supabase runs on AWS) | No (Supabase is AWS-only) | No |
| Startup credits | Up to $100K (via Activate) | Up to $200K (Start/Scale) | Up to $150K (via VCs) |
| Bootstrapped credits | $1K (Activate Founders) | Via application | $1K-$5K (self-serve) |
| Free tier | 12 months generous | Always Free tier + 90-day trial | 12 months + always free |
| Node.js/NestJS support | Lambda, ECS, Fargate, App Runner | Cloud Run, Cloud Functions, GKE | App Service, Azure Functions, AKS |
| Community/docs | Largest ecosystem | Strong, growing | Large, enterprise-focused |
| Auto-discounts | No (must buy RIs/Savings Plans) | Yes (Sustained-Use Discounts) | No (must buy RIs) |

### Why AWS wins for Emuni specifically:
1. **Supabase runs on AWS** — deploying your own infra on AWS means same-network latency to your Supabase DB
2. **il-central-1 has the services you need** — RDS/Aurora, Lambda, S3, ECS all available
3. **Largest ecosystem** — most tutorials, StackOverflow answers, community support
4. **Activate Founders** — $1K free credits for bootstrapped founders (no VC needed)

### If you weren't using Supabase:
GCP me-west1 would be a strong contender due to automatic sustained-use discounts and potentially lower costs for variable workloads.

### Sources
- [AWS Activate](https://aws.amazon.com/activate/)
- [Google for Startups Cloud Program](https://cloud.google.com/startup)
- [Microsoft for Startups](https://www.microsoft.com/en-us/startups)
- [Cloud Pricing Comparison 2026](https://www.effectivesoft.com/blog/cloud-pricing-comparison.html)
- [AWS vs Azure vs GCP 2026](https://northflank.com/blog/aws-vs-azure-vs-google-cloud)

---

## 5. Vercel / Netlify

### Relevance for React Native + NestJS: **LOW**

Vercel and Netlify are optimized for **web frontends** (Next.js, static sites, Jamstack). They are NOT ideal for:
- React Native apps (mobile apps distributed via app stores, not web hosting)
- NestJS backends (long-running Node.js servers, not serverless functions)

### If you had a web dashboard/landing page:
| Feature | Vercel | Netlify |
|---------|--------|---------|
| Free tier | Hobby (free) — 100GB bandwidth, 100 hrs serverless | Free — 100GB bandwidth, 300 build min |
| Edge nodes | 100+ global locations | 100+ global locations |
| Israel edge | Not explicitly listed (CDN likely covers via nearby PoPs) | Not explicitly listed |
| TTFB | ~70ms | ~90ms |
| Best for | Next.js | Static/Jamstack |

### Verdict for Emuni
Not relevant for your core stack. Use only if you build a marketing website or web admin panel with Next.js.

### Sources
- [Vercel vs Netlify 2026](https://www.clarifai.com/blog/vercel-vs-netlify)
- [Edge Performance Comparison 2026](https://dev.to/dataformathub/cloudflare-vs-vercel-vs-netlify-the-truth-about-edge-performance-2026-50h0)
- [Deploying Full Stack Apps 2026](https://www.nucamp.co/blog/deploying-full-stack-apps-in-2026-vercel-netlify-railway-and-cloud-options)

---

## 6. Railway / Render / Fly.io

### For hosting NestJS backends:

| Feature | Railway | Render | Fly.io |
|---------|---------|--------|--------|
| **Free tier** | 30-day trial ($5 credit) | Free (750 hrs, 1GB Postgres) | $5/mo included on Hobby |
| **Hobby plan** | $5/mo (includes $5 usage) | $7/mo (Starter) | Pay-as-you-go after $5 |
| **Pro plan** | $20/mo | $25/mo (Standard) | Usage-based |
| **Regions** | US, EU | US (Oregon, Virginia, Ohio), EU (Frankfurt), Asia (Singapore) | 35+ global regions |
| **Israel region** | No | No | No dedicated Israel region |
| **Closest to Israel** | EU | Frankfurt (eu-central) | Amsterdam (ams) or similar EU |
| **Deploy from GitHub** | Yes, auto-detect | Yes, auto-detect | Yes, via flyctl CLI |
| **Postgres included** | Add-on | Free 1GB on free tier | Fly Postgres (managed) |
| **Best for** | Prototyping, simple deploys | Production-ready, generous free | Edge deployment, multi-region |

### Verdict for Emuni
- **For MVP/prototyping**: Railway ($5/mo) or Render (free tier) — fastest path to deployment
- **For production**: AWS il-central-1 (ECS/Fargate or Lambda) — latency matters for Israeli users
- **Fly.io advantage**: If you need multi-region later (Israel + Europe), Fly.io's 35+ regions are unmatched among PaaS providers

### Important Note
None of these have an Israel region. If sub-50ms latency to Israeli users is critical, you need AWS il-central-1, GCP me-west1, or Azure Israel Central directly.

### Sources
- [Railway Pricing](https://railway.com/pricing)
- [Render Pricing](https://render.com/pricing)
- [Fly.io Regions](https://fly.io/docs/reference/regions/)
- [Railway vs Render 2026](https://northflank.com/blog/railway-vs-render)
- [Fly.io vs Railway 2026](https://thesoftwarescout.com/fly-io-vs-railway-2026-which-developer-platform-should-you-deploy-on/)

---

## 7. GitHub Actions — Free Tier Limits (March 2026)

### Current Limits (unchanged since Jan 2026 pricing update)

| Plan | Minutes/month (private repos) | Storage |
|------|-------------------------------|---------|
| **Free** | 2,000 min | 500 MB |
| **Pro** | 3,000 min | 1 GB |
| **Team** | 3,000 min | 2 GB |
| **Enterprise** | 50,000 min | 50 GB |

### Minute Multipliers (OS)
- Linux: 1x
- Windows: 2x
- macOS: 10x

### January 2026 Changes
- **Up to 39% price reduction** on GitHub-hosted runners
- Free minute quotas **unchanged**

### March 2026 Change
- **Self-hosted runners now consume free minutes** based on list price (previously unlimited)
- This is a significant change if you use self-hosted runners

### Public Repos
- **Unlimited free minutes** — no changes

### Cache Storage
- 10 GB per repository included; excess billed per GB

### Sources
- [GitHub Actions Billing](https://docs.github.com/en/actions/concepts/billing-and-usage)
- [GitHub Pricing](https://github.com/pricing)
- [2026 Pricing Changes](https://github.com/resources/insights/2026-pricing-changes-for-github-actions)
- [GitHub Actions Pricing Changelog](https://github.blog/changelog/2025-12-16-coming-soon-simpler-pricing-and-a-better-experience-for-github-actions/)

---

## 8. CI/CD Alternatives Comparison (2026)

| Feature | GitHub Actions | GitLab CI | CircleCI | Dagger |
|---------|---------------|-----------|----------|--------|
| **Best for** | GitHub-native repos | Self-contained DevOps | Build speed | Portable pipelines |
| **Config format** | YAML | YAML | YAML | Go/Python/TypeScript code |
| **Free tier** | 2,000 min/mo | 400 min/mo (shared) | 6,000 min/mo (free plan) | Open source (free) |
| **Marketplace** | 20,000+ actions | Smaller | Orbs marketplace | SDK-based |
| **Local testing** | Limited (act) | docker-compose | Limited | Excellent (core feature) |
| **Docker layer caching** | Manual | Built-in | Built-in (50%+ faster) | Via Dagger Cloud |
| **OIDC/Cloud auth** | Native | Via integration | Via integration | Via CI provider |
| **Learning curve** | Low | Medium | Medium | Higher (SDK) |
| **Self-hosted runners** | Yes (now consumes minutes) | Yes (free) | Yes | Runs anywhere |

### Recommendation for Solo Founder
**GitHub Actions** — no question. Reasons:
1. Already using GitHub for source control
2. 2,000 free minutes/month is plenty for a solo project
3. Largest marketplace of pre-built actions
4. Zero setup overhead — integrated into your repo
5. OIDC integration with AWS for secure, credential-free deployments

Dagger is interesting but adds complexity a solo founder doesn't need. CircleCI's free tier (6,000 min) is generous but adds another vendor. GitLab CI only makes sense if you're on GitLab.

### Sources
- [CI/CD Decision Guide 2026](https://technologymatch.com/blog/jenkins-vs-gitlab-ci-vs-circleci-vs-github-actions-the-ci-cd-decision-guide-in-2026)
- [Top 10 CI/CD Tools 2026](https://www.siit.io/blog/best-ci-cd-tools)
- [14 Best CI/CD Tools 2026](https://northflank.com/blog/best-ci-cd-tools)
- [Dagger CI/CD Pipelines as Code](https://www.youngju.dev/blog/devops/2026-03-03-dagger-cicd-pipeline-as-code.en)

---

## 9. Sentry — Error Monitoring (2026)

### Current Plans

| Plan | Price | Errors/mo | Performance Units | Users |
|------|-------|-----------|-------------------|-------|
| **Developer (Free)** | $0 | 5,000 | 10,000 | 1 |
| **Team** | $26-29/mo | 50,000 | 5M spans | Unlimited |
| **Business** | $80-89/mo | 100,000+ | Custom | Unlimited |
| **Enterprise** | Custom | Custom | Custom | Unlimited |

### Key Features
- React Native SDK available (official)
- Source maps upload for readable stack traces
- Performance monitoring (transaction tracing)
- Release tracking and deploy notifications
- 14-day free trial of paid features on signup

### Verdict for Emuni
**Developer (Free) plan is perfect for MVP**:
- 5,000 errors/month is more than enough for a pre-launch / early app
- 1 user is fine for a solo founder
- Upgrade to Team ($26/mo) when you have paying users

### Sources
- [Sentry Pricing](https://sentry.io/pricing/)
- [Sentry Pricing Breakdown](https://signoz.io/guides/sentry-pricing/)
- [Sentry 2026 Plans Compared](https://costbench.com/software/developer-tools/sentry/)

---

## 10. Product Analytics: Mixpanel vs PostHog vs Amplitude vs June.so

### Comparison Table

| Feature | PostHog | Mixpanel | Amplitude | June.so |
|---------|---------|----------|-----------|---------|
| **Free tier** | 1M events/mo | 1M events/mo (was 20M, reduced) | 10K MTUs | No free plan |
| **Paid from** | ~$0.00045/event after free | $0.28/1K events after free | Custom | Custom |
| **Session replay** | Yes (5K free/mo) | Yes (added 2024) | No | No |
| **Feature flags** | Yes (1M requests free) | Yes (added recently) | Yes | No |
| **Error tracking** | Yes (100K free) | No | No | No |
| **Self-host option** | Yes (MIT license) | No | No | No |
| **Best for** | Technical/engineering teams | Product managers | Enterprise analytics | B2B SaaS ($1M+ ARR) |
| **React Native SDK** | Yes | Yes | Yes | Limited |
| **Seats** | Unlimited (all plans) | Limited on free | Limited on free | Limited |
| **Status** | Active, growing fast | Active | Active | **Acquired by Amplitude** |

### Critical Update: June.so
June.so has been **acquired by Amplitude** and is no longer an independent product. Do not build on June.so for a new project.

### Recommendation for Emuni
**PostHog (Free tier)** — clear winner for a solo founder:
1. **1M events/mo free** — sufficient for early growth
2. **All-in-one**: analytics + session replay + feature flags + error tracking + surveys
3. **Unlimited seats** — no cost surprise when adding team members later
4. **Self-host option** — can move to self-hosted if costs grow
5. **98% of customers use it for free** — designed for startups
6. Replaces 3-4 separate tools (analytics + Sentry + LaunchDarkly + Hotjar)

### If you want PostHog for analytics + Sentry for errors:
That's also a valid split. Sentry's error tracking is more mature and has better React Native integration. PostHog's error tracking is newer but rapidly improving.

### Sources
- [PostHog Pricing](https://posthog.com/pricing)
- [Mixpanel Review 2026](https://hackceleration.com/mixpanel-review/)
- [PostHog vs Mixpanel](https://posthog.com/blog/posthog-vs-mixpanel)
- [PostHog vs Amplitude](https://posthog.com/blog/posthog-vs-amplitude)
- [Best Product Analytics 2026](https://cleverx.com/blog/product-analytics-tools-12-best-options-compared)
- [June.so (now Amplitude)](https://www.june.so/)

---

## 11. Recommended Monitoring Stack for Solo Founder

### The "Zero-Cost MVP Stack"

| Layer | Tool | Free Tier | Notes |
|-------|------|-----------|-------|
| **Error Tracking** | Sentry (Developer) | 5,000 errors/mo, 1 user | Best React Native support, source maps |
| **Product Analytics** | PostHog Cloud | 1M events/mo, unlimited users | Also gives session replay (5K/mo) + feature flags (1M/mo) |
| **Uptime Monitoring** | UptimeRobot | 50 monitors, 5-min intervals | Email/Slack/Telegram alerts, free forever |
| **Logging** | AWS CloudWatch Logs | 5 GB ingestion + 5 GB storage (free tier) | Already included with AWS il-central-1 |
| **APM/Tracing** | PostHog (basic) or skip | Included in PostHog | Sentry also has basic performance monitoring |
| **Status Page** | Instatus or Better Stack | Free tier available | Public status page for transparency |

**Total monthly cost: $0**

### The "Growing Startup Stack" (~$50-100/mo)

| Layer | Tool | Cost | Why Upgrade |
|-------|------|------|-------------|
| **Error Tracking** | Sentry Team | $26/mo | Unlimited users, 50K errors, issue owners |
| **Product Analytics** | PostHog Cloud | $0 (still free at <1M events) | Session replay, feature flags, surveys |
| **Uptime Monitoring** | Better Stack | $24/mo | 1-min checks, incident management, on-call |
| **Logging** | Better Stack Logs | Included | Structured logs, 30-day retention |
| **APM/Tracing** | Sentry Performance | Included in Team | Transaction tracing, slow query detection |
| **Status Page** | Better Stack | Included | Branded status page |

### What to SKIP as a solo founder
- **Datadog** — costs $15/host/mo minimum, scales to thousands quickly. Overkill.
- **New Relic** — generous free tier (100GB/mo) but complex setup. Consider if you outgrow the stack above.
- **PagerDuty** — not needed until you have a team. UptimeRobot or Better Stack handles alerts.
- **Grafana Cloud** — free tier (10K metrics) is good but adds operational complexity. Not worth it solo.
- **LaunchDarkly** — PostHog includes feature flags for free.
- **Hotjar** — PostHog includes session replay for free.

### Sources
- [UptimeRobot Pricing](https://uptimerobot.com/pricing/)
- [Better Stack Pricing](https://betterstack.com/pricing)
- [Sentry Pricing](https://sentry.io/pricing/)
- [PostHog Pricing](https://posthog.com/pricing)
- [Best Uptime Monitoring 2026](https://uptimerobot.com/knowledge-hub/monitoring/11-best-uptime-monitoring-tools-compared/)

---

## Summary: Emuni Infrastructure Recommendations

### Day 1 (MVP, $0/mo infra monitoring cost)
```
Cloud:        AWS il-central-1 (Tel Aviv)
Database:     Supabase Free (closest region: Frankfurt eu-central-1)
Backend:      NestJS on Railway ($5/mo) or AWS Lambda (free tier)
CI/CD:        GitHub Actions (2,000 free min/mo)
Errors:       Sentry Developer (free, 5K errors/mo)
Analytics:    PostHog Cloud (free, 1M events/mo)
Uptime:       UptimeRobot (free, 50 monitors)
Logging:      AWS CloudWatch (free tier)
Feature flags: PostHog (free, 1M requests/mo)
```

### Day 30+ (Post-launch, ~$30-60/mo)
```
Cloud:        AWS il-central-1
Database:     Supabase Pro ($25/mo) — still Frankfurt, but acceptable latency
Backend:      AWS ECS Fargate or App Runner in il-central-1
CI/CD:        GitHub Actions (still free tier)
Errors:       Sentry Team ($26/mo) — when error volume grows
Analytics:    PostHog Cloud (still free tier)
Uptime:       UptimeRobot (still free) or Better Stack ($24/mo)
Logging:      AWS CloudWatch or Better Stack
```

### Key Latency Note
Supabase does NOT yet offer AWS il-central-1 as a hosting region. Your Supabase database will be in Frankfurt (eu-central-1), adding ~50-80ms latency for DB queries from Israel. Mitigation options:
1. Accept it — 50-80ms is fine for most CRUD operations
2. Self-host PostgreSQL + PostGIS on AWS il-central-1 (more work, lower latency)
3. Wait for Supabase to add il-central-1 support (unknown timeline)
4. Use Supabase Edge Functions with regional invocation to reduce some latency

---

*Research conducted 2026-03-07. All pricing and availability should be verified before purchasing decisions.*
