# SAPM Monte Carlo — Palm Oil / Substitution Impossibility

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Palm Oil (Substitution Impossibility).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **6.3** |
| β_W mean | 6.43 |
| β_W std | 1.26 |
| **90% CI** | **[4.6, 8.7]** |
| 99% CI | [4.1, 10.0] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$428.3B/yr** |
| Π (revenue) | $68.0B/yr |

**β_W = 6.3** means the palm oil industry destroys **$6.3 in system
welfare for every $1.00 in revenue** — across 5 channels and 100,000 Monte Carlo draws.

**Classification**: Class 1 — Impossibility

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-palm-oil.git
cd sapm-mc-palm-oil
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 6.3` and `ΔW median : $428.3B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_carbon_climate | $147.4B | [$89.3B, $242.4B] | Lognormal |
| C2_biodiversity_habitat | $105.3B | [$63.9B, $174.0B] | Lognormal |
| C3_health_haze | $84.2B | [$51.0B, $138.9B] | Lognormal |
| C4_labor_exploitation | $63.2B | [$50.6B, $75.8B] | Normal |
| C5_governance_certification_failure | $21.1B | [$16.9B, $25.3B] | Normal |
| **Total ΔW** | **$428.3B** | **[$313.7B, $592.1B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 3.4 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0260%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Palm Oil (Substitution Impossibility)*.
> GitHub: epostnieks/sapm-mc-palm-oil.
> https://github.com/epostnieks/sapm-mc-palm-oil
