# Henhouse ADU — Chassis Contract

> **Status**: Draft — B002-B007 will flesh out each section

## Overview

The chassis contract defines what the Henhouse ADU platform provides to any fit-out configuration. It is the spatial equivalent of an API: the chassis is the platform, this contract is the interface, and fit-out configurations are consumers.

A fit-out configuration can validate compatibility by checking its requirements against this contract. If every requirement maps to a chassis provision, the configuration fits.

## Design Principles

1. **Configuration-agnostic.** The chassis doesn't know what goes inside it. It provides structure, climate, and power.
2. **Worst-case sized.** Systems are sized for the most demanding fit-out (Time Machine). Simpler configurations use a subset of capacity.
3. **Interface-defined.** Connection points, mounting points, and capacities are explicitly specified. A fit-out designer knows exactly what's available without guessing.
4. **Prototyping reveals constraints.** Where a value is assumed rather than validated, it's marked `[ASSUMED]`. Prototyping will confirm or correct.

## Exterior Envelope (To Be Defined in B002)

### Transport-Legal Dimensions
| Dimension | Value | Notes |
|-----------|-------|-------|
| Max exterior width | 8'0" (2438mm) | DOT road-legal, no oversize permit |
| Max exterior height | 13'6" (4115mm) | Including trailer deck height |
| Practical max length | 28'-30' (8534-9144mm) | Pickup-towable practical limit |
| Trailer deck height | TBD | [ASSUMED ~18-24" — varies by trailer frame] |
| Box height on deck | TBD | Total height minus deck height |

### Weight Budget
| Component | Weight | Notes |
|-----------|--------|-------|
| Trailer frame + running gear | TBD | |
| Floor assembly | TBD | |
| Wall assembly (× 2 long walls) | TBD | |
| Wall assembly (× 2 end walls) | TBD | |
| Roof assembly | TBD | |
| HVAC system | TBD | |
| Electrical system | TBD | |
| **Chassis subtotal** | **TBD** | |
| Fit-out allowance | TBD | Remaining weight for interior build-out |
| **Max tow weight** | **TBD** | [ASSUMED 10,000-14,000 lbs] |

## Wall Assembly Options (To Be Defined in B003)

Three candidate assemblies to evaluate:

### Option A: Wood Stud + Mineral Wool
- **Framing**: 2×4 or 2×6 wood studs at 16" or 24" OC
- **Insulation**: Mineral wool batts (R-15 for 2×4, R-23 for 2×6)
- **Exterior**: Sheathing + weather barrier + cladding
- **Interior**: Finish surface (fit-out specific)
- **Total wall thickness**: TBD
- **R-value**: TBD
- **Weight per linear foot**: TBD
- **Width impact**: TBD (remaining interior clear width)
- **Pros**: Jay's preferred material (woodworking), readily available, well-understood
- **Cons**: Thermal bridging at studs, potentially heavier than alternatives

### Option B: SIPs (Structural Insulated Panels)
- **Panel**: OSB skins + foam core
- **Total wall thickness**: TBD
- **R-value**: TBD
- **Weight per linear foot**: TBD
- **Width impact**: TBD
- **Pros**: High R-value per inch, fast assembly, minimal thermal bridging
- **Cons**: Less flexibility for modifications, harder to route wiring

### Option C: Composite / Alternative
- **TBD** — research needed on thin-wall high-performance assemblies
- Possible: vacuum insulated panels, aerogel blankets, etc.
- **Pros**: Potentially thinnest wall, maximizing interior width
- **Cons**: Cost, availability, repairability

## Structural Grid (To Be Defined in B004)

- Bay spacing: TBD
- Load paths: roof → wall → floor → trailer frame
- Wall mounting capacity: TBD lbs/sq ft (must support LED panels for Time Machine)
- Ceiling mounting capacity: TBD lbs per point (lighting, HVAC registers, rigging)
- Floor load capacity: TBD lbs/sq ft (audience standing load for Time Machine)

## HVAC System (To Be Defined in B005)

### Sizing Basis: Time Machine Worst Case
- LED panel heat generation: TBD BTU/hr
- Audience body heat (10 people): ~4,000 BTU/hr [ASSUMED — ~400 BTU/hr per person]
- Compute hardware heat: TBD BTU/hr
- Audio amplifier heat: TBD BTU/hr
- **Total cooling load**: TBD BTU/hr

### Ventilation
- Fresh air requirement: TBD CFM (passive house ventilation standard)
- CO2 monitoring: yes (required for occupied space)
- ERV (Energy Recovery Ventilator): TBD — recommended for passive house

### Zone Layout
- TBD — dependent on whether zones are chassis-defined or fit-out-defined
- Minimum: one supply register and one return per fit-out zone
- HVAC register locations are part of the fit-out interface

## Electrical System (To Be Defined in B006)

### Shore Power
- Connection: TBD (30A / 50A / 100A)
- Voltage: 120/240V split phase [ASSUMED — standard US]

### Distribution
- Main panel: TBD amp rating
- Circuit count: TBD
- Dedicated circuits for: HVAC, fit-out general, fit-out high-load, lighting, control systems

### Connection Points (Fit-Out Interface)
- Location and rating of each available circuit at fit-out boundary
- TBD — defined in B006 and formalized in B007

## Fit-Out Interface (To Be Defined in B007)

This is the key deliverable — the "API" between chassis and configuration.

### What the Interface Specifies
- **Clear interior volume**: length × width × height of the buildable space
- **Electrical connection points**: location, circuit number, amperage, voltage
- **HVAC register locations**: supply and return positions, CFM capacity per register
- **Structural mounting grid**: wall, ceiling, and floor mounting points with load ratings
- **Cable routing paths**: chase locations for running fit-out wiring
- **Entry point(s)**: door location, clear opening dimensions
- **Floor**: surface type, load rating, level tolerance

### Interface Rules
1. Fit-out must not exceed total electrical capacity
2. Fit-out must not exceed structural mounting load ratings
3. Fit-out must not block HVAC airflow paths
4. Fit-out must maintain minimum clearance to entry/egress
5. Fit-out must not penetrate the thermal envelope
6. Fit-out total weight must not exceed weight allowance (total tow weight minus chassis weight)
