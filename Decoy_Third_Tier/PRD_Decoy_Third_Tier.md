# PRD: Decoy Third Tier Pricing Experiment (Monologue + Cora)

| Field | Value |
|-------|-------|
| Products | Monologue (monologue.to) + Cora (cora.computer) |
| Status | Draft — Pending Approval |
| Created | February 3, 2026 |
| Stakeholders | Product, Engineering, Design, Marketing, Finance |

---

## 🎯 TL;DR

Monologue and Cora both use 2-tier pricing. Every competitor uses 3+. Adding a strategically positioned third tier (decoy effect) typically lifts revenue per visitor 15-30% in SaaS. For Monologue, a "Plus" tier at $60/yr makes Pro ($100/yr) look like a bargain. For Cora, a "Starter" tier at $12/mo makes Professional ($20/mo) a no-brainer. Even worst-case modeling shows +7% revenue for Monologue.

---

## ⚡ The Gap

| Product | Current Structure | Problem |
|---------|------------------|---------|
| **Monologue** | Free ($0) → Pro ($100/yr) | $100 jump with no middle ground |
| **Cora** | Professional ($20/mo) → Unlimited ($39/mo) | Only 1 differentiating feature for +95% premium; no entry tier |

**Competitors all use 3+ tiers:** Otter (4), Descript (5), Superhuman (3), Shortwave (4), SaneBox (3)

---

## 📊 Success Metrics

| Metric | Target | Role |
|--------|--------|------|
| Revenue per pricing page visitor | +15% min | **Primary KPI** |
| Target tier conversion (Pro / Professional) | ≥90% of current | Guardrail |
| Total paid conversion | +10% min | Expansion metric |
| Tier distribution | See below | Diagnostic |

### Target Tier Distribution

| | Free/Bounce | New Tier | Target Tier | Top Tier |
|---|:-:|:-:|:-:|:-:|
| **Monologue current** | 70% | — | 30% | — |
| **Monologue target** | 55-60% | 10-15% (Plus) | 25-35% (Pro) | — |
| **Cora current** | 80% | — | 15% | 5% |
| **Cora target** | 70-75% | 8-12% (Starter) | 12-18% (Professional) | 4-6% (Unlimited) |

**Non-goals:** Changing existing tier prices, pricing page redesign, bundle changes

---

## 🆕 Proposed New Tiers

### Monologue — "Plus" ($60/yr)

| | Free | **Plus (NEW)** | Pro |
|---|:-:|:-:|:-:|
| **Price** | $0 | $60/yr ($5/mo) | $100/yr ($8.33/mo) |
| **Words/mo** | 1,000 | 10,000 | Unlimited |
| **Usage meter** | — | ✓ | — |
| **Priority processing** | — | — | ✓ |
| **Badge** | — | — | ★ Recommended |

**Why it works:** 10,000 words ≈ 67 min/mo (~3 min/day) — enough for casual, constraining for daily users. "Only $40 more for unlimited" makes Pro the obvious choice.

### Cora — "Starter" ($12/mo)

| | **Starter (NEW)** | Professional | Unlimited |
|---|:-:|:-:|:-:|
| **Price** | $12/mo | $20/mo | $39/mo |
| **Email accounts** | 1 | 2 | Unlimited |
| **AI organize + briefs** | ✓ | ✓ | ✓ |
| **Pre-drafted responses** | — | ✓ | ✓ |
| **Support** | Self-serve | ✓ | ✓ |
| **Badge** | — | ★ Most Popular | — |

**Why it works:** Starter = "AI reads for you" / Professional = "AI reads AND writes for you." $8 more for AI drafting + support = no-brainer upgrade.

---

## 🛡️ Anti-Cannibalization

### Monologue (prevent Plus eating Pro)

| Mechanism | Detail |
|-----------|--------|
| Usage meter | "7,200 / 10,000 words used this month" progress bar |
| 80% nudge | "Running low — upgrade to Pro for $3.33/mo more" |
| Monthly reset email | "Last month: 9,400/10,000 words. Never worry about limits with Pro." |
| Feature tease | "Priority processing" grayed out: "Available on Pro" |

### Cora (prevent Starter eating Professional)

| Mechanism | Detail |
|-----------|--------|
| Draft teaser | Show what AI *would* have drafted (blurred/preview), with upgrade CTA |
| Support gate | "Upgrade to Professional for direct support" |
| Account hard limit | 1 account — multi-account users must upgrade |

### 🚨 Kill-Switch Alerts

| Trigger | Check | Action |
|---------|-------|--------|
| Target tier share drops >20% | Day 7, 14, 21 | Pause experiment |
| New tier >25% of all paid | Day 14 | Review pricing/features |
| Revenue per visitor drops | Day 7 | Immediate review; possible kill |

---

## 🧪 Experiment Design

| Parameter | Detail |
|-----------|--------|
| Type | A/B test (50/50) — 2-tier control vs 3-tier variant |
| Randomization | User-level (cookie + account ID) |
| Products | Independent experiments on each product |
| Min sample | 2,000 per variant per product |
| Stats | Two-sided, p<0.05, 80% power, 15% MDE |

### Events to Track

**Both products:** `pricing_page_viewed` · `tier_card_clicked` · `checkout_started` · `checkout_completed` · `subscription_cancelled` · `tier_upgrade`

**Monologue-specific:** `word_limit_reached` · `upgrade_nudge_shown/clicked`

**Cora-specific:** `draft_teaser_shown` · `draft_teaser_upgrade_clicked` · `support_upgrade_prompt_shown`

---

## 🛠️ Implementation

| Area | Monologue | Cora |
|------|-----------|------|
| **Billing** | Plus plan ($60/yr, 10K word cap) | Starter plan ($12/mo, 1 account) |
| **Feature gating** | Word counter + usage meter + nudges | AI draft disable + teaser + support routing |
| **Pricing page** | 3-column layout, Pro = "Recommended" | 3-column layout, Professional = "Most Popular" |
| **Mobile** | Stacked: Pro first → Plus → Free | Stacked: Professional first → Starter → Unlimited |
| **Feature flag** | A/B assignment + persistence | A/B assignment + persistence |

---

## 💰 Scenario Modeling

### Monologue (10K monthly visitors, 30% current conversion)

| Scenario | Plus | Pro | Revenue | vs Current |
|----------|------|-----|---------|-----------|
| **Current** | — | 30% | $25,000/mo | — |
| Decoy works | 15% | 30% | $32,500 | **+30%** |
| Decoy + Pro uplift | 12% | 38% | $37,667 | **+51%** |
| Decoy cannibalizes | 25% | 25% | $33,333 | **+33%** |
| Worst case | 20% | 20% | $26,667 | **+7%** |

⬆️ Even worst case is positive — new tier captures users who'd otherwise stay free.

### Cora (5K monthly visitors, 20% current conversion)

| Scenario | Starter | Professional | Unlimited | Revenue | vs Current |
|----------|---------|-------------|-----------|---------|-----------|
| **Current** | — | 16% | 4% | $23,800/mo | — |
| Decoy works | 10% | 14% | 4% | $24,800 | **+4%** |
| Decoy + Pro uplift | 8% | 18% | 4% | $26,480 | **+11%** |
| Full cannibalization | 12% | 10% | 3% | $19,850 | **-17%** |

⚠️ Cora has downside risk — anti-cannibalization safeguards are critical. Only offer Starter to NEW users initially.

---

## ⚠️ Risks

| Risk | Mitigation |
|------|-----------|
| New tier cannibalizes target | Feature gating + real-time alerts + kill switch |
| Decision fatigue (3 options) | "Recommended" / "Most Popular" badge |
| Existing Cora users downgrade | Starter only for new users initially |
| Mobile layout breaks | Thorough QA; fallback to 2-tier on mobile |

---

## ✅ Decision Framework

```
Revenue/visitor ≥115% AND target tier ≥90%
  → Roll out 3-tier permanently

Revenue up but target tier drops >15%
  → Raise new tier (Plus→$75, Starter→$15) or cut features

Revenue flat (±5%)
  → Try different price points or stronger differentiation

Revenue drops >10%
  → Kill. Revert to 2-tier. Diagnose cause.
```

---

## 📅 Timeline

| Phase | Duration |
|-------|----------|
| Design: 3-tier mockups (desktop + mobile) | Week 1 |
| Billing: new plan setup | Week 2 |
| Feature gating (word counter / AI draft gate) | Weeks 2-3 |
| Pricing page variant + feature flags | Week 3 |
| QA: all variants, both platforms | Week 4 |
| A/B test live | Week 5 |
| Monitor (weekly + cannibalization alerts) | Weeks 5-9 |
| Analysis + decision | Week 10 |
| Rollout | Week 11 |

Both can run simultaneously (different products), but stagger by 2 weeks if significant user overlap via Every bundle.

---

## 📎 Appendix: References

1. Huber, Payne & Puto (1982) — "Adding Asymmetrically Dominated Alternatives"
2. Ariely — *Predictably Irrational* (2008), Chapter 1
3. ProfitWell — "The Psychology of SaaS Pricing Pages"
4. Price Intelligently — "Three-Tier Pricing: Why It Works"
