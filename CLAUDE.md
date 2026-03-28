# CLAUDE.md — Henhouse Spatial

## Project Identity

**Henhouse Spatial** is the parametric design and simulation environment for the Henhouse ADU platform — a deployable, towable, passive-house-grade structure on a trailer chassis. The ADU is a **platform product**: a universal, climate-controlled box that accepts different interior fit-out configurations. Time Machine (immersive LED experience) is the most demanding fit-out. A living unit is the simplest.

This project models the chassis envelope, validates fit-out configurations against structural and spatial constraints, and simulates the physical systems that Container OS will control.

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
configs/             # Fit-out configurations (time-machine/, adu-living/, etc.)
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

### Key Design Principle: Platform vs. Fit-Out Separation
- **Chassis files** define the universal platform (structure, envelope, HVAC, electrical)
- **Config files** define specific fit-outs (Time Machine, living unit, office, etc.)
- The chassis does not reference any specific fit-out
- Fit-outs reference the chassis interface contract to validate compatibility
- When a constraint changes, check ALL fit-out configs for impact

### Dimensional Constants
These are the binding constraints from DOT road-legal towable transport:
- **Max exterior width**: 8'0" (2438mm)
- **Max exterior height**: 13'6" (4115mm) including trailer deck
- **Practical max length**: 28'-30' (8534-9144mm) for pickup-towable
- **Interior clear width**: ~6'8" (2032mm) after wall assembly
- Interior clear width is THE binding spatial constraint for all fit-outs

## Architecture Context

This project sits alongside two other Henhouse products:

```
henhouse-spatial     ◄── THIS PROJECT — physical platform design + simulation
henhouse-container-os    — software control plane for deployed venues
time-machine             — the immersive experience product (fit-out config)
```

The spatial simulation informs Container OS by defining what physical systems exist and what the OS needs to control. Container OS protocol commands map to physical subsystems modeled here.

## Rules for AI Collaboration

- Reference specific files in prompts, don't re-describe what's already documented
- After fixing a bug, explain what went wrong so rules can be updated
- When you discover a constraint or dimension, add it to the relevant contract file
- All dimensional values must include both imperial and metric (metric is source of truth)
- Never modify chassis contracts without checking all fit-out configs for impact
- If a spatial assumption is unvalidated, flag it as `[ASSUMED]` in the document
