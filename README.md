# Every Growth Experiments

Pricing strategy experiments and A/B test specifications for Every's SaaS products.

## Overview

This repository contains Product Requirements Documents (PRDs) and interactive prototypes for pricing experiments targeting two products:

| Product | Description | Website |
|---------|-------------|---------|
| **Monologue** | Voice dictation tool | monologue.to |
| **Cora** | AI email assistant | cora.computer |

## Experiments

| Experiment | Products | Goal | Status |
|------------|----------|------|--------|
| **Price Elasticity** | Monologue | Test $120 and $150 price points (vs current $100/yr) to find revenue-maximizing price | Draft |
| **Decoy Third Tier** | Monologue, Cora | Add strategically positioned middle tier to leverage decoy effect and lift revenue per visitor | Draft |

## Repository Structure

```
Every_Growth_Experiments/
├── Monologue_Price_Elasticity/
│   ├── PRD_Monologue_Price_Elasticity.md   # Full experiment specification
│   └── proto_monologue_elasticity.html     # Interactive pricing page prototype
│
└── Decoy_Third_Tier/
    ├── PRD_Decoy_Third_Tier.md             # Full experiment specification
    ├── proto_monologue_decoy.html          # Monologue 3-tier prototype
    └── proto_cora_decoy.html               # Cora 3-tier prototype
```

## Viewing Prototypes

The HTML prototypes are self-contained files that can be opened directly in a browser:

1. Navigate to the experiment folder
2. Open the `.html` file in your browser
3. Prototypes show proposed pricing page layouts with tier comparisons

## Status

All experiments are currently **Draft — Pending Approval**.

Stakeholders: Product, Engineering, Design, Marketing, Finance
