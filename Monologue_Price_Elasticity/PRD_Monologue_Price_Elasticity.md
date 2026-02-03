# PRD: Monologue Pro Price Elasticity Experiment

| Field | Value |
|-------|-------|
| Product | Monologue (monologue.to) |
| Status | Draft — Pending Approval |
| Created | February 3, 2026 |
| Stakeholders | Product, Engineering, Marketing, Finance |

---

## 🎯 TL;DR

Monologue Pro at $100/yr matches Otter.ai and is 65% cheaper than Descript. The "Early Bird" badge signals a price increase with no timeline set. This experiment tests $120 and $150 price points with/without the badge to find the revenue-maximizing price. Even a 25% conversion drop at $150/yr still yields +12.5% revenue.

---

## ⚡ Market Position

| Product | Entry Price | vs Monologue |
|---------|-----------|-------------|
| **Monologue Pro** | $100/yr ($8.33/mo) | — |
| Otter.ai Pro | $100/yr ($8.33/mo) | Same price, different use case |
| Descript Hobbyist | $288/yr ($24/mo) | 2.9x more expensive |

**Current tiers:** Free (1,000 words/mo) → Pro ~~$144~~ $100/yr (Early Bird) → Every Bundle $30/mo

⚠️ **Anomalies found:**
- "Save $20" toggle doesn't match ~~$144~~ → $100 ($44 gap) — implies monthly ≈ $10/mo
- Bundle shows $30/mo on Monologue page, $20/mo on Cora page

---

## ❓ Questions to Answer

1. What's the max price before meaningful conversion loss?
2. Does the "Early Bird" badge drive conversions independent of price?
3. What's the optimal strikethrough anchor at each price?

---

## 📊 Success Metrics

| Metric | Target | Role |
|--------|--------|------|
| Revenue per pricing page visitor | +20%+ | **Primary KPI** |
| Free → Pro conversion rate | ≥85% of current | Guardrail |
| Annual plan adoption | No decline | Guardrail |
| 30-day new subscriber churn | ≤110% of current | Guardrail |
| Bundle adoption | Monitor only | Informational |

**Non-goals:** Free tier changes, bundle price changes, monthly/annual split testing

---

## 🔬 Phase 1: Pre-Experiment Surveys (Weeks 1-2)

### Exit Survey (at 2nd word-limit hit)

"What's the main reason you haven't upgraded to Pro?"

| If "too expensive" is... | Then... |
|--------------------------|---------|
| ≥40% | Test conservatively ($120 max) |
| <30% | Low risk, test up to $150 |
| <15% | Very low risk, test up to $180 |

### Van Westendorp (200+ free users who've hit limit)

Four questions → four curves → identify Optimal Price Point (OPP) and Point of Marginal Expensiveness (PME). Test variants should fall between OPP and PME.

---

## 🧪 Phase 2: A/B Test (Weeks 3-6+)

### Test Matrix: Price × Badge

| Variant | Price | Badge | Anchor |
|---------|-------|-------|--------|
| **Control** | $100/yr | Early Bird | ~~$144~~ |
| **A** | $120/yr | Early Bird | ~~$168~~ |
| **B** | $150/yr | Early Bird | ~~$200~~ |
| **C** | $100/yr | None | Flat price |
| **D** | $120/yr | None | Flat price |
| **E** | $150/yr | None | Flat price |

Anchor formula: price × 1.4 (rounded to nearest $4). Reduce to 3 variants (Control/B/D) if traffic insufficient.

### Parameters

| Parameter | Value |
|-----------|-------|
| Min sample | 500 conversions/variant (p<0.05, 80% power, 15% MDE) |
| Randomization | User-level (cookie), not session |
| Exclusions | Existing subscribers, prior pricing page visitors |
| Max duration | 8 weeks |
| Early stopping | Only via sequential testing framework (no peeking) |

---

## 🛠️ Implementation

| Area | Requirements |
|------|-------------|
| **Engineering** | Feature flags · 6 pricing card variants · Event tracking (`pricing_page_viewed` → `checkout_completed` → `subscription_cancelled`) · Multi-price Stripe setup · Analytics pipeline |
| **Design** | Badge-removed variant that looks intentional · Consistent strikethrough styling · Identical layout/colors/CTA across variants |
| **Analytics** | Real-time dashboard with CIs · Segmentation (source, device, country, day) · Annualized revenue projections |

---

## 👴 Grandfathering

| Segment | Policy |
|---------|--------|
| Pre-experiment subscribers | Keep $100/yr for 1 renewal, then migrate |
| Converted at $100 during test | Keep $100/yr for 1 renewal |
| Converted at higher price | Stay at their price |
| Post-experiment new users | Winning price |

Communicate 60 days before migration. Offer "renew now at $100 for one more year."

---

## ⚠️ Risks

| Risk | Mitigation |
|------|-----------|
| Conversion drops >25% | Auto-pause variant if >30% drop for 7+ days |
| Screenshot sharing (price differences) | "Early Bird" badge justifies variance; or test sequentially |
| Insufficient traffic | Reduce to 3 variants |
| Negative reviews | Grandfather existing; frame as "Early Bird ending" |

---

## ✅ Decision Framework

```
Revenue/visitor ≥120% AND conversion ≥85% AND churn ≤110%
  → Roll out winner (highest revenue/visitor if multiple qualify)

No variant meets all criteria
  → Keep $100; consider $110 or feature-based pricing

Badge removal within 5% of badged
  → Safe to retire "Early Bird"

Badge removal causes >15% drop
  → Replace with new urgency mechanism
```

---

## 💰 Revenue Impact Model (10,000 subscribers)

| Scenario | Revenue | vs Current |
|----------|---------|-----------|
| Current $100/yr | $1,000,000 | — |
| $120, -5% conversion | $1,140,000 | **+14%** |
| $120, -15% conversion | $1,020,000 | +2% |
| $150, -5% conversion | $1,425,000 | **+42.5%** |
| $150, -15% conversion | $1,275,000 | **+27.5%** |
| $150, -25% conversion | $1,125,000 | **+12.5%** |

Even worst case ($150, -25%) beats current pricing.

---

## 📅 Timeline

| Phase | Duration |
|-------|----------|
| Surveys (exit + Van Westendorp) | Weeks 1-2 |
| Analyze surveys, finalize variants | Week 3 |
| Build feature flags + pricing variants | Weeks 3-4 |
| QA (all variants, billing verification) | Week 5 |
| A/B test live | Weeks 6-14 |
| Analysis + decision | Week 14-15 |
| Rollout + grandfathering comms | Week 16 |

---

## 📎 Appendix: Competitive Positioning Post-Increase

```
$8.33/mo  Otter Pro ─────────── Monologue current
$10/mo    Monologue $120/yr ◄── Variant A
$12.50/mo Monologue $150/yr ◄── Variant B
$19.99/mo Otter Business ──────────────────
$20/mo    Cora Professional ───────────────
$24/mo    Descript Hobbyist ───────────────
$25/mo    Superhuman Starter ──────────────
```

At $150/yr, Monologue remains cheaper than every AI competitor.
