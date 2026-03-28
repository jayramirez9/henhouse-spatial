# Henhouse Spatial — Masterplan

## What This Is

Henhouse Spatial is the parametric design and simulation environment for the Henhouse ADU platform. It models the physical chassis, validates fit-out configurations, and simulates the building systems that Container OS will control in deployed venues.

The core insight: **the ADU is a platform, not a product.** It's a universal, towable, passive-house-grade box on a trailer chassis. What goes inside — a Time Machine immersive experience, a living unit, a studio — is a fit-out configuration. The chassis doesn't know or care what's inside it. It provides structure, climate, and power. The fit-out provides purpose.

## The Problem

Henhouse needs to design a single physical chassis that:
1. Meets passive house energy efficiency standards
2. Is towable by a pickup truck without oversize permits
3. Provides excellent ventilation, heating, and cooling
4. Accepts multiple interior fit-out configurations without structural changes
5. Supports the most demanding fit-out (Time Machine: LED panels, audio, compute, audiences) without over-engineering the simplest (a well-ventilated box)

These constraints interact in non-obvious ways. Wall thickness affects interior width, which affects fit-out viability. Weight affects towability, which constrains material choices. HVAC capacity must handle Time Machine's heat loads without being oversized for a living unit.

**Problem statement:** Henhouse needs a parametric model of the ADU chassis that lets designers explore structural, thermal, and spatial tradeoffs — and validate that specific fit-out configurations satisfy their requirements within the chassis constraints.

## Who It's For

### Primary: Jay (Founder / Designer)
Needs to make design decisions about the chassis: wall assembly, structural system, HVAC sizing, electrical capacity. Needs to see how those decisions affect interior space, weight, cost, and fit-out compatibility.

**Success looks like:** Jay can change wall thickness from 4" to 6", see the interior width drop from 6'8" to 6'4", check whether Time Machine's LED panels still fit, and see the weight and R-value impact — all in one tool.

### Secondary: Fabrication Partners
When the design is locked, fabrication partners need precise dimensional drawings, material specs, and assembly sequences.

**Success looks like:** The parametric model exports construction-grade specifications that a fabricator can build from.

### Tertiary: Container OS (Machine Consumer)
The simulation defines what physical systems exist in the chassis — HVAC zones, electrical circuits, lighting fixtures, sensor locations. Container OS needs this to know what it's controlling.

**Success looks like:** The spatial model exports a system manifest that Container OS can import as its hardware map.

## Platform Architecture

### The Chassis Provides

| System | What the Chassis Gives Every Configuration |
|--------|-------------------------------------------|
| **Structure** | Trailer frame, floor deck, wall framing, roof structure. Load-bearing, weatherproof, road-legal. |
| **Thermal envelope** | Insulation, air sealing, vapor management. Passive house grade. |
| **Climate** | HVAC system — heating, cooling, ventilation, filtration. Ducted to configurable zones. |
| **Electrical** | Shore power connection, main panel, circuit distribution. Capacity spec'd for worst-case fit-out. |
| **Entry** | At least one door with weather seal. Location and size per chassis spec. |
| **Floor** | Flat, level, load-bearing interior floor ready for fit-out finish. |

### The Chassis Does Not Provide

- Interior partition walls (fit-out specific)
- Interior finish surfaces (fit-out specific)
- Plumbing (not every configuration needs it)
- Audio/visual infrastructure (fit-out specific)
- Network infrastructure beyond basic electrical (fit-out specific)
- Specific lighting (fit-out provides its own)

### The Fit-Out Interface

The chassis exposes a **fit-out interface** — a defined set of connection points, capacities, and spatial allowances that any configuration can use:

- Electrical connection points (location, capacity per circuit)
- HVAC register locations (supply and return)
- Structural mounting points (wall, ceiling, floor — with load ratings)
- Cable/conduit routing paths
- Interior clear dimensions (the buildable volume)

This is the spatial equivalent of an API. The chassis is the platform. The fit-out interface is the contract. The configuration is the consumer.

## Binding Constraints

### Transport (DOT Road-Legal, Pickup-Towable)
- **Max exterior width**: 8'0" (2438mm)
- **Max exterior height**: 13'6" (4115mm) including trailer deck height
- **Practical max length**: 28'-30' (8534-9144mm)
- **Max tow weight**: ~10,000-14,000 lbs depending on tow vehicle class [ASSUMED — needs validation against specific truck + trailer ratings]

### Interior Clear Width
After wall assembly (structure + insulation + interior surface), the usable interior width is approximately **6'8" (2032mm)**. This is THE binding spatial constraint for all fit-outs. It determines:
- How many people can stand side-by-side
- Whether standard fixtures (appliances, furniture) fit
- LED panel sizing for Time Machine
- Aisle width for wheelchair accessibility [ASSUMED — ADA may require 36" clear aisle]

### Passive House Performance Targets
- Airtightness: ≤0.6 ACH50 [ASSUMED — standard passive house requirement]
- Heating demand: ≤15 kWh/m²/year
- Total primary energy: ≤120 kWh/m²/year
- Thermal bridge free construction

## Fit-Out Configurations

### Time Machine (Most Demanding)
The immersive LED experience venue. Drives the chassis design because it has the highest requirements across every system.

- **Zone allocation**: Entry/transition (4'), experience chamber (16'), control room (4'), mechanical (4')
- **Electrical load**: High — LED panels, compute hardware, audio amplifiers, experience lighting
- **Thermal load**: High — LED heat generation + audience body heat in a sealed, dark space
- **Acoustic requirement**: High — sound isolation from exterior, interior acoustic treatment
- **Structural load**: Medium — LED panels mounted to walls, possible ceiling-mounted equipment
- **Audience**: 6-10 people per session
- **Light control**: Total blackout capability required
- **LED layout**: Flat panels on both long interior walls
- **Experience design options**: Corridor (walk-through), Theater (seated), Pod (standing, short duration)

### Living Unit (Simplest)
A well-ventilated, efficient dwelling. The ADU in its purest form.

- **Zone allocation**: Entry, kitchen, bath, sleeping, living/flex
- **Electrical load**: Standard residential
- **Thermal load**: Standard — cooking, bathing, body heat
- **Acoustic requirement**: Low-medium — residential comfort
- **Structural load**: Low — standard fixtures and cabinetry
- **Plumbing**: Yes — kitchen and bath (chassis modification or fit-out addition?)
- **Light control**: Windows required (unlike Time Machine)

### Office / Studio (Medium)
Climate-controlled workspace.

- **Zone allocation**: Entry, main workspace, storage
- **Electrical load**: Medium — computing, displays, lighting
- **Thermal load**: Low-medium
- **Acoustic requirement**: Medium — quiet workspace
- **Structural load**: Low
- **Network**: High-speed connectivity required

## Success Criteria (Evals)

| Criteria | Measurement |
|----------|-------------|
| Parametric model is dimensional | Changing one input (wall thickness) cascades to all dependent values |
| Time Machine fits | LED panels + audience + zones fit within chassis clear dimensions |
| Weight is towable | Total chassis weight (worst-case fit-out) is within pickup tow rating |
| Passive house targets met | R-values, airtightness, thermal bridge analysis pass thresholds |
| Fit-out interface is clear | Any configuration can determine compatibility from the interface spec |
| HVAC handles worst case | Climate system sized for Time Machine heat loads (then everything else is covered) |

## Open Questions

- [ ] What wall assembly? (Wood stud + mineral wool? SIPs? Composite panels?) — affects width, weight, R-value, cost, buildability
- [ ] Is weight or width the actual binding constraint? Jay suspects prototyping will reveal this.
- [ ] Plumbing: chassis-provided or fit-out-provided? If some configs need it and others don't, where does the rough-in live?
- [ ] Trailer deck height? (Affects total height budget remaining for the box)
- [ ] Single or dual axle? (Affects weight capacity and towing dynamics)
- [ ] Does the chassis need to be self-leveling or does the fit-out handle site adaptation?
- [ ] ADA accessibility requirements for commercial deployments (Time Machine)?
- [ ] Fire code / egress requirements for 6-10 occupancy commercial use?
