# Colonial Farms 1776 — Growth Strategy & Technical Playbook

> **Last updated:** April 2026
> **Author:** Ric (developer/consultant)
> **Audience:** Developer reference + Claude Code context document
> **See also:** CLAUDE.md (repo root) for project context and active work queue

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Key Decisions](#key-decisions)
3. [Current State Assessment](#current-state-assessment)
4. [Phased Growth Plan](#phased-growth-plan)
5. [Shipping & Pricing Strategy](#shipping--pricing-strategy)
6. [Developer Automation Playbook](#developer-automation-playbook)
7. [Claude in Chrome Workflows](#claude-in-chrome-workflows)
8. [Target Customer Segments](#target-customer-segments)
9. [Budget Estimates](#budget-estimates)
10. [90-Day Action Plan](#90-day-action-plan)
11. [Key Success Metrics](#key-success-metrics)

---

## Executive Summary

Colonial Farms 1776 is a Maryland-based small farm brand selling shelf-stable canned meats (beef, chicken, turkey, pork in 28 oz cans), plus curated meat snacks, gourmet cheeses, and signature sauces from partner producers. The business is a one-man operation run from a farm where the owner raises beef cattle, with plans to eventually can his own beef as the ultimate brand differentiator.

This document outlines a phased plan to increase online sales, expand to Amazon as the primary growth channel, and build brand presence — all powered by a lightweight automation stack centered on **Claude Code** (repo-based scripting and content generation) and **Claude in Chrome** (browser automation for platform management). No cloud infrastructure is required at this stage.

The core insight: a developer with Claude Code + Claude in Chrome can give a solo farm operator the marketing and operational capabilities of a small team, all managed from a single GitHub repo.

**The guiding constraint:** Steve is a solo farmer. Every initiative must reduce his workload or directly drive revenue. If it creates new review burden, meeting overhead, or operational complexity without a clear payoff, it doesn't belong in the current phase.

---

## Key Decisions

These are strategic decisions already made. They should not be revisited without new evidence.

| Decision | Rationale |
|----------|-----------|
| **Stay on GoDaddy** (defer Shopify) | Site is live and selling. Steve knows the platform. A migration disrupts operations for a backend improvement that only matters at higher volume. Revisit when GoDaddy becomes a specific bottleneck or Amazon validates the business. |
| **Amazon is the #1 growth priority** | Canned meats are a proven Amazon category with existing buyer traffic. Every other channel requires Colonial Farms to bring its own customers — Amazon already has them. |
| **Repo-centric architecture** (no cloud infra) | Lambda, RDS, and Supabase are overkill for a side project supporting a one-man farm. Git repo + GitHub Actions + Claude API is sufficient and costs essentially $0. |
| **Cornerstone content over content treadmill** | 3–5 high-quality reusable pieces (farm story, buyer's guide, recipes) beat a weekly publishing cadence that buries Steve in review work. |
| **Focus beats breadth** | Nail GoDaddy + Amazon before adding Walmart, Etsy, eBay, or subscriptions. A solo operator spreading across 6 channels will be mediocre on all of them. |

---

## Current State Assessment

### Website & Platform

| Aspect | Current State | Gap |
|--------|--------------|-----|
| Platform | GoDaddy Website Builder (staying here for now) | Limited e-commerce features, no API access, weak SEO tools |
| Products | 6 active products across combos and 4-packs | Minimal descriptions, no SEO optimization, no structured data |
| Branding | Strong patriotic/heritage identity | Underleveraged — no farm story page, no behind-the-scenes content |
| Content | Near zero | No blog, no recipes, no educational content |
| Email | None | No list, no capture mechanism, no sequences |
| Analytics | Unknown | No GA4, no Search Console, no conversion tracking |
| Reviews | None | No social proof on products |
| SEO | Minimal | No structured data, thin content, limited keyword targeting |

### Current Product Line (from live store)

| Product | Price | Notes |
|---------|-------|-------|
| Supper and Appetizer Combo | $40.00 | Pick: protein (28oz) + appetizer + cheese + sauce |
| 4-can Variety Pack (you pick) | $78.00 | 4x 28oz cans, choose each protein |
| 4-can Beef Pack | $78.00 | 4x 28oz beef |
| 4-can Chicken Pack | $78.00 | 4x 28oz chicken |
| 4-can Turkey Pack | $78.00 | 4x 28oz turkey |
| 4-can Pork Pack | $78.00 | 4x 28oz pork |

**Component products** (sold as options within combos, not individually):
- Canned meats: Beef, Chicken, Turkey, Pork (28 oz) — branded Colonial Farms 1776, sourced from co-packer
- Wenzel's Farm: Summer Sausage (12 oz), Beef Sticks (8 oz), Beef Jerky (10 oz, +$9 upcharge in combo)
- Williams Gourmet Cheese: Smoked Cheddar (8 oz), Smoked Gouda (8 oz)
- Signature Sauces (12+ oz): Japanese Teriyaki, Caribbean Jerk, Chinese Sweet & Sour, Sweet Thai Chili, American BBQ, Texas Chili

**Empty categories:** Bundles, Suppers (both show "Coming soon")

See `products/catalog.json` for the full structured product catalog.

### Strengths

- Shelf-stable products = easy nationwide shipping (no cold chain)
- Authentic farm story: owner raises cattle on a Maryland farm
- Premium "craft proteins" positioning with heritage branding
- Large 28 oz cans offer strong value vs. competitors (Keystone sells 14.5 oz)
- Broader product line than initially expected: meats, snacks, cheeses, sauces, combos
- Future vertical integration: plans to can own beef

### Challenges

- One-man operation: extremely limited time for marketing and operations
- GoDaddy has no API for its website builder — automation requires browser-level interaction
- No existing email list, social following, or content library
- Currently sourcing from third-party producers (limited product differentiation today)
- Competitive Amazon space: Keystone Meats dominates with established listings and reviews
- No individual can sales — $78 4-pack is a high barrier for first-time buyers
- Shipping heavy 28 oz cans is expensive — margins depend on getting shipping strategy right

---

## Phased Growth Plan

### Phase 1: Foundation + Amazon Prep (Months 1–3)

**Goal:** Optimize the GoDaddy site, start Amazon application, establish data collection, create cornerstone content.

#### 1.1 GoDaddy Site Optimization

The site is live and functional. Optimize what's there rather than rebuilding:

- Rewrite all product descriptions with SEO-optimized copy (farm story, protein content, shelf life, versatility)
- Add structured data (JSON-LD) via GoDaddy's custom code injection if supported
- Create an "Our Story" page with farm photos and the owner's journey
- Add email capture with a 10% discount incentive
- Improve product photography (multiple angles, lifestyle/cooking shots)
- **Consider adding a single-can SKU** ($22–24) to lower the barrier for first-time buyers

**Why not Shopify?** Shopify's API access is compelling for automation, but a platform migration is disruptive and only pays off at higher order volume. GoDaddy works today. If it becomes a bottleneck (e.g., can't handle inventory sync, checkout conversion is poor, or Amazon drives enough volume to justify deeper automation), revisit then.

#### 1.2 Amazon Marketplace — Application & Prep

Amazon is the single highest-leverage channel for shelf-stable canned meats. Start the application process immediately — Grocery & Gourmet Foods category approval can take 2–4 weeks.

- **Account setup:** Apply for Professional Seller account ($39.99/month) and Grocery category approval
- **Listing content:** Generate A+ Content with farm story, comparison charts (28 oz vs. Keystone's 14.5 oz), recipe suggestions
- **Product photography:** Amazon-compliant images (white background main image, lifestyle shots, infographics)
- **Pricing strategy:** See [Shipping & Pricing Strategy](#shipping--pricing-strategy) section
- **Fulfillment:** Start with FBM (Fulfilled by Merchant) to control costs and learn the process. Consider FBA once volume justifies sending inventory to Amazon warehouses.

#### 1.3 Amazon Reviews Strategy

Reviews are the make-or-break factor for new Amazon listings. Zero-review products don't convert. This needs a specific plan, not an afterthought.

- **Amazon Vine:** Enroll eligible products immediately after listing. Vine provides early reviews from trusted reviewers in exchange for free product. Cost: ~$200 per parent ASIN (one-time).
- **Request a Review:** Use Amazon's built-in "Request a Review" button aggressively for every order. Can be semi-automated via Claude in Chrome.
- **Cross-channel seeding:** Include card inserts in GoDaddy direct orders encouraging customers to leave an Amazon review (within Amazon's TOS — no incentivized reviews).
- **Target:** 15–25 reviews per product within first 90 days of listing. This is the minimum threshold where conversion rates meaningfully improve.
- **Review monitoring:** Track review velocity and sentiment. Negative reviews need rapid response.

#### 1.4 Email Marketing Setup

- Set up Mailchimp (free tier) or Klaviyo (free up to 250 contacts)
- Create welcome sequence: 3–4 emails introducing the brand, farm story, and a recipe
- Offer 10% first-order discount for email signups
- Plan monthly newsletter: new products, recipes, farm updates, seasonal promos

#### 1.5 Analytics & Tracking

- Install Google Analytics 4 and Google Tag Manager
- Set up conversion tracking for purchases, add-to-cart, and email signups
- Implement Facebook/Meta Pixel for future ad retargeting
- Set up Google Search Console and submit sitemap

#### 1.6 Cornerstone Content

Instead of a content treadmill, create 3–5 high-quality pieces that serve multiple purposes (site pages, Amazon A+ content, email sequences, social media):

1. **"Our Story"** — The farm, the cattle, the vision for farm-to-can. Used on: site, Amazon A+ content, email welcome sequence.
2. **"Why 28 oz Canned Meats?"** — Buyer's guide comparing CF1776 to competitors (Keystone, SPAM). Shelf life, value per ounce, quality. Used on: site blog, Amazon listing copy.
3. **2–3 Recipes** — Simple, appealing meals using CF1776 canned meats. Used on: site, Amazon images, social media, email.
4. **"Emergency Preparedness Pantry Guide"** — Targets the prepper segment. Used on: site blog, Amazon backend keywords, social.

This is enough content to populate the site, seed Amazon listings, fill the email welcome sequence, and provide months of social media material — without putting Steve on a weekly review treadmill.

---

### Phase 2: Amazon Launch + Optimization (Months 3–6)

**Goal:** Get products live on Amazon, optimize listings, start building review base.

#### 2.1 Amazon Go-Live

- Create all Amazon listings using content from Phase 1
- Enroll in Amazon Vine for initial reviews
- Launch Amazon Sponsored Products with conservative budget ($10–15/day)
- Target keywords: "canned beef", "shelf stable meat", "emergency food", "survival food", "craft canned meat"
- Monitor and optimize listings weekly: adjust keywords, pricing, images based on performance

#### 2.2 Fulfillment Operations

- Establish FBM shipping workflow: packing, labeling, carrier selection
- Track shipping costs per order to validate pricing model
- Evaluate FBA once doing 30+ orders/month on Amazon (reduced shipping burden on Steve, Prime badge)

#### 2.3 GoDaddy Store Refinements

Based on data from Phase 1:
- Update product descriptions with SEO-optimized copy
- Add cornerstone blog content to the site
- Optimize based on GA4 data: which pages convert, where visitors drop off
- Consider adding individual can sales if 4-pack conversion rate is low

#### 2.4 Content Expansion (Moderate Pace)

- Add 1–2 blog posts per month (AI-drafted, Ric reviews, Steve approves)
- Monthly email newsletter to growing list
- Social media: 2–3 posts per week on Instagram (batched weekly via AI generation)

---

### Phase 3: Scale & Diversify (Months 6–12)

**Goal:** Scale what's working on Amazon, consider additional channels, build community.

#### 3.1 Amazon Scaling

- Increase Sponsored Products budget based on ROAS data
- Launch Sponsored Brands campaigns if brand registry is approved
- A/B test listing elements: titles, images, pricing
- Evaluate FBA transition
- Consider additional product formats for Amazon (individual cans, 2-packs, variety sampler)

#### 3.2 Additional Channels (only after Amazon is stable)

Evaluate these one at a time based on effort vs. expected return:

| Platform | Why | Effort | When to Consider |
|----------|-----|--------|-----------------|
| Etsy | Perfect for "artisan/small-batch" positioning | Low | When Amazon is doing $2K+/month |
| Facebook/Instagram Shop | Free, leverages social content | Low | When social media presence is established |
| Walmart Marketplace | Growing, less competition | Medium | When Amazon is doing $5K+/month |
| Local farmers markets | Brand building, direct feedback | Low | Seasonally, as Steve's schedule allows |

#### 3.3 Subscription / Bundle Model

- "Patriot Pantry Box": curated monthly mix of canned meats, snacks, and cheese
- Start manual (track in spreadsheet), automate only after validating demand with 10+ subscribers
- Offer 10–15% subscription discount to lock in recurring revenue

#### 3.4 Customer Reviews & Social Proof

- Post-purchase review request emails 7 days after delivery
- Feature customer photos and testimonials on product pages and social
- Encourage video reviews with incentive (15% off next order)

#### 3.5 Content Marketing (Sustainable Cadence)

Once cornerstone content is performing and Amazon is generating revenue:

| Segment | Keywords to Target |
|---------|-------------------|
| Recipe seekers | "canned beef recipes", "what to make with canned chicken", "emergency food recipes" |
| Information seekers | "how long does canned meat last", "is canned meat healthy", "canned vs fresh meat nutrition" |
| Preppers | "best canned meats for emergency preparedness", "survival pantry list", "long shelf life foods" |
| Farm curious | "raising beef cattle in Maryland", "farm to can process", "small farm canned meat" |

Target: 2–4 posts per month, only once the review workflow is smooth and not burdensome.

---

### Phase 4: Optimize & Prepare for Farm-to-Can (Months 12+)

**Goal:** Increase AOV, lifetime value, and prepare for own-beef canning.

#### 4.1 Paid Advertising (only after organic foundations are in place)

- Google Shopping Ads: high-intent keywords ("buy canned beef online")
- Facebook/Instagram Ads: interest-based (preppers, homesteaders, hunting/fishing, military)
- Amazon Sponsored Products: already running, optimize and scale
- Start budget: $300–500/month, scale based on ROAS

#### 4.2 Product Line Expansion

- Meal kits: canned meats + sides for complete shelf-stable meals
- Gift boxes: holiday and special occasion bundles
- Bulk/wholesale pricing for preppers and group buys
- Seasonal limited editions (BBQ season, holiday boxes)

#### 4.3 Preparing for Own-Beef Canning

This is the transformative milestone:

- Research USDA inspection requirements for on-farm canning in Maryland
- Document the journey on social media and blog ("From Our Pasture to Your Pantry" campaign)
- Pre-sell limited runs of "Farm-Raised, Farm-Canned" beef at a premium
- Use the transition as a major PR/marketing event

#### 4.4 Strategic Partnerships

- Prepper/survival content creators for sponsored reviews and affiliate deals
- Outdoor/hunting/camping influencers
- Military family organizations for bulk sales
- Explore co-packing for other small farms

#### 4.5 Platform Reassessment

At this point, if GoDaddy is limiting growth (poor conversion rate, can't handle order volume, manual inventory sync is breaking), evaluate Shopify migration with real data to justify the switch.

---

## Shipping & Pricing Strategy

> **Status:** Needs input from Steve on cost data. Framework is ready; fill in the numbers.

### Why This Matters

28 oz cans are heavy. Shipping cost directly impacts margins and determines whether Amazon FBM is viable. This must be figured out before Amazon listings go live.

### Unit Economics (fill in with Steve)

| Item | Cost | Notes |
|------|------|-------|
| Cost per 28 oz can from co-packer | **TODO** | Need from Steve |
| Shipping materials per 4-pack | **TODO** | Box, padding, tape |
| USPS Priority Mail medium flat rate | ~$16.10 | Fits 2–3 cans |
| USPS Priority Mail large flat rate | ~$22.45 | Fits 4 cans |
| UPS Ground (estimated, 7 lbs) | ~$12–18 | Varies by zone |
| Amazon FBA fee (estimated, 28 oz can) | **TODO** | Research after category approval |

### Pricing Analysis

| Product | Revenue | Est. Shipping | Est. COGS | Est. Margin |
|---------|---------|---------------|-----------|-------------|
| 4-can Pack (GoDaddy, customer pays shipping) | $78.00 | Passed to customer | TODO | TODO |
| 4-can Pack (Amazon FBM, free shipping) | $78.00 | ~$18–22 | TODO | TODO |
| 4-can Pack (Amazon FBA) | $78.00 | FBA fee TBD | TODO | TODO |
| Supper Combo (GoDaddy) | $40.00 | Passed to customer | TODO | TODO |

### Shipping Strategy Options

1. **GoDaddy site:** Charge actual shipping or set flat-rate tiers ($8 for combos, $12 for 4-packs). Consider free shipping threshold at $100+ to increase AOV.
2. **Amazon FBM:** Free shipping is expected on Amazon. Build shipping cost into price. May need to price 4-packs at $82–85 on Amazon to maintain margins.
3. **Amazon FBA:** Higher fees but Prime badge significantly increases conversion. Evaluate once volume hits 30+ orders/month.
4. **USPS flat rate boxes** are likely the best FBM option for heavy canned goods — predictable cost regardless of destination zone.

### Competitive Pricing Reference

| Competitor | Product | Size | Amazon Price | Price/oz |
|------------|---------|------|-------------|----------|
| Keystone Meats | Canned Beef | 14.5 oz | **TODO** | **TODO** |
| Mountain Essentials | Canned Beef | 28 oz | **TODO** | **TODO** |
| Grabill Country Meats | Canned Beef | 28 oz | **TODO** | **TODO** |
| SPAM | Classic | 12 oz | **TODO** | **TODO** |
| Colonial Farms 1776 | Canned Beef (4-pack) | 28 oz x4 | $78.00 | $0.70/oz |

**Action item:** Run a competitor price check (via Claude in Chrome on Amazon) to fill in these numbers before setting Amazon pricing.

---

## Developer Automation Playbook

### Architecture: Repo-Centric, No Cloud Required

The traditional approach would be Lambda functions, databases, and cloud dashboards. For a side project supporting a one-man farm operation, that's overkill. Instead:

| Layer | Tool | What It Does |
|-------|------|-------------|
| **Content Generation** | Claude Code + Claude API | Generates all marketing content from prompt templates in the repo |
| **Platform Management** | Claude in Chrome | Navigates GoDaddy, Amazon Seller Central via browser |
| **Data Management** | Git repo (JSON/MD files) | catalog.json is source of truth; everything versioned and reviewable |
| **Scheduling** | GitHub Actions | Weekly content batches, competitor checks, analytics pulls (2,000 free min/month) |
| **Future (if needed)** | Supabase or lightweight VPS | Only add if project outgrows the repo approach |

### Automation Project 1: AI Content Engine

**Priority: HIGH | Effort: Medium | Impact: High**

Python scripts in `scripts/` that call the Claude API to generate content from prompt templates:

- `generate_product_copy.py` — Reads catalog.json, generates SEO-optimized descriptions for website and Amazon
- `generate_blog_post.py` — Takes keyword + outline, generates full blog post draft
- `generate_email.py` — Creates newsletter and email sequence drafts
- `generate_social_batch.py` — Produces a week's worth of social media captions
- `generate_amazon_listing.py` — Creates complete Amazon listing packages (title, bullets, description, backend keywords, A+ content)

**Workflow:** Script generates draft → saved to `content/` or `products/` directory → Ric reviews → approved content is published (manually or via Claude in Chrome)

### Automation Project 2: Claude in Chrome Workflows

**Priority: HIGH | Effort: Low-Medium | Impact: High**

Documented browser workflows that Claude in Chrome can execute:

**GoDaddy Product Updates:**
1. Navigate to GoDaddy site editor → Store → Products
2. Select product by name
3. Update description field with content from `products/godaddy-updates/`
4. Update pricing if changed
5. Save and verify on live site

**Amazon Listing Creation:**
1. Navigate to Seller Central → Catalog → Add Products
2. Select "I'm adding a product not sold on Amazon"
3. Choose category (Grocery & Gourmet Food → Canned & Packaged Meats)
4. Fill all fields from `products/amazon-listings/{product-slug}.json`
5. Upload product images
6. Submit and verify listing

**Amazon Review Requests:**
1. Navigate to Seller Central → Orders → Manage Orders
2. For each delivered order, click "Request a Review"
3. Track which orders have been requested in a local log

**Competitor Research:**
1. Navigate to Amazon best sellers in canned beef/meat categories
2. Capture pricing, review counts, ratings for key competitors
3. Save to `competitor-data/pricing-snapshots/YYYY-MM-DD.json`

### Automation Project 3: Competitor Intelligence

**Priority: HIGH | Effort: Low | Impact: High**

Elevated to HIGH priority because Amazon pricing decisions depend on competitor data.

- `scripts/competitor_check.py` — Uses Claude API with web search tool to gather competitor pricing and review data
- Stores snapshots in `competitor-data/pricing-snapshots/`
- Weekly GitHub Action trigger
- Claude API summarizes changes: "Keystone raised their 28oz beef price by $2, now $X. Mountain Essentials has 47 new reviews this month."

### Automation Project 4: Scheduled Content Pipeline (GitHub Actions)

**Priority: LOW (Phase 2+) | Effort: Low | Impact: Medium**

`.github/workflows/weekly-tasks.yml`:

- **Monday:** Generate weekly social media caption batch
- **Wednesday:** Run competitor price check
- **Friday:** Generate blog post outline for next week (Ric reviews over weekend)

All outputs committed to the repo as PRs for review.

### Automation Project 5: Analytics & Reporting

**Priority: LOW (Phase 2+) | Effort: Medium | Impact: Medium**

- `scripts/analytics_report.py` — Pulls data from Google Analytics 4 API and Amazon SP-API
- Claude API generates a plain-English weekly summary
- Output: markdown report in `docs/reports/YYYY-WNN-weekly.md`
- Could be emailed to owner via a simple SMTP script or SendGrid free tier

### Automation Project 6: Platform Migration Toolkit (Deferred)

**Priority: DEFERRED | Effort: Medium | Impact: High (when needed)**

If and when GoDaddy becomes a bottleneck, this toolkit enables migration to Shopify:

- `scripts/shopify_migrate_products.py` — Reads catalog.json, creates products via Shopify Admin API
- `scripts/shopify_theme_setup.py` — Applies theme customizations (colors, fonts, layout adjustments)
- Shopify Liquid templates in `templates/shopify/` for custom sections (farm story, recipe cards)
- Claude in Chrome handles non-API tasks: domain pointing, payment setup, shipping zone configuration

**Trigger conditions for revisiting:** Order volume exceeds 100/month, inventory sync across channels becomes unmanageable, or GoDaddy checkout conversion is measurably lower than industry average.

---

## Claude in Chrome Workflows — Detailed Reference

### When to Use Claude in Chrome vs. Claude Code

| Task | Use Claude Code | Use Claude in Chrome |
|------|----------------|---------------------|
| Generate content (descriptions, blog posts, emails) | ✅ | |
| Create/edit files in repo | ✅ | |
| Call APIs programmatically (Claude, GA4) | ✅ | |
| Update product on GoDaddy | | ✅ |
| Create listing on Amazon Seller Central | | ✅ |
| Request reviews on Amazon | | ✅ |
| Browse competitor pages on Amazon | | ✅ |
| Post to social media (if not using Buffer/Later) | | ✅ |
| Research (pricing, keywords, trends) | | ✅ |

### Workflow Documentation Standard

Each workflow doc in `browser-workflows/` follows this format:

```markdown
# Workflow: [Name]
## Goal
What this workflow accomplishes.
## Prerequisites
What needs to be ready before running this workflow.
## Starting URL
The URL to navigate to first.
## Steps
1. Step-by-step instructions with expected page states
2. Reference specific selectors or text labels where helpful
3. Note any fields that pull from repo data files
## Validation
How to verify the workflow completed successfully.
## Notes
Edge cases, known issues, things to watch for.
```

---

## Target Customer Segments

| Segment | Why They Buy | How to Reach Them | Key Messaging |
|---------|-------------|-------------------|---------------|
| Preppers / Survivalists | Shelf life, food security, emergency prep | Amazon search, prepper forums, YouTube, Facebook groups | 5-year shelf life, fully cooked, no refrigeration, American-made |
| Homesteaders | Local sourcing, authenticity, knowing the producer | Farmers markets, Instagram, farm directories | Farm-raised cattle, small-batch, Maryland family farm |
| Outdoor / Camping | Portable, shelf-stable, high-protein | Amazon search, outdoor forums, YouTube | Ready to eat on the trail, high protein, no refrigeration |
| Military Families | Care packages, deployment food, patriotic alignment | Military spouse groups, patriotic brands, Amazon | American-made, patriotic heritage, long shelf life |
| Convenience / Busy Families | Quick meals, pantry staples | Amazon search, Google search, meal planning content | Fully cooked, heat and serve, gourmet quality |
| Gift Buyers | Unique food gifts, holiday baskets | Etsy (Phase 3), holiday marketing, gift guides | Heritage brand, premium variety packs, farm story |

---

## Budget Estimates

| Item | Monthly | Annual | Phase |
|------|---------|--------|-------|
| GoDaddy (existing plan) | ~$20 | ~$240 | 1 |
| Domain (keep existing) | — | $15 | 1 |
| Email Marketing (Mailchimp/Klaviyo free → paid) | $0–45 | $0–540 | 1 |
| Claude API (content generation) | $20–50 | $240–600 | 1 |
| Amazon Seller (Professional) | $39.99 | $480 | 1 |
| Amazon Vine (one-time per ASIN) | — | ~$800–1,200 | 1 |
| Product Photography (one-time) | — | $500–1,500 | 1 |
| Amazon Sponsored Products | $300–450 | $3,600–5,400 | 2 |
| Paid Advertising — Google, Meta (Phase 4 only) | $300–500 | $3,600–6,000 | 4 |
| **TOTAL (Year 1 Estimate)** | | **$5,500–$10,000** | |

Infrastructure cost is essentially $0 — GitHub repo is free, GitHub Actions free tier is sufficient, Claude API is the only per-use cost and it's modest at this volume. Shopify ($468/year) is removed from the budget until if/when a migration is justified.

---

## 90-Day Action Plan

### Weeks 1–2: Data & Amazon Application

- [x] Set up repo structure, populate catalog.json with current product data
- [ ] Apply for Amazon Seller Central Professional account
- [ ] Apply for Grocery & Gourmet Foods category approval (can take 2–4 weeks)
- [ ] Create prompt templates for product descriptions and Amazon listings
- [ ] Run competitor price check on Amazon (Keystone, Mountain Essentials, Grabill, SPAM)
- [ ] Work out shipping cost model with Steve (per-can costs, shipping materials, carrier rates)

### Weeks 3–4: Content & Photography

- [ ] Professional product photography session (Amazon-compliant + lifestyle shots)
- [ ] Generate SEO-optimized product descriptions for all GoDaddy products
- [ ] Write cornerstone content: "Our Story", buyer's guide, 2–3 recipes
- [ ] Set up email capture on GoDaddy site with 10% discount offer
- [ ] Set up Google Analytics 4, Search Console, Meta Pixel on current site
- [ ] Set up Mailchimp/Klaviyo, create welcome email sequence

### Weeks 5–8: Amazon Listing & Site Updates

- [ ] Generate Amazon listing content for all canned meat products (title, bullets, description, backend keywords, A+ content)
- [ ] Create Amazon listings (via Claude in Chrome on Seller Central)
- [ ] Enroll products in Amazon Vine
- [ ] Update GoDaddy product descriptions with new optimized copy (via Claude in Chrome)
- [ ] Add cornerstone content to GoDaddy site
- [ ] Build AI content engine scripts (generate_product_copy.py, generate_amazon_listing.py)
- [ ] Launch first email newsletter

### Weeks 9–12: Amazon Optimization

- [ ] Launch Amazon Sponsored Products ($10–15/day budget)
- [ ] Monitor and optimize Amazon listings: keyword performance, conversion rate, ad spend
- [ ] Use "Request a Review" on all Amazon orders
- [ ] Begin social media posting on Instagram (2–3x/week, batched)
- [ ] Create Instagram and Facebook accounts if not existing
- [ ] Review all data, adjust strategy for Phase 2
- [ ] Assess: Is GoDaddy becoming a bottleneck? Is Amazon revenue validating the business?

---

## Key Success Metrics

| Metric | 3-Month Target | 6-Month Target | 12-Month Target |
|--------|---------------|----------------|-----------------|
| Monthly GoDaddy Revenue | $1,000–2,000 | $2,000–3,000 | $3,000–5,000 |
| Monthly Amazon Revenue | — (listing) | $1,000–3,000 | $5,000–10,000 |
| Amazon Reviews (per product) | 15–25 | 50–100 | 150+ |
| Email List Size | 100–250 | 500–1,000 | 2,000–3,000 |
| Monthly Website Traffic | 300–500 | 1,000–2,000 | 3,000–5,000 |
| Amazon Conversion Rate | 5–8% | 8–12% | 12–15% |
| Repeat Customer Rate | 10% | 15% | 25%+ |

Note: Revenue targets are adjusted to reflect a focused GoDaddy + Amazon strategy rather than the previous multi-channel projections. Amazon metrics are added since it's now the primary growth channel.
