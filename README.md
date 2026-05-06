
# Peace Capital — Quant Pricer "EmA"

Production-grade pricer for monetary (SOFR/IRS/swaptions) and credit (CDS) derivatives.
Aims for parity with industry oracles (QuantLib, ISDA, Bloomberg) before adding exotics.

## Layout

```
Peace Capital/
├── harness/              # Validation harness — the source of trust
│   ├── catalog/          # Reference trades (YAML), one per file
│   ├── market_data/      # Frozen market snapshots (curves, vols, spreads)
│   ├── oracles/          # Reference pricers (QuantLib, ISDA, academic)
│   ├── tolerances.yaml   # Acceptable PV/Greek error per instrument class
│   ├── runner.py         # Loads catalog, runs candidate + oracle, reports diffs
│   └── report.py         # Pass/fail report (HTML + JSON)
├── pricers/              # In-house pricers (port BS+MC, IRS, CDS here)
├── reports/              # Output reports from harness runs
└── tests/                # Unit/smoke tests
```

## Day 1 status

- 3 seed reference trades (IRS, swaption, CDS)
- QuantLib oracle wired up
- Runner produces pass/fail report
- Smoke test: QuantLib-vs-QuantLib (sanity check on plumbing)

## Run

```bash
cd "Peace Capital"
python3 -m harness.runner
```

## Roadmap to TaaS-grade

1. ~50 reference trades covering vanilla rates + credit
2. Port in-house pricers, identify gaps vs. oracle
3. Multi-curve bootstrap (OIS-discounting)
4. Stochastic models (Hull-White, G2++, CIR intensity)
5. Exotics + XVA (where in-house earns its premium over Bloomberg)
6. REST/Python SDK + audit trail
