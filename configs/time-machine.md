# Time Machine — Fit-Out Configuration

> **Status**: Draft — B008-B012 will flesh out each section
> **Type**: Fit-out configuration consuming the Henhouse ADU chassis contract

## Overview

Time Machine is the most demanding fit-out configuration for the Henhouse ADU chassis. It transforms the platform into an immersive LED experience venue for groups of 6-10 people. If the chassis can support Time Machine, it can support any configuration.

This document defines Time Machine's spatial requirements in terms of the chassis interface contract. Each requirement maps to a chassis provision. Where a requirement exceeds standard chassis capacity, it's flagged as a chassis design driver.

## Zone Allocation (To Be Defined in B008)

Total interior length: ~26'-28' (after end wall assembly)

```
┌──────────────────────────────────────────────────┐
│  ENTRY/     │  EXPERIENCE CHAMBER    │ CTRL│MECH │
│  TRANSITION │                        │     │     │
│  ~4'        │  ~16'                  │ ~4' │ ~4' │
│  (1219mm)   │  (4877mm)             │     │     │
└──────────────────────────────────────────────────┘
  Interior width: ~6'8" (2032mm) throughout
```

### Entry / Transition Zone (~4')
- **Purpose**: Light lock between exterior and experience. Mood transition, audience briefing.
- **Requirements**: Door to exterior, door/curtain to chamber. Total light blocking. Minimal footprint.
- **Systems needed**: Transition lighting (dimmable), speaker for briefing audio.
- **Chassis interface**: 1 electrical circuit, 1 lighting mount point, entry door.

### Experience Chamber (~16')
- **Purpose**: The show space. LED walls, immersive audio, controlled environment.
- **Floor area**: ~107 sq ft (9.9 m²) at 6'8" × 16'
- **Audience density**: 10.7-17.8 sq ft per person (6-10 people)
- **Requirements**: Total blackout, acoustic isolation, climate control, LED panels on both long walls.
- **Systems needed**: LED panels (×2 walls), immersive audio (min 4-channel), climate (supply + return), emergency lighting, emergency exit.
- **Chassis interface**: Multiple high-amperage circuits, structural mounting for LED panels on both long walls, HVAC supply and return, ceiling mounting for audio and emergency systems.
- **This zone drives chassis design.**

### Control Room (~4')
- **Purpose**: Operator station, Container OS hardware, network equipment.
- **Requirements**: Standing workstation, rack or shelf for compute hardware, display for Container OS tablet UI, cable routing to chamber.
- **Systems needed**: Standard electrical, network, small HVAC supply for equipment cooling.
- **Chassis interface**: 1-2 electrical circuits, cable routing to adjacent zones.

### Mechanical (~4')
- **Purpose**: HVAC equipment, electrical panel, audio amplifiers, power distribution.
- **Requirements**: Acoustic isolation from chamber (HVAC noise can't bleed into the experience). Access panels for maintenance. Ventilation for heat-generating equipment.
- **Systems needed**: Chassis HVAC lives here (or partially here). Fit-out audio amps and compute power supplies.
- **Chassis interface**: This zone IS part of the chassis (HVAC equipment location). Fit-out adds audio/compute gear.
- **Open question**: Does mechanical share space with control room to free up length for the chamber?

## LED Panel Layout (To Be Defined in B009)

### Geometry
- **Configuration**: Flat panels on both long interior walls of the experience chamber
- **Wall available width**: ~16' (4877mm) per side (chamber length)
- **Wall available height**: TBD (interior clear height, minus any baseboard/crown clearance)
- **Panel mounting surface**: Interior face of wall assembly

### Panel Sizing Constraints
- Panel width (horizontal dimension mounted on wall): limited by chamber length
- Panel height (vertical dimension): limited by interior clear height minus clearances
- Panel depth (projection from wall): **critical** — every inch of panel depth subtracts from the 6'8" clear width
  - At 2" (50mm) panel depth × 2 walls = 4" (100mm) total lost width
  - Remaining audience width: ~6'4" (1932mm)
  - At 4" (100mm) panel depth × 2 walls = 8" (200mm) total lost width
  - Remaining audience width: ~6'0" (1832mm)
- **Panel depth is a binding constraint.** Thin panels are not optional — they're required.

### Mounting Requirements
- Panel weight per sq ft: TBD
- Total panel weight per wall: TBD
- Mounting type: TBD (direct to structure, Z-clip, French cleat, rail system)
- Serviceability: individual panels must be removable without removing adjacent panels
- Cable routing: power and data to each panel, routed behind panel or through wall chase

## Acoustic Treatment (To Be Defined in B010)

### Isolation Requirements
- **Exterior → Interior**: Exterior noise must not be audible during experience. Target STC rating TBD.
- **Interior → Exterior**: Experience audio must not be audible at property boundary. Target TBD.
- **Mechanical → Chamber**: HVAC and equipment noise must not be audible in chamber. Target NC rating TBD.

### Treatment Impact on Clear Width
- Acoustic treatment adds thickness to interior wall surfaces
- Every 1" of acoustic treatment × 2 walls = 2" total lost width
- Must be budgeted alongside LED panel depth
- **Combined panel + acoustic depth per wall is a critical dimension**

### Budget: Wall Thickness from Clear Width
```
Starting interior width:           ~6'8"  (2032mm)
Minus acoustic treatment (×2):     -TBD"
Minus LED panel depth (×2):        -TBD"
Minus any air gap / mounting (×2): -TBD"
═══════════════════════════════════════════
Remaining audience clear width:     TBD
```
**Target: maintain ≥5'6" (1676mm) clear width between LED panel faces** [ASSUMED — minimum for 2 people to pass comfortably]

## Electrical & Thermal Loads (To Be Defined in B011)

### Electrical Load Estimate
| Component | Qty | Watts Each | Total Watts |
|-----------|-----|-----------|-------------|
| LED panels | TBD | TBD | TBD |
| Compute hardware | TBD | TBD | TBD |
| Audio amplifiers | TBD | TBD | TBD |
| Experience lighting | TBD | TBD | TBD |
| Container OS hardware | 1 | TBD | TBD |
| HVAC (chassis-provided) | 1 | TBD | TBD |
| **Total** | | | **TBD** |

### Thermal Load
- All electrical power eventually becomes heat
- Additional: audience body heat (10 people × ~400 BTU/hr = 4,000 BTU/hr)
- Chamber is sealed and dark — no solar gain, no natural ventilation
- **Cooling is the dominant HVAC concern**, not heating (even in winter, internal heat generation likely exceeds losses in a passive house envelope)

## Experience Layout Options (To Be Defined in B012)

Three candidate layouts for the experience chamber, all within the same physical envelope:

### Option A: Corridor (Walk-Through)
- Audience moves linearly through the space between LED walls
- Duration: 5-8 minutes
- Capacity: 6-8 flowing through
- Requires: clear floor, guided path, possible one-way flow (enter one end, exit other)
- Chair/fixture requirements: none

### Option B: Theater (Seated)
- Audience seated in 1-2 rows, content on both walls
- Duration: 15-30 minutes
- Capacity: 8-10 seated
- Requires: chairs or bench seating that fits within clear width between panels
- Seating depth budget: clear width minus 2× (panel depth + acoustic treatment + air gap)

### Option C: Pod (Standing, Short-Duration)
- Audience enters as a group, stands surrounded by content
- Duration: 3-5 minutes
- Capacity: 6-8 standing
- Requires: clear floor, no fixtures
- Highest throughput (sessions per hour)

### Layout Comparison
| Factor | Corridor | Theater | Pod |
|--------|----------|---------|-----|
| Session duration | 5-8 min | 15-30 min | 3-5 min |
| Capacity | 6-8 | 8-10 | 6-8 |
| Sessions/hour | ~8 | ~2-3 | ~12 |
| Throughput/hour | ~48-64 | ~16-30 | ~72-96 |
| Revenue model | Mid-price, mid-volume | Higher price, lower volume | Lower price, highest volume |
| Setup complexity | Medium (path markers) | Medium (seating) | Low (empty room) |
| Experience depth | Linear narrative | Deeper, contemplative | Intense, sensory |
