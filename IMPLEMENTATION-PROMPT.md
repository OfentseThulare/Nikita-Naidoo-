# Website Implementation Prompt — nikitatrusha.co.za

> **Instructions for Claude Code**: Implement ALL of the following changes to `/index.html`. This is a single-file static website (all CSS, HTML, JS inline). Preserve the existing design system, animation patterns, and code structure. Do NOT create separate files — everything stays in `index.html` unless explicitly stated otherwise (robots.txt, llms.txt, sitemap.xml are exceptions).

---

## DESIGN SYSTEM (preserve exactly)

```
--blue-primary: #0033A0     --blue-dark: #001F6B
--blue-light: #E8F0FB       --blue-accent: #1A56DB
--white: #ffffff             --text-primary: #1a1a2e
--text-secondary: #4a4a68   --text-muted: #7a7a96
--radius-sm: 6px  --radius-md: 12px  --radius-lg: 20px
--max-width: 1200px          Font: Inter (Google Fonts)
Animation: .reveal class + IntersectionObserver
```

---

## PHASE 1: SEO FOUNDATION & META OVERHAUL

### 1.1 Update `<title>` and meta tags

```html
<title>Nikita Naidoo | Financial Adviser for Business Owners & Professionals | Sanlam</title>
<meta name="description" content="Nikita Naidoo is a Sanlam Financial Adviser specialising in retirement annuities, tax-free investments, and life cover for business owners and professionals in South Africa. Advice is free, no obligation." />
<meta name="keywords" content="financial adviser South Africa, Sanlam financial adviser, retirement annuity South Africa, tax free savings account, life cover business owners, two-pot retirement system, financial planner professionals, TFSA 2026, key person insurance, buy sell agreement South Africa, financial planning entrepreneurs" />
<meta name="author" content="Nikita Naidoo" />
```

### 1.2 Add Open Graph and Twitter Card meta tags (after existing meta tags)

```html
<!-- Open Graph -->
<meta property="og:type" content="website" />
<meta property="og:title" content="Nikita Naidoo | Financial Adviser for Business Owners & Professionals" />
<meta property="og:description" content="Expert financial advice for business owners and professionals. Retirement annuities, tax-free investments, life cover. Advice is free, no obligation." />
<meta property="og:url" content="https://nikitatrusha.co.za" />
<meta property="og:site_name" content="Nikita Naidoo Financial Advisory" />
<meta property="og:locale" content="en_ZA" />
<meta property="og:image" content="https://nikitatrusha.co.za/nikita-naidoo.png" />

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Nikita Naidoo | Financial Adviser for Business Owners & Professionals" />
<meta name="twitter:description" content="Expert financial advice for business owners and professionals in South Africa." />
<meta name="twitter:image" content="https://nikitatrusha.co.za/nikita-naidoo.png" />
```

### 1.3 Add JSON-LD Structured Data (before closing `</head>`)

Add THREE schema blocks:

**FinancialService schema:**
```json
{
  "@context": "https://schema.org",
  "@type": "FinancialService",
  "name": "Nikita Naidoo Financial Advisory",
  "description": "Sanlam Financial Adviser specialising in retirement annuities, tax-free investments, and life cover for business owners and professionals in South Africa.",
  "url": "https://nikitatrusha.co.za",
  "telephone": "+27609812201",
  "email": "nikita.naidoo@sanlam4u.co.za",
  "areaServed": {
    "@type": "Country",
    "name": "South Africa"
  },
  "provider": {
    "@type": "Person",
    "name": "Nikita Naidoo",
    "jobTitle": "Financial Adviser",
    "worksFor": {
      "@type": "Organization",
      "name": "Sanlam"
    }
  },
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Financial Services",
    "itemListElement": [
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Retirement Annuity Planning"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Tax-Free Savings Investment"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Life Cover & Risk Protection"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Financial Needs Analysis"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Key Person Insurance"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Buy-Sell Agreement Cover"}}
    ]
  }
}
```

**Person schema:**
```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Nikita Naidoo",
  "jobTitle": "Financial Adviser",
  "description": "Sanlam Financial Adviser specialising in retirement planning, tax-free investments, and life cover for business owners and professionals. Banking Certification holder, pursuing CFP designation.",
  "worksFor": {"@type": "Organization", "name": "Sanlam"},
  "url": "https://nikitatrusha.co.za",
  "email": "nikita.naidoo@sanlam4u.co.za",
  "telephone": "+27609812201",
  "sameAs": ["https://linkedin.com/in/nikita-t-naidoo-1b14a5123"],
  "knowsAbout": ["Retirement Annuities", "Tax-Free Savings Accounts", "Life Insurance", "Two-Pot Retirement System", "Financial Planning for Business Owners", "Key Person Insurance", "Buy-Sell Agreements"]
}
```

**FAQPage schema** — Generate dynamically from the FAQ section content (see Phase 5).

### 1.4 Add canonical URL

```html
<link rel="canonical" href="https://nikitatrusha.co.za" />
```

---

## PHASE 2: HERO & NAVBAR UPDATES

### 2.1 Update navbar brand text

Change `Nikita Naidoo` to keep as-is OR use `Nikita Trusha Naidoo` — keep it as `Nikita Naidoo` since that is her professional name. Add new nav links for the new sections:

**Updated navbar links (in this order):**
1. About (`#about`)
2. Services (`#services`)
3. Products (`#products`)
4. Calculator (`#calculator`)
5. Blog (`#blog`)
6. FAQs (`#faqs`)
7. Contact (`#contact`)

### 2.2 Update hero copy to target business owners & professionals

```html
<h1>Nikita Naidoo</h1>
<p class="hero-subtitle">Financial Adviser for Business Owners & Professionals</p>
<p class="hero-description">
  Helping business owners and professionals in South Africa build lasting wealth through
  retirement annuities, tax-free investments, and comprehensive life cover.
  Expert advice — free, with no obligation.
</p>
```

Keep the two CTA buttons as-is (Book a Consultation + Call Now).

---

## PHASE 3: ENHANCED ABOUT SECTION

### 3.1 Add qualifications and credentials

After the existing about paragraph, add a credentials subsection. Keep the existing heading ("You have the opportunity to change the course of your life...") and paragraph. Add below the paragraph, before the pillars:

```html
<div class="about-credentials">
  <h3 class="credentials-title">Qualifications & Credentials</h3>
  <ul class="credentials-list">
    <li>
      <span class="credential-icon"><!-- graduation cap SVG --></span>
      <div>
        <strong>Banking Certification</strong>
        <span>Certified Banking Professional</span>
      </div>
    </li>
    <li>
      <span class="credential-icon"><!-- book/study SVG --></span>
      <div>
        <strong>Certified Financial Planner (CFP&reg;)</strong>
        <span>Currently pursuing designation</span>
      </div>
    </li>
    <li>
      <span class="credential-icon"><!-- Sanlam shield SVG --></span>
      <div>
        <strong>Sanlam Authorised Representative</strong>
        <span>Licensed Financial Services Provider</span>
      </div>
    </li>
  </ul>
</div>
```

Style credentials-list as a clean vertical list with icons, matching the existing pillar card aesthetic. Use `--blue-primary` for icons.

### 3.2 Add introduction video embed

Below the credentials, add a video section. Use a placeholder structure that accepts a video file or Loom embed:

```html
<div class="about-video reveal">
  <h3>Meet Nikita</h3>
  <div class="video-wrapper">
    <!-- VIDEO PLACEHOLDER: Replace src with actual video URL when provided -->
    <div class="video-placeholder" id="introVideo">
      <div class="video-placeholder-content">
        <svg><!-- Play button circle SVG --></svg>
        <p>Introduction video coming soon</p>
      </div>
    </div>
    <!-- When video is ready, replace the placeholder div above with:
    <video controls preload="metadata" poster="video-poster.jpg">
      <source src="nikita-intro.mp4" type="video/mp4">
    </video>
    OR for Loom:
    <iframe src="LOOM_EMBED_URL" frameborder="0" allowfullscreen></iframe>
    -->
  </div>
</div>
```

Style `video-wrapper` with:
- `aspect-ratio: 16 / 9`
- `border-radius: var(--radius-md)`
- `overflow: hidden`
- `box-shadow: var(--shadow-lg)`
- `background: var(--blue-light)`
- Max width: 100% of the about content column
- The placeholder should have a centered play icon and text on `--blue-light` background

---

## PHASE 4: PRODUCT FINDER SECTION (new section, after Services)

Create a new section `#products` between Services and Calculator. This is a product information hub for Nikita's three main product offerings, with educational content and CTAs.

### Section heading:
```
Find the Right Product for You
Compare Nikita's core product offerings to find what fits your financial goals.
```

### Three product cards (side by side on desktop, stack on mobile):

**Card 1: Retirement Annuity (RA)**
- Icon: Pie chart or retirement/savings SVG
- Title: "Retirement Annuity"
- Key points (bullet list):
  - Tax-deductible contributions up to 27.5% of income (max R350,000/year)
  - Investment growth is tax-free while invested
  - First R550,000 of retirement lump sum is tax-free
  - Two-Pot System: access 1/3 of new contributions annually
  - Protected from creditors — ideal for business owners
  - Sanlam Cumulus Echo with Wealth Bonus
- CTA button: "Calculate Your Retirement" → scrolls to `#calculator`

**Card 2: Tax-Free Savings Account (TFSA)**
- Icon: Shield with checkmark or piggy bank SVG
- Title: "Tax-Free Investment"
- Key points:
  - Zero tax on interest, dividends, and capital gains
  - R36,000 annual contribution limit (increasing to R46,000 from March 2026)
  - R500,000 lifetime contribution limit
  - Withdraw anytime — no lock-in period
  - 40% penalty on excess contributions
  - Flexible investment options via Sanlam
- CTA button: "Get Started" → scrolls to `#contact`

**Card 3: Life Cover & Risk Protection**
- Icon: Shield with heart or family SVG
- Title: "Life Cover & Business Protection"
- Key points:
  - Death cover — tax-free lump sum to beneficiaries
  - Income protection — tax-free monthly payouts
  - Key person insurance for businesses
  - Buy-sell agreement cover
  - Disability and severe illness cover
  - Sanlam Wealth Bonus and Reality programme savings
- CTA button: "Speak to Nikita" → scrolls to `#contact`

### Card styling:
- White background, `--shadow-md`, `--radius-md`
- Icon in `--blue-primary` circle at top
- Title in `--blue-primary`, 1.25rem, font-weight 700
- Bullet points with small blue checkmark SVGs
- CTA button: `.btn-primary` style (matching existing buttons)
- Hover: lift with `transform: translateY(-4px)` and `--shadow-lg`
- Grid: `grid-template-columns: repeat(auto-fit, minmax(320px, 1fr))` with gap 24px

### Fee transparency banner (below the cards):

```html
<div class="fee-transparency reveal">
  <div class="fee-icon"><!-- Handshake or open-hands SVG --></div>
  <div>
    <h3>Advice is Free, No Obligation</h3>
    <p>Nikita provides expert financial advice at no cost to you.
       There is no obligation to proceed — the consultation is yours to explore your options freely.</p>
  </div>
</div>
```

Style: light blue background (`--blue-light`), rounded corners, flex layout with icon on left, padding 32px, subtle left border in `--blue-primary`.

---

## PHASE 5: FAQ SECTION (new section, after Testimonials)

Create section `#faqs` between Testimonials and Contact.

### Section heading:
```
Frequently Asked Questions
Answers to the most common questions about financial planning in South Africa.
```

### Accordion-style FAQ items (10 questions):

Implement as clickable question headers that expand/collapse answer panels. Use a `+` / `−` toggle icon. Only one open at a time (accordion behaviour).

**Q1:** How much do I need to retire comfortably in South Africa?
**A1:** Most financial planners recommend a replacement ratio of 75% of your final salary. The amount you need depends on your lifestyle, age, and existing savings. As a general benchmark, you would need a retirement capital of roughly 15–17 times your desired annual income in retirement. Use the retirement calculator on this site to get a personalised estimate based on your specific circumstances.

**Q2:** What is the two-pot retirement system and how does it affect me?
**A2:** The two-pot retirement system, effective from 1 September 2024, splits your new retirement fund contributions into two components: a savings component (one-third) that you can access once per tax year (minimum R2,000, taxed at your marginal rate), and a retirement component (two-thirds) that remains preserved until retirement. Existing savings before September 2024 form a vested component under the old rules. If you have a retirement annuity, this applies to your new contributions going forward.

**Q3:** Is a retirement annuity worth it in 2026?
**A3:** A retirement annuity remains one of the most tax-efficient savings vehicles in South Africa. Your contributions are tax-deductible up to 27.5% of your taxable income (capped at R350,000 per year), your investment grows tax-free, and the first R550,000 of your retirement lump sum is tax-free. For business owners, RA savings are also protected from creditors — a significant advantage. With the two-pot system now in place, you also have limited access to savings if needed.

**Q4:** How much can I invest in a tax-free savings account per year?
**A4:** The current annual contribution limit is R36,000, increasing to R46,000 from March 2026 as announced in the 2026 Budget. The lifetime limit remains R500,000 across all TFSA providers. If you exceed these limits, SARS imposes a 40% penalty on the excess amount. All returns — interest, dividends, and capital gains — are completely tax-free, making TFSAs an excellent complement to a retirement annuity.

**Q5:** How much life cover do I need in South Africa?
**A5:** A common rule of thumb is 8–10 times your annual income, but the right amount depends on your debts, dependants, lifestyle costs, and existing cover. Business owners should also consider key person insurance, buy-sell agreement cover, and business overhead protection separately from personal life cover. A financial needs analysis will identify the exact amount you need.

**Q6:** What insurance does a small business need in South Africa?
**A6:** Beyond personal life cover, business owners should consider key person insurance (protects against loss of a critical team member), buy-sell agreement cover (funds the purchase of a deceased partner's share), business overhead protection (covers 6–12 months of operating costs), income protection (especially important for self-employed with no UIF), and contingent liability cover for personal sureties on business debt.

**Q7:** What is key person insurance and do I need it?
**A7:** Key person insurance provides a lump sum payout if a person critical to your business — such as a founder, director, or top salesperson — dies or becomes permanently disabled. The payout helps the business survive the financial impact of losing that person, covering costs like recruiting a replacement, lost revenue, or settling debts. If your business depends heavily on any one individual, key person insurance is essential.

**Q8:** How does a buy-sell agreement work in South Africa?
**A8:** A buy-sell agreement is a legal contract between business partners that pre-arranges the sale of a partner's share if they die, become disabled, or exit the business. It is funded by life insurance policies on each partner. When a triggering event occurs, the insurance pays out, and the surviving partners use those funds to purchase the departing partner's share at a pre-agreed valuation. The proceeds are exempt from estate duty under Section 3(3)(a)(iA) of the Estate Duty Act.

**Q9:** Can I access my retirement annuity before 55?
**A9:** Under the two-pot system (from September 2024), you can access the savings component of your RA once per tax year, with a minimum withdrawal of R2,000. This applies only to contributions made after September 2024. The withdrawal is taxed at your marginal income tax rate. The retirement component and vested component remain locked until you retire (earliest age 55). Early access beyond the savings pot is only possible through emigration (financial emigration via SARS) or if the total value is below R15,000.

**Q10:** Does financial advice cost anything?
**A10:** Nikita provides financial advice at no cost and with no obligation. As a Sanlam Financial Adviser, the consultation is free — you are under no pressure to proceed with any product or recommendation. The goal is to help you understand your options and make informed decisions about your financial future.

### FAQ JS:
```javascript
document.querySelectorAll('.faq-question').forEach(q => {
  q.addEventListener('click', () => {
    const item = q.parentElement;
    const isOpen = item.classList.contains('active');
    // Close all
    document.querySelectorAll('.faq-item').forEach(i => i.classList.remove('active'));
    // Toggle clicked
    if (!isOpen) item.classList.add('active');
  });
});
```

### FAQ CSS:
- `.faq-item`: border-bottom `1px solid #e0e0e0`, padding 0
- `.faq-question`: padding 20px 0, cursor pointer, display flex, justify-content space-between, align-items center, font-weight 600, font-size 1.05rem, color `--text-primary`
- `.faq-question::after`: content `'+'`, font-size 1.5rem, color `--blue-primary`, transition transform 0.3s
- `.faq-item.active .faq-question::after`: content `'−'`
- `.faq-answer`: max-height 0, overflow hidden, transition max-height 0.4s ease, padding 0
- `.faq-item.active .faq-answer`: max-height 500px, padding-bottom 20px
- `.faq-answer p`: color `--text-secondary`, line-height 1.8, font-size 0.95rem

### FAQPage Schema (add to head):
Generate JSON-LD `FAQPage` schema from all 10 Q&A pairs above.

---

## PHASE 6: BLOG SECTION (new section, after Calculator)

Create section `#blog` between Calculator and Testimonials.

### Section heading:
```
Financial Insights
Expert articles on retirement planning, tax-free investments, and protecting your business.
```

### Blog card grid (3 articles):

Display as a 3-column grid on desktop (stack on mobile). Each card:
- Featured image area (placeholder gradient in `--blue-light` to `--blue-primary` with article number or icon)
- Category tag (small pill badge above title)
- Article title (h3, font-weight 700)
- Excerpt (2-3 lines, `--text-secondary`)
- Read time estimate
- "Read Article" link/button
- On click: expands to full article view (see below)

---

### ARTICLE 1: "Your Business is NOT Your Retirement Plan"

**Category:** Retirement Planning
**Read time:** 8 min read
**Meta description:** Less than 6% of South Africans retire comfortably. Business owners are statistically worse off. Here are 5 moves to fix that.

**Full article content (write directly into HTML, hidden by default, shown on click):**

The article must be written in a warm, authoritative, educational tone — as if written by the domain (nikitatrusha.co.za) editorial team. Use "we" sparingly. Address the reader directly ("you", "your").

**Structure:**
1. **Opening hook** — The uncomfortable truth: less than 6% of South Africans retire comfortably (National Treasury). Business owners are statistically worse off because they reinvest everything and assume they will just sell the business.

2. **Why selling your business is a dangerous retirement strategy** — Illiquidity (finding a buyer takes 6-18 months on average), valuation gaps (what you think it's worth vs what someone will pay), capital gains tax implications (up to 18% effective rate for individuals), concentration risk (your entire retirement depends on a single asset), and the emotional difficulty of actually letting go.

3. **Five moves every business owner should make now:**
   - **Move 1: Start or increase your retirement annuity** — Tax-deductible contributions up to 27.5% of income (max R350,000). Investment growth is tax-free. RA savings are protected from creditors under the Pension Funds Act — critical for business owners with personal sureties. Sanlam's Cumulus Echo RA includes the Wealth Bonus feature.
   - **Move 2: Max out your tax-free savings account** — R36,000 annual limit (R46,000 from March 2026). Zero tax on returns. Flexible access — no lock-in. Complements the RA because it provides liquidity the RA does not.
   - **Move 3: Understand the two-pot system for your RA** — Since September 2024, new RA contributions split into savings (1/3, accessible annually) and retirement (2/3, preserved). This gives business owners a liquidity safety net within their RA.
   - **Move 4: Get a succession plan with a buy-sell agreement** — 76% of African family businesses lack succession plans (PwC). A buy-sell agreement funded by life insurance ensures your partners can buy your share at a pre-agreed price. Proceeds are exempt from estate duty.
   - **Move 5: Separate personal from business finances** — Ensure personal risk cover (life, disability, income protection) exists independently of the business. If the business fails, your family's financial security should not fail with it.

4. **Closing** — Your business is an asset, not a retirement plan. The difference between the 6% who retire comfortably and the 94% who do not is that the 6% planned separately. Speak to a financial adviser about building a retirement strategy that does not depend on a single outcome.

**Key data points to include:** Less than 6% retire comfortably, 76% lack succession plans, R350,000 RA cap, 27.5% deduction rate, two-pot split ratios, R36,000/R46,000 TFSA limits, R500,000 lifetime TFSA limit.

---

### ARTICLE 2: "The Complete Guide to Tax-Free Savings in 2026"

**Category:** Tax-Free Investments
**Read time:** 7 min read
**Meta description:** The TFSA annual limit just increased to R46,000. Here's everything you need to know to maximise your tax-free investment in 2026.

**Structure:**
1. **Opening** — The 2026 Budget increased the TFSA annual limit from R36,000 to R46,000 — the first increase in five years. What this means for your savings strategy.

2. **How TFSAs work** — No tax on interest, dividends, or capital gains. Contributions from after-tax income (no upfront deduction like an RA). Withdraw anytime with no penalties. Available from R350/month through Sanlam.

3. **The new 2026 limits explained:**
   - Annual: R46,000 (from March 2026, previously R36,000)
   - Lifetime: R500,000 (unchanged)
   - At R46,000/year, you reach the lifetime cap in approximately 10 years and 10 months
   - The limit applies across ALL TFSA providers combined

4. **Five common TFSA mistakes that cost you money:**
   - Withdrawing and losing lifetime contribution room (withdrawals do not "free up" space)
   - Over-contributing and facing the 40% SARS penalty
   - Holding only cash/money market (missing growth potential)
   - Not using the full annual limit (the unused portion does not roll over)
   - Having TFSAs at multiple providers without tracking the combined total

5. **TFSA vs Retirement Annuity — where should your money go?**
   - RA: Tax deduction upfront, locked until 55+, creditor-protected, mandatory annuitisation of 2/3
   - TFSA: No upfront deduction, fully flexible, fully tax-free on withdrawal, no annuitisation requirement
   - The optimal strategy: Max your RA deduction first (it reduces taxable income), then put the rest in a TFSA
   - For business owners: RA first (creditor protection + deduction), TFSA second (liquidity)

6. **How much could a TFSA be worth?**
   - Example: R3,000/month for 15 years at 10% nominal return → approximately R1.24 million (with only R540,000 contributed)
   - The tax saving: compared to a taxable investment at a 40% marginal rate, the TFSA saves you roughly R250,000+ in taxes over that period

7. **Closing** — The TFSA is one of the simplest wealth-building tools available in South Africa. The R46,000 limit gives you more room than ever. Whether you invest R350 or R3,833 per month, the key is to start and to be consistent.

---

### ARTICLE 3: "What Happens to Your Business If Something Happens to You?"

**Category:** Business Protection
**Read time:** 9 min read
**Meta description:** Most business owners have personal life cover but none of the business-specific protection that actually saves their company. Here's what you need.

**Structure:**
1. **Opening scenario** — Paint a vivid (but respectful) picture: two partners run a successful business. One dies unexpectedly. The surviving partner now faces the deceased's family demanding their share, creditors calling in personal sureties, key clients leaving because they dealt only with the deceased, and no cash to keep operating. This is preventable.

2. **The four types of business risk cover every owner needs:**

   **Type 1: Personal + Business life cover**
   - Personal cover protects your family (replaces your income, covers debts)
   - Business cover protects the company (separate policies with separate beneficiaries)
   - Sanlam offers the Immediate Expenses Benefit — 48-hour payout for urgent costs
   - The Wealth Bonus invests a portion of premiums, matched by Sanlam from age 70

   **Type 2: Key person insurance**
   - Covers the financial loss to the business if a critical person dies or is permanently disabled
   - Payout used for: recruitment costs, lost revenue, client retention, debt settlement
   - The business is the policyholder and beneficiary (not the individual)
   - Premiums are not tax-deductible, but the payout is tax-free

   **Type 3: Buy-sell agreement cover**
   - Legal agreement + life insurance policy on each partner
   - When a partner dies: insurance pays out, surviving partners buy the deceased's share
   - Family gets fair value in cash, business continues uninterrupted
   - Exempt from estate duty under Section 3(3)(a)(iA) of the Estate Duty Act
   - Without this: family inherits a share they cannot sell, business is paralysed

   **Type 4: Income protection (critical for self-employed)**
   - No employer sick leave, no UIF, no safety net
   - Pays a tax-free monthly income if you cannot work due to illness or injury
   - Typically covers 75% of income for a specified benefit period
   - Disability claims are the second-highest claim type in SA after death claims

3. **The statistics that should keep you up at night:**
   - 76% of African family businesses have no succession plan (PwC)
   - Only 30% of family businesses survive to the second generation
   - Only 41% of South African business owners have a valid will
   - Disability claims are the second-highest after death claims

4. **A simple action plan:**
   - Step 1: Get a financial needs analysis (free, no obligation)
   - Step 2: Ensure personal life and disability cover are in place
   - Step 3: Assess key person risk in your business
   - Step 4: Put a buy-sell agreement in place with your partners
   - Step 5: Add income protection if you are self-employed

5. **Closing** — The best time to put business protection in place is before you need it. Speak to a financial adviser who understands both personal and business risk.

---

### Blog article display implementation:

**Card view (default):** 3-column grid, each card shows image, category, title, excerpt, read time, "Read Article" button.

**Full article view (on click):** When "Read Article" is clicked:
- The blog section expands to show the full article
- Article layout: centered, max-width 720px, white background
- Title at top (h2, `--blue-primary`)
- Category pill + read time + date below title
- Body text: 1rem, line-height 1.9, `--text-primary`
- H3 subheadings: 1.25rem, font-weight 700, `--blue-dark`, margin-top 40px
- Bullet lists: custom blue dot, 0.95rem
- Statistics/callouts: light blue background box (`--blue-light`), border-left 4px `--blue-primary`, padding 20px
- Image placeholders: aspect-ratio 16/9, rounded `--radius-md`, background `--blue-light`
- "Back to Articles" link at top to return to card view
- Smooth transition between views

**Blog article JS:**
- Click "Read Article" → hide card grid, show full article, smooth scroll to top of blog section
- Click "Back to Articles" → hide article, show card grid
- Track which article is open via data attributes

**Blog CSS must include:**
- `.blog-grid`: grid, 3 columns on desktop, 1 on mobile
- `.blog-card`: white bg, shadow, radius, hover lift
- `.blog-card-image`: aspect-ratio 16/9, bg gradient placeholder
- `.blog-category`: small pill, `--blue-primary` bg, white text, font-size 0.75rem
- `.blog-article-full`: max-width 720px, margin auto, article typography
- `.blog-article-full blockquote`: left border, italic, `--blue-light` bg
- `.blog-article-full .stat-callout`: callout box for key statistics

**Article schema** — Add `Article` JSON-LD for each blog post with:
- `@type`: "Article"
- `headline`: article title
- `description`: meta description
- `author`: `{"@type": "Organization", "name": "nikitatrusha.co.za"}`
- `datePublished`: "2026-03-04"
- `publisher`: organization details

---

## PHASE 7: CALCULATOR UPDATES (2026 Budget figures)

Update the retirement calculator JavaScript to reflect 2026 Budget changes:

1. **TFSA annual limit**: Change R36,000 → R46,000 (update both the JS constant and any display text/labels)
2. **RA deduction cap**: Change R350,000 → R430,000 (update the `Math.min` calculation and display text)
3. **CGT annual exclusion**: Update to R50,000 if referenced anywhere
4. Update any text/labels in the calculator section that reference the old limits
5. Keep the 2025/2026 tax brackets as-is (they were frozen at 2024/2025 levels per the Budget)

---

## PHASE 8: CONTACT SECTION ENHANCEMENT

### 8.1 Add clear CTA above the contact form

```html
<div class="contact-cta reveal">
  <h3>Ready to Take Control of Your Finances?</h3>
  <p>Book a free consultation with Nikita. No obligation, no cost — just clear,
     personalised financial guidance for business owners and professionals.</p>
</div>
```

### 8.2 Keep existing contact form but update the submit button text

Change "Send Message" to "Book Your Free Consultation"

---

## PHASE 9: FOOTER UPDATES

### 9.1 Update footer disclaimer

```html
<p class="footer-disclaimer">
  Nikita Naidoo is an authorised Financial Services Provider representative of Sanlam Life Insurance Ltd.
  This website is for informational purposes only and does not constitute financial advice as defined in the
  Financial Advisory and Intermediary Services Act (FAIS Act, Act 37 of 2002).
  All calculators and tools provide general financial information only.
</p>
<p class="footer-copyright">
  &copy; 2026 Nikita Naidoo. All rights reserved. |
  <a href="https://nikitatrusha.co.za">nikitatrusha.co.za</a>
</p>
```

---

## PHASE 10: TECHNICAL SEO FILES (create as separate files)

### 10.1 Create `robots.txt`

```
User-agent: *
Allow: /

# AI Crawlers - explicitly allowed
User-agent: ChatGPT-User
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: Claude-Web
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /

User-agent: Amazonbot
Allow: /

Sitemap: https://nikitatrusha.co.za/sitemap.xml
```

### 10.2 Create `sitemap.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://nikitatrusha.co.za/</loc>
    <lastmod>2026-03-04</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

### 10.3 Create `llms.txt`

```
# Nikita Naidoo Financial Advisory
> Nikita Naidoo is a Sanlam Financial Adviser based in South Africa, specialising in retirement annuities, tax-free investments, and life cover for business owners and professionals.

## Services
- Retirement Annuity Planning (Sanlam Cumulus Echo)
- Tax-Free Savings Account Investment
- Life Cover and Risk Protection
- Key Person Insurance
- Buy-Sell Agreement Cover
- Financial Needs Analysis
- Income Protection

## Key Facts
- Advice is free, no obligation
- Banking Certification holder
- Pursuing Certified Financial Planner (CFP) designation
- Sanlam authorised representative
- Specialises in business owners and professionals

## Products
- Sanlam Retirement Annuity (Cumulus Echo) — tax-deductible, creditor-protected, Wealth Bonus
- Sanlam Tax-Free Investment — R46,000 annual limit (2026), R500,000 lifetime
- Sanlam Life Cover — death, disability, income protection, key person, buy-sell

## Contact
- Email: nikita.naidoo@sanlam4u.co.za
- Phone: +27 60 981 2201
- Website: https://nikitatrusha.co.za
- LinkedIn: https://linkedin.com/in/nikita-t-naidoo-1b14a5123
```

---

## PHASE 11: MOBILE RESPONSIVENESS AUDIT

Verify and enhance mobile responsiveness for ALL new sections:

1. **Products grid**: 1 column on mobile (< 768px), 2 columns on tablet, 3 on desktop
2. **Blog grid**: 1 column on mobile, 2 on tablet, 3 on desktop
3. **FAQ section**: Full width, padding adjustments for mobile
4. **Video embed**: 100% width, maintain 16:9 aspect ratio
5. **Navbar**: Ensure new nav items (Products, Blog, FAQs) fit in hamburger menu on mobile
6. **Blog article full view**: Adjust padding/margins for mobile readability
7. **Product cards**: Stack vertically with full-width CTAs on mobile
8. **Fee transparency banner**: Stack icon above text on mobile
9. **Credentials list**: Full width on mobile

Test breakpoints: 480px, 768px, 1024px, 1200px

---

## PHASE 12: FINAL SECTION ORDER

The complete section order in the HTML must be:

1. Navbar (About, Services, Products, Calculator, Blog, FAQs, Contact)
2. Hero
3. About (with credentials + video embed)
4. Services (existing 4 cards)
5. **Products** (new — 3 product cards + fee transparency)
6. Calculator (existing, updated figures)
7. **Blog** (new — 3 articles)
8. Testimonials (existing)
9. **FAQs** (new — 10 questions accordion)
10. Contact (enhanced CTA)
11. Footer (updated disclaimer)

---

## IMPLEMENTATION NOTES

- Add `.reveal` class to ALL new section containers for scroll animation (the IntersectionObserver already handles it)
- All new SVG icons should be inline (no external icon libraries) — match the style of existing SVGs (24x24, stroke-width 2, currentColor)
- Blog articles should use semantic HTML: `<article>`, `<header>`, `<section>`, `<aside>` for callouts
- Maintain the existing colour palette — no new colours
- All text must be proofread for South African English spelling (specialising, colour, behaviour, etc.)
- Ensure all new interactive elements are keyboard-accessible
- Add `aria-expanded` attributes to FAQ accordion items
- Blog "Read Article" / "Back to Articles" should use `history.pushState` to update URL hash without page reload (e.g., `#blog/article-1`)
- Test that the existing calculator still works after all changes

---

## SKILLS TO USE DURING IMPLEMENTATION

When implementing this prompt in Claude Code, consider using these skills for quality assurance:

```bash
# SEO audit after implementation
npx skills add https://github.com/coreyhaines31/marketingskills --skill seo-audit

# AI discoverability check
npx skills add https://github.com/coreyhaines31/marketingskills --skill ai-seo

# Programmatic SEO patterns
npx skills add https://github.com/coreyhaines31/marketingskills --skill programmatic-seo

# Copywriting quality
npx skills add https://github.com/coreyhaines31/marketingskills --skill copywriting

# Prompt enhancement
npx skills add https://github.com/google-labs-code/stitch-skills --skill enhance-prompt

# Embedding strategies
npx skills add https://github.com/wshobson/agents --skill embedding-strategies

# GSD workflow
npx skills add https://github.com/gsd-build/get-shit-done.git
```

---

## SUCCESS CRITERIA

After implementation, the website must:
- [ ] Load as a single `index.html` file with all CSS/JS inline
- [ ] Have all 7 navbar links working and scrolling to correct sections
- [ ] Display 3 product cards with accurate Sanlam product information
- [ ] Show 3 full blog articles accessible from card view
- [ ] Have a working 10-question FAQ accordion
- [ ] Include video embed placeholder ready for Nikita's video
- [ ] Show qualifications (Banking Cert, CFP pursuit) in About section
- [ ] State "Advice is free, no obligation" prominently
- [ ] Target "business owners and professionals" in hero and throughout
- [ ] Have JSON-LD schema for FinancialService, Person, FAQPage, and 3 Articles
- [ ] Include Open Graph and Twitter Card meta tags
- [ ] Have robots.txt, sitemap.xml, and llms.txt as separate files
- [ ] Calculator updated with 2026 Budget figures (R46k TFSA, R430k RA cap)
- [ ] Be fully responsive on mobile, tablet, and desktop
- [ ] Pass basic accessibility checks (keyboard nav, aria attributes)
- [ ] All existing functionality (calculator, contact form, animations) still works
