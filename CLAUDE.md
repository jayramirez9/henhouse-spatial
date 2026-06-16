# CLAUDE.md — Henhouse Spatial

## Project Identity

**Henhouse Spatial** is the parametric design and simulation environment for the Henhouse mobile micro-venue platform — a hyper-efficient, Passivhaus-level, towable box on a flatbed trailer. The unit is a **platform product**: a universal, climate-controlled shell that accepts different interior "cartridge" configurations. Content Node (broadcast studio / immersive LED venue) is the most demanding cartridge. Sanctuary (luxury green room) is the simplest.

This project models the chassis envelope, validates cartridge configurations against structural and spatial constraints, and simulates the physical systems that Container OS will control.

## Before You Do Anything

1. Read `masterplan.md` — understand the platform-first product model
2. Read `implementation-plan.md` — understand the current phase and epic sequence
3. Read `tasks.md` — find the current build task
4. Read `builds.md` — understand what's already been built
5. Read relevant files in `contracts/` — understand spatial contracts and constraints
6. Read relevant files in `configs/` — understand existing fit-out configurations
7. Only then write code or modify files

## Project Conventions

### Methodology
This project follows **Forge v0.2** (see `docs/forge-programming-system.md`). Key rules:
- Contract-first: define spatial constraints before writing simulation code
- Write the eval before the feature
- One build per session, one concern per build
- Commit messages use build numbers: `B001: description`

### Epic & Build Tracking
- Epics defined in `implementation-plan.md`
- Current tasks in `tasks.md`
- Completed builds logged in `builds.md`
- Build numbers are global across the project (B001, B002, B003...)

### File Organization
```
contracts/           # Spatial contracts, structural constraints, interface specs
  schemas/           # JSON schemas for constraint validation
configs/             # Cartridge configurations (content-node, sanctuary, sportsbook, lounge)
simulation/
  src/               # Simulation engine code
  tests/             # Tests mirror src/ structure
docs/                # Reference documents, methodology, research
```

### Code Standards
- **Language**: JavaScript/TypeScript (Node.js) for simulation logic. Three.js for 3D visualization.
- **Units**: All dimensions in millimeters internally. Display in feet/inches for US context.
- **Naming**: camelCase for variables/functions, PascalCase for classes, UPPER_SNAKE for constants
- **Comments**: Only where "why" isn't obvious from the code
- **Dependencies**: Minimize. Justify each one.

### Key Design Principle: Platform vs. Cartridge Separation
- **Chassis files** define the universal platform (SIP shell, ERV, HVAC, 50A electrical, ISO castings)
- **Config files** define specific cartridges (Content Node, Sanctuary, Pop-Up Sportsbook, Heavy-Air Lounge)
- The chassis does not reference any specific cartridge
- Cartridges reference the chassis interface contract to validate compatibility
- When a constraint changes, check ALL cartridge configs for impact

### Dimensional Constants
These are the binding constraints from road-legal towable transport (no CDL):
- **Exterior width**: 8'6" (102" / 2591mm) — Georgia statewide legal max, no oversize permit for GA-local delivery (D002, 2026-06-16; was 8'0"/2438mm). 12'-lane caveat on narrow final approaches.
- **Exterior height**: 13'6" (4115mm) including trailer deck
- **Length**: 30' (9144mm)
- **Interior clear width**: ~7'3" (2210mm) as-built, **7'2" (2184mm) design target** after 6½" GPS SIP wall assembly (D002; was ~6'8")
- Interior clear width is THE binding spatial constraint for all cartridges

## Architecture Context

This project sits alongside two other Henhouse products:

```
henhouse-spatial     ◄── THIS PROJECT — physical platform design + simulation
henhouse-container-os    — software control plane for deployed venues
time-machine             — immersive experience software (consumed by Content Node cartridge)
```

The spatial simulation informs Container OS by defining what physical systems exist and what the OS needs to control. Container OS protocol commands map to physical subsystems modeled here.

## Rules for AI Collaboration

- Reference specific files in prompts, don't re-describe what's already documented
- After fixing a bug, explain what went wrong so rules can be updated
- When you discover a constraint or dimension, add it to the relevant contract file
- All dimensional values must include both imperial and metric (metric is source of truth)
- Never modify chassis contracts without checking all cartridge configs for impact
- If a spatial assumption is unvalidated, flag it as `[ASSUMED]` in the document
