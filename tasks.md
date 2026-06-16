# Current Tasks

## ▶ Resume Here (last updated 2026-06-16)

**Next build: B006 — Electrical system spec.** B001–B005 + decision D001 are done. B005 (HVAC + ERV) just landed.

**Key context for B006** (read `contracts/chassis-contract.md` HVAC + electrical sections first):
- **🔑 B005 surfaced a binding cross-constraint the electrical spec must honor: the 50A service is the governor on the studio's thermal output.** A 50A/240V service = **9,600 W continuous** (NEC 80%). HVAC compressor ~3,000 W + ERV ~150 W reserve ~3,150 W, leaving **~6,450 W continuous for the entire cartridge**. B006 must allocate the panel so HVAC/ERV draw is reserved *before* the cartridge circuits, and flag that 50A — not HVAC tonnage — caps how bright/loud Content Node can run. (B011 itemizes the cartridge against this.)
- **Weight is the tracked binding budget.** D001: aluminum frame + FRP skins → **~5,750 lb cartridge allowance** at 14K no-CDL GVWR. HVAC+ERV firmed at **~280 lbs**; ~320 lbs budgeted for electrical (panel/wiring/conduit) — track B006 against it.
- Chassis envelope locked: 6½" GPS-core FRP-skinned SIP walls (R-28), 8¼" roof, ~6'8" interior design width, ~10'1"–10'7" interior height.
- Reserve panel space/conduit for the **future battery bank + V2L** (designed-for). Note in B006: if future power lifts the 9,600 W ceiling, both the studio load *and* the HVAC requirement rise together (B005).

**Three open items parked** (not blocking, but resolve before fleet build):
1. **Tow vehicle** — non-CDL needs a truck rated ≤~12,000 lb GVWR; many 1-tons exceed that. The truck choice, not the build, is the binding no-CDL constraint.
2. **FRP fire rating** — interior thermal/ignition barrier required for occupied commercial use (regulatory check).
3. **Condenser packaging** — 3-ton condenser rejects ~45,000 BTU/hr; must mount exterior (end wall/roof) or in a fully louvered bay, not a sealed mechanical room. Locks in B007.

---

## Active Epic: E01-chassis-contract — Platform Specification

- [x] **B001** — Project setup: masterplan, CLAUDE.md, implementation plan, contracts, project structure
- [x] **B002** — Exterior envelope spec: transport-legal dimensions (8'×13'6"×30'), trailer config (gooseneck, dual axle, steel frame, 14K GVWR), height budget (standard vs low-profile deck), weight budget, CDL math, deployment modes. Output: `contracts/chassis-contract.md` exterior envelope section.
- [x] **B003** — SIP wall assembly: research SIP options (core material, thickness, skins). For each: total thickness, R-value, weight per linear foot, interior width impact, cost estimate. Output: updated `contracts/chassis-contract.md` wall assembly section.
- [x] **B004** — Structural grid: define SIP panel joint layout, load paths, wall/ceiling/floor mounting point locations and capacities. Must support Content Node LED panel weight and camera grid. Output: updated `contracts/chassis-contract.md` structural grid section.
- [x] **B005** — HVAC + ERV system spec: sized ERV (150 cfm enthalpy wheel) + 3-ton variable-capacity mini-split for Content Node worst case. **Key finding: cooling load is power-capped by the 50A service, not the envelope — the service governs tonnage.** Total cooling load ~29,200 BTU/hr (~2.4 tons), sized to 3 tons. HVAC+ERV ~280 lbs. Zone/duct/register method defined; coords deferred to B007. Output: `contracts/chassis-contract.md` HVAC section, `configs/content-node.md` thermal load.
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
