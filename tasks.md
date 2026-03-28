# Current Tasks

## Active Epic: E01-chassis-contract — Platform Specification

- [x] **B001** — Project setup: masterplan, CLAUDE.md, implementation plan, contracts, project structure
- [ ] **B002** — Exterior envelope spec: document transport-legal dimensions, trailer frame constraints, height budget calculation (total height minus deck height = box height). Output: updated `contracts/chassis-contract.md` exterior envelope section.
- [ ] **B003** — Wall assembly options: research and document 2-3 candidate wall assemblies. For each: total thickness, R-value, weight per linear foot, interior width impact, material cost estimate, buildability notes. Output: updated `contracts/chassis-contract.md` wall assembly section.
- [ ] **B004** — Structural grid: define bay spacing, load paths, wall/ceiling/floor mounting point locations and capacities. Must support Time Machine LED panel weight. Output: updated `contracts/chassis-contract.md` structural grid section.
- [ ] **B005** — HVAC system spec: size for Time Machine worst case. Calculate total thermal load, specify equipment type, zone layout, duct routing, register locations. Output: updated `contracts/chassis-contract.md` HVAC section.
- [ ] **B006** — Electrical system spec: shore power sizing, main panel, circuit allocation. Must support Time Machine electrical load. Output: updated `contracts/chassis-contract.md` electrical section.
- [ ] **B007** — Fit-out interface contract: compile the complete interface — clear volume, electrical connection points, HVAC registers, structural mounting grid, cable routing, entry points. Output: `contracts/fitout-interface.md`, updated chassis contract.

## Next Epic: E02-time-machine-config — Time Machine Fit-Out Specification

- [ ] **B008** — Zone allocation: dimensions, adjacency requirements, door/transition specs between zones. Output: updated `configs/time-machine.md` zone section.
- [ ] **B009** — LED panel layout: panel sizing, mounting spec, depth budget, clearance validation against interior width. Output: updated `configs/time-machine.md` LED section.
- [ ] **B010** — Acoustic treatment spec: STC targets, material options, thickness budget, combined depth impact (acoustic + LED + air gap) on clear width. Output: updated `configs/time-machine.md` acoustic section.
- [ ] **B011** — Electrical and thermal load calculation: itemized watts and BTU for all Time Machine components. Validates against chassis electrical and HVAC capacity. Output: updated `configs/time-machine.md` load section.
- [ ] **B012** — Experience layout validation: dimensional validation of corridor, theater, and pod layouts within the actual clear width (after panels + acoustic treatment). Output: updated `configs/time-machine.md` layout section.

## Queued: E03-parametric-model — Chassis Simulation Engine

- [ ] **B013** — Base chassis renderer: Three.js scene with parametric exterior box. Inputs: length, width, height, wall thickness. Output: `simulation/src/chassis-renderer.js`
- [ ] **B014** — Wall assembly toggle: switch between assembly options in the model. See interior width change in real-time. Output: updated renderer.
- [ ] **B015** — Weight calculator: sum structural + envelope + system weights, compare to tow rating. Output: `simulation/src/weight-calc.js`
- [ ] **B016** — Thermal calculator: R-value computation from assembly, passive house target comparison. Output: `simulation/src/thermal-calc.js`

---

## How to Use This File

1. Find the first unchecked task
2. Read the referenced contract/config files for context
3. Complete the build
4. Mark the task as checked
5. Log the build in `builds.md`
6. Commit with `B{NNN}: description`
