# Current Tasks

## ▶ Resume Here (last updated 2026-06-09)

**Next build: B005 — HVAC + ERV sizing.** B001–B004 + decision D001 are done and committed (`f3f34b3`).

**Key context for B005/B006** (read `contracts/chassis-contract.md` first):
- **Weight is the tracked binding budget.** D001 resolved the weight fork: aluminum frame + FRP skins → **~5,750 lb cartridge allowance** at 14K no-CDL GVWR. HVAC (B005) and electrical (B006) equipment weights draw down this allowance — track them.
- Chassis envelope is locked: 6½" GPS-core FRP-skinned SIP walls (R-28), 8¼" roof, ~6'8" interior design width, ~10'1"–10'7" interior height.

**Two open items parked** (not blocking, but resolve before fleet build):
1. **Tow vehicle** — non-CDL now needs a truck rated ≤~12,000 lb GVWR; many 1-tons exceed that. The truck choice, not the build, is the binding no-CDL constraint.
2. **FRP fire rating** — interior thermal/ignition barrier required for occupied commercial use (regulatory check).

---

## Active Epic: E01-chassis-contract — Platform Specification

- [x] **B001** — Project setup: masterplan, CLAUDE.md, implementation plan, contracts, project structure
- [x] **B002** — Exterior envelope spec: transport-legal dimensions (8'×13'6"×30'), trailer config (gooseneck, dual axle, steel frame, 14K GVWR), height budget (standard vs low-profile deck), weight budget, CDL math, deployment modes. Output: `contracts/chassis-contract.md` exterior envelope section.
- [x] **B003** — SIP wall assembly: research SIP options (core material, thickness, skins). For each: total thickness, R-value, weight per linear foot, interior width impact, cost estimate. Output: updated `contracts/chassis-contract.md` wall assembly section.
- [x] **B004** — Structural grid: define SIP panel joint layout, load paths, wall/ceiling/floor mounting point locations and capacities. Must support Content Node LED panel weight and camera grid. Output: updated `contracts/chassis-contract.md` structural grid section.
- [ ] **B005** — HVAC + ERV system spec: size ERV (enthalpy wheel) and supplemental HVAC for Content Node worst case. Calculate total thermal load, specify equipment, zone layout, duct routing, register locations. Output: updated `contracts/chassis-contract.md` HVAC section.
- [ ] **B006** — Electrical system spec: 50A shore power, main panel, circuit allocation. Must support Content Node electrical load. Reserve space/conduit for future LiFePO4 battery bank and V2L. Output: updated `contracts/chassis-contract.md` electrical section.
- [ ] **B007** — Cartridge interface contract: compile the complete interface — clear volume, electrical connection points, HVAC registers, structural mounting grid, cable routing, entry points. Output: `contracts/cartridge-interface.md`, updated chassis contract.

## Next Epic: E02-content-node-config — Content Node Cartridge Specification

- [ ] **B008** — Zone allocation: dimensions, adjacency requirements, door/transition specs between zones. Output: updated `configs/content-node.md` zone section.
- [ ] **B009** — LED panel layout: panel sizing, mounting spec, depth budget, clearance validation against interior width. Output: updated `configs/content-node.md` LED section.
- [ ] **B010** — Acoustic treatment spec: room-within-a-room decoupling, STC targets, material options, thickness budget, combined depth impact (acoustic + LED + air gap) on clear width. Output: updated `configs/content-node.md` acoustic section.
- [ ] **B011** — Electrical and thermal load calculation: itemized watts and BTU for all Content Node components. Validates against chassis electrical and HVAC capacity. Output: updated `configs/content-node.md` load section.
- [ ] **B012** — Studio/experience layout validation: broadcast, immersive, and hybrid layouts within actual clear width (after panels + acoustic treatment). Output: updated `configs/content-node.md` layout section.

## Queued: E03-parametric-model — Chassis Simulation Engine

- [ ] **B013** — Base chassis renderer: Three.js scene with parametric exterior box (SIP panels). Inputs: length, width, height, wall thickness. Output: `simulation/src/chassis-renderer.js`
- [ ] **B014** — Wall assembly toggle: switch between SIP thickness options in the model. See interior width change in real-time. Output: updated renderer.
- [ ] **B015** — Weight calculator: sum structural + envelope + system weights, compare to tow rating. Output: `simulation/src/weight-calc.js`
- [ ] **B016** — Thermal calculator: R-value computation from SIP assembly, passive house target comparison. Output: `simulation/src/thermal-calc.js`

---

## How to Use This File

1. Find the first unchecked task
2. Read the referenced contract/config files for context
3. Complete the build
4. Mark the task as checked
5. Log the build in `builds.md`
6. Commit with `B{NNN}: description`
