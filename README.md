# NCS Field Production Benchmark

Benchmarking production decline across Norwegian Continental Shelf (NCS) oil & gas fields — and the operators that run them — using open regulatory data.

> **The question this answers:** Across the producing fields on the Norwegian shelf, which are declining fastest, and which operators manage that decline best — so where should attention and capital go?

## Why it matters

The NCS is a mature basin. Managing production decline across an ageing portfolio of fields is a constant capital-allocation decision for operators and the firms that analyse them. This project turns the Norwegian Offshore Directorate's open production records into a decision tool that surfaces *where* output is weakening and *who* is managing decline well.

## What it does

- Ranks fields by **size-weighted decline rate** (a big field declining fast matters more than a small one)
- Compares **operators** by portfolio-level production trend
- Flags fields producing **below their recent trend** — a watch list
- Maps field locations and each field's contribution to total NCS output

## Data & tools

- **Data:** Norwegian Offshore Directorate (Sodir) FactPages — monthly field production, field overview, and field outlines. Published under the Norwegian Licence for Open Government Data (NLOD 2.0).
- **Tools:** Power BI (Power Query for transformation, DAX for measures), with Python for decline-curve fitting.

## Status

🚧 **In active development**, built in documented stages. The full goal, scope, requirements, and approach are in the [project specification »](docs/SPEC.md)

## Repository structure

```
.
├── README.md          # you are here
├── docs/
│   └── SPEC.md        # project specification (Stage 1)
├── data/
│   └── README.md      # data sources & download steps (no raw files committed)
├── analysis/          # profiling notes & Python (decline-curve fit)
├── powerbi/           # the .pbix report
└── images/            # dashboard screenshots
```

---

*Built by [Alli Mariam](https://github.com/AlliMariam). Part of a series of projects on data-driven decision-making in asset-intensive industries.*
