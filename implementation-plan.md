# Henhouse Spatial — Implementation Plan

## Current Phase: Phase 0/1 — Discovery + Architecture

Defining the chassis constraints, fit-out interface, and spatial contracts before building any simulation code. The platform-first model means the chassis design must be configuration-agnostic — designed around interface contracts, not around any specific fit-out.

## Epic Map

### E01-chassis-contract — Platform Specification
**Phase**: Architecture (current)
**What**: Define the chassis as a spatial contract — exterior envelope, structural grid, thermal performance targets, electrical capacity, HVAC system, and the fit-out interface (mounting points, connection points, clear dimensions). This is the "API" of the physical platform.
**Depends on**: Nothing. This is the foundation.
**Consumers**: Every fit-out config, the simulation engine, Container OS (hardware map).

### E02-time-machine-config — Time Machine Fit-Out Specification
**Phase**: Architecture (current)
**What**: Define Time Machine's spatial requirements as a fit-out configuration that consumes the chassis interface. Zone allocation, LED panel layout, acoustic treatment, electrical loads, HVAC demands, audience capacity validation. This is the most demanding config and stress-tests the chassis design.
**Depends on**: E01 (needs chassis interface to validate against)

### E03-parametric-model — Chassis Simulation Engine
**Phase**: Build
**What**: Parametric 3D model of the chassis. Change inputs (wall thickness, length, insulation type) and see cascading effects on interior dimensions, weight, R-value, cost estimates. Browser-based using Three.js.
**Depends on**: E01 (needs dimensional constraints and structural spec)

### E04-fitout-placement — Configuration Placement Engine
**Phase**: Build
**What**: Place fit-out components inside the parametric chassis. Validate clearances, weight distribution, electrical load, HVAC capacity. Detects conflicts (LED panel doesn't fit at current wall thickness, electrical load exceeds panel capacity).
**Depends on**: E01 (chassis model), E02+ (fit-out configs), E03 (simulation engine)

### E05-constraint-eval — Spatial Contract Validation
**Phase**: Build
**What**: Automated checks that validate a fit-out configuration against the chassis contract. "Does this configuration fit? Does it exceed electrical capacity? Does the HVAC handle the thermal load? Is the weight towable?" These are the spatial evals.
**Depends on**: E01, E03, E04

### E06-visualization — Interactive 3D Viewer
**Phase**: Build
**What**: Browser-based 3D viewer for the parametric model. Orbit, section cuts, dimension overlays, zone highlighting. Primarily a design review tool, not a consumer product.
**Depends on**: E03, E04

### E07-system-manifest — Container OS Export
**Phase**: Build
**What**: Export the physical system inventory (HVAC zones, electrical circuits, lighting fixtures, sensor locations) from the spatial model in a format Container OS can import as its hardware map. This bridges the spatial and software projects.
**Depends on**: E01, E04, Container OS protocol spec (from henhouse-container-os project)

### E08-adu-config — Living Unit Fit-Out Specification
**Phase**: Future
**What**: Define the living unit fit-out configuration. Simpler than Time Machine — validates that a livable space works within the chassis. Includes plumbing considerations.
**Depends on**: E01

## Dependency Graph

```
E01-chassis-contract ──────┬──────────────────────────┐
        │                  │                           │
        ▼                  ▼                           ▼
E02-time-machine    E03-parametric-model        E08-adu-config
        │                  │
        └──────┬───────────┘
               ▼
        E04-fitout-placement
               │
        ┌──────┼──────┐
        ▼      ▼      ▼
   E05-eval  E06-viz  E07-manifest
```

## Build Sequence (Near-Term)

### Phase 0/1 Builds (Architecture — Current)
```
E01-chassis-contract
  B001 — Project setup: masterplan, CLAUDE.md, implementation plan, project structure
  B002 — Exterior envelope spec: transport-legal dimensions, trailer frame constraints
  B003 — Wall assembly options: document 2-3 candidate assemblies with R-value, weight, width impact
  B004 — Structural grid: bay spacing, load paths, mounting point capacity
  B005 — HVAC system spec: capacity sizing (sized for Time Machine worst case), zone layout, duct routing
  B006 — Electrical system spec: shore power, panel sizing, circuit allocation, connection points
  B007 — Fit-out interface contract: the complete "API" — what the chassis provides to any configuration

E02-time-machine-config
  B008 — Zone allocation: entry, chamber, control, mechanical — dimensions and adjacency
  B009 — LED panel layout: panel sizing, mounting spec, clearances, within 6'8" width
  B010 — Acoustic treatment spec: isolation requirements, material options, thickness impact on clear width
  B011 — Electrical and thermal load calc: LED + compute + audio + audience heat
  B012 — Experience layout options: corridor vs. theater vs. pod — dimensional validation for each
```

### Phase 3 Builds (Implementation — Next)
```
E03-parametric-model
  B013 — Base chassis renderer: Three.js scene with parametric exterior box
  B014 — Wall assembly toggle: switch between assembly options, see interior width change
  B015 — Weight calculator: sum structural + envelope + system weights, compare to tow rating
  B016 — Thermal calculator: R-value computation from assembly, comparison to passive house targets
```

## Technology Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Simulation engine | Three.js (browser-based) | Fast iteration, shareable, no install required. Claude Code friendly. |
| Parametric logic | JavaScript | Dimensional math, constraint checking, state management — all JS-native |
| Schema format | JSON Schema | Consistent with Container OS project, runtime-validatable |
| Unit system | Millimeters (internal) | Metric is source of truth. Display converts to imperial for US context. |
| 3D format | glTF export (future) | Industry standard for downstream tools if needed |
| Testing | node:test | Built-in, zero dependencies |

## Open Design Questions

### Structural
- [ ] Wall assembly: wood stud + mineral wool vs. SIPs vs. composite panels?
- [ ] Is weight or thickness the actual binding constraint on movability?
- [ ] Roof structure: flat, low-slope, or peaked? (Affects interior height, drainage, aesthetics)
- [ ] Floor assembly: trailer deck integration, insulation below floor?
- [ ] Structural bay spacing: 16" OC, 24" OC, or non-standard?

### Systems
- [ ] HVAC type: mini-split, ducted heat pump, ERV for ventilation?
- [ ] Electrical service: 30A, 50A, or 100A shore power?
- [ ] Where does mechanical equipment live? Under floor? Dedicated zone? Exterior-mounted?

### Transport
- [ ] Trailer deck height above ground? (Determines remaining height budget for box)
- [ ] Single or dual axle?
- [ ] Tow vehicle class assumption: half-ton, three-quarter-ton, or one-ton truck?
- [ ] Tongue weight limits and weight distribution requirements

### Regulatory
- [ ] ADA requirements for commercial use (Time Machine)?
- [ ] Fire code egress for 6-10 occupancy?
- [ ] Electrical code: is this classified as an RV, a trailer, or a commercial structure?
- [ ] Which building code or standard governs? (IRC, IBC, ANSI A119.5 for park trailers?)

### Business
- [ ] Single chassis SKU for MVP? (Design to Time Machine spec, use for all configs)
- [ ] Or tiered SKUs? (Base for ADU, enhanced for Time Machine)
- [ ] Target unit cost for the chassis?
