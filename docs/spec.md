# NCS Field Production Benchmark - Project Specification

*A decline and performance benchmarking dashboard for Norwegian Continental Shelf oil & gas fields, built in Power BI on open regulatory data.*

> **Status:** Draft v0.1 · **Owner:** Alli Mariam · **Last updated:** _27/06/2026_

---

## 1. What is the goal of this report?

To build a decision-support dashboard that shows **which producing fields on the Norwegian Continental Shelf (NCS) are declining fastest, and which operators manage that decline best**, so that an asset team can see at a glance where production performance is weakening and where attention or investment is most warranted.
The goal is to aid a *decision*, not just a reporting dashboard. Everything below exists to support that one question.

## 2. What are the objectives?

1. Rank NCS fields by rate of production decline, adjusted for field size.
2. Quantify each operator's portfolio-level production trend (so operators can be compared, not just fields).
3. Identify fields producing below their recent trend ("watch list" candidates).
4. Show each field's contribution to total NCS production over time.
5. Deliver all of this as a single interactive, filterable Power BI report backed by a clean, documented data model.

## 3. Requirements of this report?

### 3.1 Functional - what the project will do

- Load three open Sodir datasets: monthly field production, the field overview/master table, and field outline geometry.
- Transform and model the data into a **star schema**: one production fact table joined to Field, Operator/Area, and Date dimensions.
- Compute, in DAX:
  - cumulative production per field,
  - a decline-rate measure (e.g. annualised change in oil production over a trailing window),
  - each field's share of total NCS production,
  - a composite **ranking ("watch") score** combining decline steepness and field size.
- Provide interactive slicers by **operator, area, and field status** (producing / shut down).
- Present the results across report pages: an NCS overview, a single-field detail view, an operator comparison, and a map of field locations.
- *(Conditional)* If field-level produced-water volumes are usable, add a water-share trend as an additional decline signal - to be confirmed during data profiling.

### 3.2 Non-functional - quality rules

- **Reproducible:** the whole report can be rebuilt from the raw open files, with the download steps documented.
- **Open data only:** uses solely NLOD-licensed Sodir data, so it can be published freely.
- **Documented:** data sources, model, and key measures are explained in the repo README.

## 4. Scope of the report

### In scope
- Field-level production performance across the NCS.
- Historical and current production trends, decline, and operator benchmarking.

### Out of scope
- Per-well analysis or intervention modelling (the data is field-level, not per-well).
- Forecasting future production (a possible v2).
- Economic / cost / revenue modelling.

Naming what the project deliberately *excludes* is as important as naming what it does, as it keeps the build focused and the conclusions honest.

## 5. Impact & relevance

The NCS is a mature basin where managing production decline and allocating limited capital across an ageing portfolio is a live commercial problem. A tool that surfaces *where* decline is steepest and *which operators* manage it well speaks directly to capital-discipline decisions that operators and energy-intelligence firms make constantly.

## 6. Approach

A staged, documented build, each stage committed to the repo:

1. **Spec** - this document.
2. **Data acquisition** - download the Sodir tables; record source, table names, date, and licence.
3. **Data profiling** - inspect each file's columns, coverage, and quirks before modelling.
4. **Data modelling** - clean in Power Query; build the star schema and relationships.
5. **Metrics** - author the DAX measures, including the ranking score.
6. **Dashboard** - build the report pages and interactivity.
7. **Insight & recommendation** - write up what the data shows and where to focus.
8. **Documentation & publish** - README, screenshots, and a short public write-up.

**Tools:** Power BI Desktop (Power Query for transformation, DAX for measures, a Python visual for decline-curve fitting). 

**Data:** Norwegian Offshore Directorate (Sodir) FactPages - monthly field production, field overview, and field outlines

## 7. Success criteria

- The report answers the core question without further explanation needed.
- It rebuilds cleanly from the raw open files.
- The repo includes a clear README and a one-paragraph recommendation a non-technical reader can follow.

---

### Data sources

| Dataset | Use | Source |
|---|---|---|
| Field production, monthly | Fact table (volumes over time) | factpages.sodir.no → Field → Production |
| Field overview | Field dimension (operator, area, status) | factpages.sodir.no → Field |
| Field outlines (CSV, WKT geometry) | Map | factpages.sodir.no/downloads/csv/fldArea.zip |

Licence: Norwegian Licence for Open Government Data (NLOD 2.0).
