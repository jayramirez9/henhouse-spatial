# Current Tasks

## ▶ Resume Here (last updated 2026-06-21)

**Next build: B007 — Cartridge interface contract.** B001–B006 + decisions D001, D002 are done. B006 (electrical) landed: 50A service formalized, priority-tiered panel, EMS load-shed scheme, future battery/V2L interface reserved. The display + power-independence exploration (2026-06-16) still gives B009 a head start and B011 a partial load basis.

**Key context for B007** (read `contracts/chassis-contract.md` — this build *compiles* the prior sections into one interface, plus the "Cartridge Interface" stub at the bottom):
- **B007 is the keystone deliverable — the "API" between chassis and cartridge.** It pulls together the now-firm provisions: clear interior volume (D002 7'2" design width × ~10'1"–10'7" height × ~28' length), the B004 structural mounting grid (Type L spline hard points, ledger heights), the B005 HVAC registers/duct envelope, and the B006 electrical connection points (10-circuit schedule, leg assignments, mechanical-zone junction). Output: new `contracts/cartridge-interface.md` + updated chassis contract.
- **Coordinate dependencies flagged across B004/B005/B006 land here.** Several values were explicitly deferred to B007: LED ledger heights + ceiling hard-point spacing (B004), register coordinates + CFM-per-register + duct routing (B005), electrical circuit *locations* at the cartridge boundary (B006). B007 fixes coordinates — but note several still depend on Content Node's zone layout (B008) and LED/acoustic depth (B009/B010), so B007 may specify *method + envelope* and leave final coords to a B008 reconciliation, as B005/B006 did.
- **The 50A power ceiling is now the headline chassis constraint** (B005+B006): ~6,450 W continuous for the cartridge after HVAC+ERV. Interface rule #1 ("cartridge must not exceed electrical capacity") should cite the tiered budget + EMS, not just a single amp number.
- **Weight is the tracked binding budget.** D001: aluminum frame + FRP skins → **~5,750 lb cartridge allowance** at 14K no-CDL GVWR. Chassis systems now firm through B006: HVAC+ERV ~280 lbs + electrical ~300 lbs. Fold the D002 +90 lb envelope adder into the subtotal at B007.
- Chassis envelope locked: **8'6" (102") exterior (D002)**, 6½" GPS-core FRP-skinned SIP walls (R-28), 8¼" roof, **~7'2" interior design width / 7'3" as-built**, ~10'1"–10'7" interior height.
- **Future battery/V2L is designed-for, not built (B006):** ATS location, 100A busbar, battery bay, V2L inlet, oversized DC conduit all reserved. If future power lifts the 9,600 W ceiling, studio load *and* HVAC rise together (B005). B007's reserved-volume callout (battery bay) should match B006.

**Explored ahead of sequence (2026-06-16) — display system → B009/B011 head start.** Captured in `configs/content-node.md` (Display Technology & Surface + Secondary "Window" Displays):
- **Primary = focal COB back wall** (wall opening ~7'2"–7'6" wide × 8' tall; 6-tile COB build ~6.75'×8'), end-mounted so depth eats abundant *length*, not scarce width. COSM wraparound is formally off the table.
- **Two display options:** COB all-in-one DVLED (e.g. Panasonic TL-55LV12AW; ~0.6–1.0 kW, ~300 lb, true blacks, lights talent — **primary bet, broadcast**) vs UST projection (e.g. Hisense PX4-PRO; ~0.4 kW, ~80 lb, ~10× cheaper — **budget fallback, audience-viewing only**). **Decision rule (Jay): >$50k display budget → commit to COB.**
- **Immersive / Time Machine installs add long-wall "window" displays** — these eat *width* ×2, so nest them inside the acoustic buildout (B010); the ≥5'6" margin assumes nesting.
- **Load basis for B011:** displays ~2 kW total ≈ ⅓ of the ~6,450 W cartridge envelope *before* compute/audio/lighting — not "free." 50A remains the binding cap.

**Five open items parked** (not blocking, but resolve before fleet build):
1. **Tow vehicle** — non-CDL needs a truck rated ≤~12,000 lb GVWR; many 1-tons exceed that. The truck choice, not the build, is the binding no-CDL constraint.
2. **FRP fire rating** — interior thermal/ignition barrier required for occupied commercial use (regulatory check).
3. **Condenser packaging** — 3-ton condenser rejects ~45,000 BTU/hr; must mount exterior (end wall/roof) or in a fully louvered bay, not a sealed mechanical room. Locks in B007.
4. **12-foot-lane / final-approach validation (D002)** — 102" width is permit-free in GA but legal only on 12'-lane roads. **Make this a go/no-go route-clearance gate in the booking workflow — confirm the final approach to a venue *before* taking a deposit**, not a post-booking surprise. If the fleet expands beyond GA-local, re-check destination-state local-road width rules. Also: **confirm GA's 102"/§ 32-6-23 basis with the GDOT permit office** (currently [ASSUMED]).
5. **102"-capable trailer (D002)** — the trailer frame *and* deck must be built to 102", not a stock 96" deck under a 102" box. Silent build trap; lock at trailer selection / B007.

---

## Active Epic: E01-chassis-contract — Platform Specification

- [x] **B001** — Project setup: masterplan, CLAUDE.md, implementation plan, contracts, project structure
- [x] **B002** — Exterior envelope spec: transport-legal dimensions (8'×13'6"×30'), trailer config (gooseneck, dual axle, steel frame, 14K GVWR), height budget (standard vs low-profile deck), weight budget, CDL math, deployment modes. Output: `contracts/chassis-contract.md` exterior envelope section.
- [x] **B003** — SIP wall assembly: research SIP options (core material, thickness, skins). For each: total thickness, R-value, weight per linear foot, interior width impact, cost estimate. Output: updated `contracts/chassis-contract.md` wall assembly section.
- [x] **B004** — Structural grid: define SIP panel joint layout, load paths, wall/ceiling/floor mounting point locations and capacities. Must support Content Node LED panel weight and camera grid. Output: updated `contracts/chassis-contract.md` structural grid section.
- [x] **B005** — HVAC + ERV system spec: sized ERV (150 cfm enthalpy wheel) + 3-ton variable-capacity mini-split for Content Node worst case. **Key finding: cooling load is power-capped by the 50A service, not the envelope — the service governs tonnage.** Total cooling load ~29,200 BTU/hr (~2.4 tons), sized to 3 tons. HVAC+ERV ~280 lbs. Zone/duct/register method defined; coords deferred to B007. Output: `contracts/chassis-contract.md` HVAC section, `configs/content-node.md` thermal load.
- [x] **B006** — Electrical system spec: 50A service (12,000 W nameplate / 9,600 W continuous), 100A-busbar main panel, 10-circuit schedule, priority-tiered load budget (HVAC+ERV reserved → ~6,450 W cartridge ceiling), EMS load-shed scheme (Container OS as load manager), reserved ATS/battery-bay/V2L for future expansion, mobile-structure grounding, ~300 lbs (under 320 budgeted), open code/AHJ regulatory item. Output: `contracts/chassis-contract.md` electrical section, `configs/content-node.md` load table.
- [ ] **B007** — Cartridge interface contract: compile the complete interface — clear volume, electrical connection points, HVAC registers, structural mounting grid, cable routing, entry points. Output: `contracts/cartridge-interface.md`, updated chassis contract.

## Next Epic: E02-content-node-config — Content Node Cartridge Specification

- [ ] **B008** — Zone allocation: dimensions, adjacency requirements, door/transition specs between zones. Output: updated `configs/content-node.md` zone section.
- [ ] **B009** — LED panel layout: panel sizing, mounting spec, depth budget, clearance validation against interior width. **Head start (2026-06-16): display tech + surface direction already captured** in `configs/content-node.md` (COB back wall, long-wall windows, COB-vs-projection decision rule) — B009 finalizes sizing/qty/mounting coords against it. Output: updated `configs/content-node.md` LED section.
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
