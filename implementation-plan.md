# Henhouse Spatial — Implementation Plan

## Current Phase: Phase 0/1 — Discovery + Architecture

Defining the chassis constraints, cartridge interface, and spatial contracts before building any simulation code. The platform-first model means the chassis design must be configuration-agnostic — designed around interface contracts, not around any specific cartridge.

## Epic Map

### E01-chassis-contract — Platform Specification
**Phase**: Architecture (current)
**What**: Define the chassis as a spatial contract — exterior envelope, SIP wall assembly, structural grid, thermal performance targets, electrical capacity (50A shore power + future battery expansion), ERV + HVAC system, deployment modes (trailer-locked + crane-off via ISO castings), and the cartridge interface. This is the "API" of the physical platform.
**Depends on**: Nothing. This is the foundation.
**Consumers**: Every cartridge config, the simulation engine, Container OS (hardware map).

### E02-content-node-config — Content Node Cartridge Specification
**Phase**: Architecture (current)
**What**: Define Content Node (mobile studio) as the most demanding cartridge. Zone allocation, LED panel layout, acoustic decoupling, electrical loads, HVAC demands, audience capacity validation. This stress-tests the chassis design.
**Depends on**: E01 (needs chassis interface to validate against)

### E03-parametric-model — Chassis Simulation Engine
**Phase**: Build
**What**: Parametric 3D model of the chassis. Change inputs (SIP thickness, length) and see cascading effects on interior dimensions, weight, R-value, cost estimates. Browser-based using Three.js.
**Depends on**: E01 (needs dimensional constraints and structural spec)

### E04-cartridge-placement — Configuration Placement Engine
**Phase**: Build
**What**: Place cartridge components inside the parametric chassis. Validate clearances, weight distribution, electrical load, HVAC capacity. Detects conflicts (LED panel doesn't fit at current wall thickness, electrical load exceeds panel capacity).
**Depends on**: E01 (chassis model), E02+ (cartridge configs), E03 (simulation engine)

### E05-constraint-eval — Spatial Contract Validation
**Phase**: Build
**What**: Automated checks that validate a cartridge configuration against the chassis contract. "Does this configuration fit? Does it exceed electrical capacity? Does the HVAC handle the thermal load? Is the weight towable?" These are the spatial evals.
**Depends on**: E01, E03, E04

### E06-visualization — Interactive 3D Viewer
**Phase**: Build
**What**: Browser-based 3D viewer for the parametric model. Orbit, section cuts, dimension overlays, zone highlighting. Primarily a design review tool, not a consumer product.
**Depends on**: E03, E04

### E07-system-manifest — Container OS Export
**Phase**: Build
**What**: Export the physical system inventory (HVAC zones, ERV config, electrical circuits, lighting fixtures, sensor locations) from the spatial model in a format Container OS can import as its hardware map. This bridges the spatial and software projects.
**Depends on**: E01, E04, Container OS protocol spec (from henhouse-container-os project)

### E08-sanctuary-config — Sanctuary Cartridge Specification
**Phase**: Future
**What**: Define the Sanctuary (green room) cartridge. Simpler than Content Node — validates that a luxury recovery/prep space works within the chassis.
**Depends on**: E01

### E09-sportsbook-config — Pop-Up Sportsbook Cartridge Specification
**Phase**: Future
**What**: Define the Pop-Up Sportsbook (event bar) cartridge. Includes deferred gull-wing wall design.
**Depends on**: E01

### E10-lounge-config — Heavy-Air Lounge Cartridge Specification
**Phase**: Future
**What**: Define the Heavy-Air Lounge (cigar club) cartridge. Negative-pressure HVAC design, HEPA/carbon filtration integration.
**Depends on**: E01

## Dependency Graph

```
E01-chassis-contract ──────┬──────────────────────────┐──────────┐──────────┐
        │                  │                           │          │          │
        ▼                  ▼                           ▼          ▼          ▼
E02-content-node    E03-parametric-model        E08-sanctuary E09-sports E10-lounge
        │                  │
        └──────┬───────────┘
               ▼
        E04-cartridge-placement
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
  B003 — SIP wall assembly: panel options (core material, thickness, skins), R-value, weight, width impact
  B004 — Structural grid: bay spacing (SIP joint layout), load paths, mounting point capacity
  B005 — HVAC + ERV system spec: enthalpy wheel ERV, cooling capacity (sized for Content Node), zone layout
  B006 — Electrical system spec: 50A shore power, panel sizing, circuit allocation, future battery expansion
  B007 — Cartridge interface contract: the complete "API" — what the chassis provides to any configuration

E02-content-node-config
  B008 — Zone allocation: entry, studio/chamber, control, mechanical — dimensions and adjacency
  B009 — LED panel layout: panel sizing, mounting spec, clearances, within 7'2" width (D002)
  B010 — Acoustic treatment spec: room-within-a-room decoupling, isolation requirements, thickness impact
  B011 — Electrical and thermal load calc: LED + compute + audio + audience heat
  B012 — Experience/studio layout options: broadcast, immersive, hybrid — dimensional validation
```

### Phase 3 Builds (Implementation — Next)
```
E03-parametric-model
  B013 — Base chassis renderer: Three.js scene with parametric exterior box (SIP panels)
  B014 — Wall assembly toggle: switch between SIP thicknesses, see interior width change
  B015 — Weight calculator: sum structural + envelope + system weights, compare to tow rating
  B016 — Thermal calculator: R-value computation from SIP assembly, passive house target comparison
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
- [ ] SIP core material: EPS vs polyisocyanurate vs XPS?
- [ ] SIP thickness: 4" vs 4.5" vs 6"? (R-value vs interior width tradeoff)
- [ ] SIP skin material: OSB (standard) vs metal vs fiberglass?
- [ ] Roof structure: flat, low-slope, or peaked? (Affects interior height, drainage, aesthetics)
- [ ] Floor assembly: integration with trailer deck, insulation below floor?

### Systems
- [ ] HVAC type beyond ERV: mini-split, ducted heat pump?
- [ ] ERV model/capacity: which enthalpy wheel unit?
- [ ] Where does mechanical equipment live? Under floor? Dedicated zone? Exterior-mounted?
- [ ] Battery bank space reservation: how much floor volume?

### Transport
- [ ] Trailer deck height above ground? (Determines remaining height budget for box)
- [ ] Single or dual axle?
- [ ] Tow vehicle class assumption: 3/4-ton or 1-ton truck?
- [ ] Tongue weight limits and weight distribution requirements

### Regulatory
- [ ] ADA requirements for commercial use?
- [ ] Fire code egress for occupied commercial space?
- [ ] Electrical code classification: RV, trailer, or commercial structure?
- [ ] Which building code governs? (IRC, IBC, ANSI A119.5, NFPA 501C?)

### Business
- [ ] Which cartridge first? Content Node, Sanctuary, Sportsbook, or Lounge?
- [ ] Target unit cost for chassis?
- [ ] Target rental price point per cartridge?
