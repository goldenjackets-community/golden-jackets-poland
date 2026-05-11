# 🏆 Golden Jackets Brazil

Community website celebrating Brazilian professionals who earned all active AWS certifications.

🔗 **[goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)**

## Architecture

```
                    ┌─────────────┐
                    │  CloudFront  │
                    │  (CDN + SSL) │
                    └──────┬──────┘
                           │
                    ┌──────┴──────┐
                    │   WAF v2    │
                    │ (RateLimit  │
                    │  +CommonRules)│
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
       ┌──────┴──────┐ ┌──┴───┐ ┌──────┴──────┐
       │  S3 (www)   │ │  S3  │ │  S3 (origin)│
       │  Website    │ │Backup│ │  Website    │
       └─────────────┘ └──────┘ └─────────────┘

       ┌─────────────┐ ┌──────────────┐ ┌───────────┐
       │   Cognito    │ │ API Gateway  │ │  Route 53  │
       │  User Pool   │ │  (HTTP API)  │ │   (DNS)    │
       └──────┬──────┘ └──────┬───────┘ └───────────┘
              │               │
              │    ┌──────────┼──────────┬──────────┐
              │    │          │          │          │
              │ ┌──┴───┐ ┌───┴──┐ ┌─────┴────┐ ┌──┴──────┐
              │ │Lambda│ │Lambda│ │  Lambda   │ │ Lambda  │
              │ │Apply │ │Article│ │ Sponsor  │ │ Counter │
              │ └──┬───┘ └───┬──┘ └─────┬────┘ └────┬────┘
              │    │         │          │           │
              │    ▼         ▼          ▼           ▼
              │  GitHub    GitHub      SNS      DynamoDB
              │   PR        PR      + SES    (visitors +
              │                              partner clicks)
       ┌──────┴──────┐
       │  Lambda     │
       │  Admin API  │
       └──────┬──────┘
              │
              ▼
         DynamoDB
       (privacy consent
        + partner clicks)

       ┌─────────────┐  ┌─────────────┐
       │ AWS Backup  │  │   Budgets   │
       │ Daily/Weekly│  │  $10/month  │
       │ Monthly     │  │   alarm     │
       └─────────────┘  └─────────────┘
```

## AWS Services

| Service | Purpose |
|---------|---------|
| **S3** | Static website hosting (2 buckets) |
| **CloudFront** | CDN, SSL termination, caching |
| **WAF v2** | Rate limiting, scrapers block, common rules (XSS/SQLi) |
| **Route 53** | DNS management |
| **Cognito** | User authentication (Members Lounge) + auto-refresh token |
| **API Gateway** | HTTP API with rate limiting (10 req/s, burst 20) |
| **Lambda** | Backend logic (apply, article, sponsor, admin, visitor counter) |
| **DynamoDB** | Visitor counter, partner click tracking, privacy consent |
| **SES** | Transactional emails (sandbox) |
| **SNS** | Admin notifications + Discord webhook |
| **AWS Backup** | Automated S3 backups (daily/weekly/monthly) |
| **Budgets** | Cost monitoring ($10/month alarm) |
| **GitHub Actions** | CI/CD pipeline + auto-numbering cards |

## Project Structure

```
├── index.html              # Main website
├── members.html            # Members Lounge (authenticated)
├── admin.html              # Admin Console (restricted)
├── card-generator.html     # Member card generator
├── config.js               # Centralized config (admin email, API URL)
├── privacy.html            # LGPD Privacy Policy
├── robots.txt              # SEO - search engine directives
├── sitemap.xml             # SEO - sitemap for Google
├── assets/
│   ├── members/            # Member photos
│   ├── partners/           # Partner logos (Sundog Education)
│   ├── badges/             # AWS certification badges
│   └── *.png / *.jpg       # Site assets
├── .github/
│   └── workflows/
│       ├── deploy.yml      # S3 deploy + CloudFront invalidation + auto-numbering
│       ├── deploy-staging.yml  # Staging deploy
│       └── create-user.yml # User onboarding automation
├── BACKLOG.md              # Project backlog
├── SECURITY.md             # Security policy
└── README.md
```

## CI/CD

### Deploy (`deploy.yml`)
- Triggers on push to `main`
- Auto-numbers member cards without `card-number`
- Syncs to S3 buckets (origin + www)
- Invalidates CloudFront cache
- Runs smoke tests (site, lounge, admin, APIs)

### User Onboarding (`create-user.yml`)
- Triggers on PR merge (new members)
- Creates Cognito user
- Sends welcome email with 30min delay

## Backup Strategy

| Schedule | Retention |
|----------|-----------|
| Daily (5AM UTC) | 7 days |
| Weekly (Sunday) | 30 days |
| Monthly (1st) | 365 days |

## Security

- All traffic served over HTTPS via CloudFront
- WAF v2 with rate limiting, scraper blocking, and AWS Common Rules
- API Gateway rate limiting (10 req/s, burst 20)
- Input validation in all Lambdas (sanitize name, email, URL)
- Cognito authentication for Members Lounge with auto-refresh token (30 days)
- Admin Console restricted to authorized email via JWT
- CORS restricted to goldenjacketsbrazil.com domain
- S3 buckets with versioning enabled
- No secrets stored in repository
- GitHub Actions uses OIDC federation (no static credentials)
- LGPD compliant: privacy policy, consent checkbox, auditable consent in DynamoDB

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| POST | `/apply` | Member application → GitHub PR |
| POST | `/article` | Article submission → GitHub PR |
| POST | `/sponsor` | Sponsor inquiry → notification |
| POST | `/admin` | Admin operations (authenticated) |
| GET | `/count` | Visitor counter |
| POST | `/click` | Partner click tracking |
| GET | `/clicks` | Partner click stats (with month filter) |

## Partners

| Partner | Type |
|---------|------|
| **Tutorials Dojo** | Discount codes + freebies (practice exams, ebooks, courses) |
| **Sundog Education** | Discount code (GOLDEN_BRAZIL) + 5 free vouchers |

## Admin Features

- List/Create/Delete Cognito users
- Resend pending invitations
- Backup status + restore (double confirmation)
- Partner click stats (filter by partner + month)
- Export members CSV
- Community metrics (members by month)
- Promote Challenger → Golden Jacket
- View project backlog

## Community

- **Website**: [goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)
- **LinkedIn**: [Golden Jackets Brazil](https://www.linkedin.com/company/golden-jackets-brazil)
- **YouTube**: [@GoldenJacketsBrazil](https://www.youtube.com/@GoldenJacketsBrazil)
- **Spotify**: [Golden Jackets Podcast](https://open.spotify.com/episode/4JcjaBZb6uuLQnAyGw0PJF)
- **Discord**: [Join server](https://discord.gg/qntq7b7UqF)

## Contributing

Members can submit articles and content through the Members Lounge. For technical contributions, please open an issue or pull request.

## License

This project is maintained by the Golden Jackets Brazil community.

---

*Independent community, not officially affiliated with Amazon Web Services.*

*Last updated: 10/05/2026*
