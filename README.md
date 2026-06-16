# Henhouse Spatial

Parametric design and simulation environment for the Henhouse ADU platform — a deployable, towable, passive-house-grade structure on a trailer chassis.

The ADU is a **platform product**. What goes inside — a Time Machine immersive experience, a living unit, a studio — is a fit-out configuration. This project models the chassis, validates configurations, and simulates the building systems Container OS will control.

## Project Status

**Phase 0/1 — Discovery + Architecture**

Currently defining the chassis spatial contract and Time Machine fit-out requirements. No simulation code yet — contracts first.

## Documentation

| Document | Purpose |
|----------|---------|
| [masterplan.md](masterplan.md) | Platform-first product model, binding constraints, success criteria |
| [implementation-plan.md](implementation-plan.md) | Epic map, build sequence, technology decisions, open questions |
| [tasks.md](tasks.md) | Current build tasks |
| [builds.md](builds.md) | Completed build log |
| [CLAUDE.md](CLAUDE.md) | Project rules for Claude Code agent |

## Contracts & Configs

| Document | Purpose |
|----------|---------|
| [chassis-contract.md](contracts/chassis-contract.md) | The platform spec — what the chassis provides to any fit-out |
| [time-machine.md](configs/time-machine.md) | Time Machine fit-out — spatial requirements, zone layout, LED spec |

## Architecture

```
HENHOUSE ADU CHASSIS (this project models this)
  └── Fit-out configurations:
        ├── Time Machine (immersive LED experience) ← most demanding, designs the chassis
        ├── Living Unit (ADU dwelling) ← simplest
        └── Future configs...

CONTAINER OS (separate project) controls the chassis + fit-out systems
```

## Binding Constraints

- **Exterior width**: 8'6" / 102" (Georgia legal max, no permit — D002; pickup-towable)
- **Interior clear width**: ~7'2" design / 7'3" as-built after wall assembly — THE binding spatial constraint
- **Length**: 28'-30' practical max
- **Performance**: Passive house grade

## Methodology

Built using [Forge v0.2](docs/forge-programming-system.md) — contract-first, eval-driven development.
