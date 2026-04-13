# Monte Carlo Assumptions — Palm Oil / Substitution Impossibility

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $68.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 6.3 | Confirmed by N=100,000 draws |
| ΔW median (result) | $428.3B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_carbon_climate` | lognormal | $81.2B | $147.6B | $243.5B | Peatland drainage CO₂, land-use change. Indonesia/Malaysia fires. Sources: Carls |
| `C2_biodiversity_habitat` | lognormal | $58.0B | $105.4B | $173.9B | Orangutan/tiger/elephant habitat destruction. Sources: IUCN, WWF, Gaveau et al. |
| `C3_health_haze` | lognormal | $46.4B | $84.3B | $139.1B | Transboundary haze, 100K+ deaths in 2015. Sources: Koplitz et al. 2016, ASEAN. |
| `C4_labor_exploitation` | normal | $50.6B | $63.2B | $75.8B | Forced/child labor on plantations. Sources: Amnesty International, DOL. |
| `C5_governance_certification_failure` | normal | $16.9B | $21.1B | $25.3B | RSPO inadequacy, greenwashing. Sources: EIA, Greenpeace. |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 3.4 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 3.4) = 0.0260%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 6.2 | 20% DC adj = 4.96 | 40% DC adj = 3.72

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $428B = 0.4% of world GDP ($106T) ✓
- **β_W range**: 6.3 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
