# Colonial Farms 1776 — Project Context

## Project Overview

This repo is the developer operations base for growing online sales of **Colonial Farms 1776** (colonialfarms1776.com), a small Maryland farm brand selling shelf-stable canned meats and curated specialty foods. The farm owner is a solo operator who raises beef cattle and currently sources branded canned meats from third-party producers. He plans to eventually can his own farm-raised beef.

The developer (Ric) is an AI engineer providing strategic consulting and technical automation on his own time. This is not an employer project — no corporate AWS environment is involved.

## Business Context

**What they sell:**
- Colonial Farms 1776 branded canned meats: beef, chicken, turkey, pork (28 oz cans) — shelf-stable, fully cooked, heat-and-serve
- Wenzel's Farm meat snacks: summer sausage, beef sticks, beef jerky
- Williams Gourmet Cheese: smoked cheddar, smoked gouda

**Current platform:** GoDaddy Website Builder with integrated e-commerce store

**Target customers:** Preppers/survivalists, homesteaders, outdoor/camping enthusiasts, military families, gift buyers, busy families wanting pantry convenience

**Key brand differentiators:**
- Authentic farm story (owner raises cattle on a Maryland farm)
- Patriotic/heritage branding ("1776", craft proteins)
- Large 28 oz cans (strong value vs. competitors)
- Future: farm-raised, farm-canned beef (ultimate differentiator)

**Primary competitors on Amazon:** Keystone Meats, Mountain Essentials, Grabill Country Meats, SPAM

## Technical Approach

This project uses a **lightweight, repo-centric architecture** — no cloud infrastructure required at this stage.

### Core Tools
- **Claude Code** (this tool): Content generation, scripting, data management, Shopify theme development, API integration
- **Claude in Chrome** (browser agent): GoDaddy store management, Amazon Seller Central operations, Shopify admin setup, competitor research
- **GitHub Actions**: Scheduled tasks (content batches, competitor checks, analytics pulls)
- **Claude API**: Called from Python scripts for batch content generation

### What We Are NOT Using (intentionally)
- No AWS Lambda, RDS, or Supabase at this stage
- No custom dashboards or frontends yet
- These may be added later if the project outgrows the repo-based approach

## Repo Structure

```
colonial-farms-1776/
├── CLAUDE.md                      # THIS FILE — project context for Claude Code
├── docs/
│   └── STRATEGY.md                # Full technical strategy reference
├── products/
│   ├── catalog.json               # Master product catalog (source of truth)
│   ├── amazon-listings/           # Generated Amazon listing content (JSON per product)
│   ├── shopify-products/          # Shopify-formatted product data
│   └── godaddy-updates/           # Content staged for GoDaddy store updates
├── content/
│   ├── blog-posts/                # AI-generated blog post drafts (.md files)
│   ├── email-campaigns/           # Newsletter and sequence drafts
│   ├── social-media/              # Batched social media captions
│   └── recipes/                   # Recipe content for blog and product pages
├── competitor-data/
│   └── pricing-snapshots/         # Periodic competitor price captures
├── scripts/
│   ├── generate_product_copy.py   # Generate product descriptions from catalog.json
│   ├── generate_blog_post.py      # Blog content pipeline
│   ├── generate_amazon_listing.py # Amazon listing generator
│   ├── generate_email.py          # Email/newsletter content
│   ├── generate_social_batch.py   # Social media caption batches
│   ├── competitor_check.py        # Competitor price monitoring
│   └── analytics_report.py        # Pull and summarize analytics
├── templates/
│   ├── prompts/                   # Claude API prompt templates
│   │   ├── product_description.md
│   │   ├── blog_outline.md
│   │   ├── amazon_listing.md
│   │   ├── email_newsletter.md
│   │   └── social_caption.md
│   └── shopify/                   # Shopify Liquid theme customizations
├── browser-workflows/             # Claude in Chrome workflow documentation
│   ├── godaddy-product-update.md  # Steps for updating GoDaddy products
│   ├── amazon-listing-create.md   # Steps for creating Amazon listings
│   └── shopify-migration.md       # Steps for Shopify migration tasks
├── site/                          # Legacy HTML/CSS site files (historical reference)
└── .github/
    └── workflows/
        └── weekly-tasks.yml       # GitHub Actions for scheduled automation
```

## Conventions

### Content Generation
- All generated content goes through a **draft → review → publish** pipeline
- Drafts are written to the appropriate `content/` or `products/` subdirectory
- File naming: `YYYY-MM-DD-slug-name.md` for blog posts, `product-slug.json` for product data
- Nothing is published without human review — automation creates drafts, not final content

### Product Data
- `products/catalog.json` is the single source of truth for all product information
- Platform-specific formats (Amazon, Shopify, GoDaddy) are generated FROM the catalog
- When product details change, update catalog.json first, then regenerate platform files

### Prompt Templates
- Stored in `templates/prompts/` as markdown files
- Each template includes: context about the brand, tone guidelines, output format spec
- Templates reference catalog.json data — they don't hardcode product details

### Brand Voice
- Tone: Warm, authentic, patriotic without being preachy. Like a friendly farmer who's proud of his work.
- Emphasize: quality, shelf life, convenience, farm heritage, American-made
- Avoid: corporate jargon, health claims without backing, disparaging competitors
- Keywords to weave in naturally: craft proteins, shelf-stable, fully cooked, heat and serve, farm-raised, small-batch, Maryland farm

### Browser Workflows (Claude in Chrome)
- Documented in `browser-workflows/` as step-by-step markdown guides
- Each workflow describes: the goal, the starting URL, the sequence of actions, and validation steps
- These serve as reference for Claude in Chrome sessions AND as documentation for Ric

## Current Phase & Priorities

**Current phase:** Phase 1 — Foundation (see docs/STRATEGY.md for full phase details)

### Active Work Queue (update this as tasks complete)
1. [ ] Set up repo structure and populate catalog.json with current product data
2. [ ] Create prompt templates for product descriptions and blog posts
3. [ ] Generate SEO-optimized product descriptions for all current products
4. [ ] Generate first batch of 5 blog posts (recipes, farm story, buyer guides)
5. [ ] Document Claude in Chrome workflow for GoDaddy product updates
6. [ ] Research and document Amazon Seller Central application process
7. [ ] Generate Amazon listing content for all canned meat products
8. [ ] Set up Google Analytics 4 and Search Console on current site
9. [ ] Create email marketing welcome sequence (3-4 emails)
10. [ ] Evaluate Shopify migration: theme selection, cost analysis, migration plan

### Upcoming (Phase 2)
- Amazon Seller Central setup and first listings
- Shopify migration execution
- Multi-channel inventory tracking (spreadsheet-based initially)
- Social media content calendar and first month of posts

## Key URLs
- **Live site:** https://colonialfarms1776.com/
- **GoDaddy admin:** (access via Claude in Chrome when needed)
- **Amazon Seller Central:** https://sellercentral.amazon.com/ (once account is created)

## Important Notes
- The farm owner manages day-to-day operations solo — all automation should REDUCE his workload, not create new tasks for him
- Shipping cost matters: 28 oz cans are heavy. Shipping strategy is a key consideration for pricing and margins.
- The long-term brand story is "farm-to-can" — everything we do now should build toward that narrative
- This project is on Ric's own time — keep solutions simple, maintainable, and low-cost
