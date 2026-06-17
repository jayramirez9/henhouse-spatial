# Content Node — Cartridge Configuration (Mobile Studio)

> **Status**: Draft — B008-B012 will flesh out each section
> **Type**: Cartridge configuration consuming the Henhouse chassis contract
> **Role**: Most demanding cartridge — drives chassis design

## Overview

Content Node is the most demanding cartridge for the Henhouse chassis. It transforms the platform into a dead-silent, broadcast-ready mobile studio or immersive LED experience venue for groups of 6-10 people. If the chassis can support Content Node, it can support any cartridge.

This document defines Content Node's spatial requirements in terms of the chassis interface contract. Each requirement maps to a chassis provision. Where a requirement exceeds standard chassis capacity, it's flagged as a chassis design driver.

## Zone Allocation (To Be Defined in B008)

Total interior length: ~28' (after end wall SIP assembly)

```
┌──────────────────────────────────────────────────┐
│  ENTRY/     │  STUDIO / EXPERIENCE     │ CTRL│MECH│
│  TRANSITION │  CHAMBER                 │     │    │
│  ~4'        │  ~16'                    │ ~4' │ ~4'│
│  (1219mm)   │  (4877mm)               │     │    │
└──────────────────────────────────────────────────┘
  Interior width: ~7'2" (2184mm) throughout  ← D002 (102" exterior)
```

### Entry / Transition Zone (~4')
- **Purpose**: Light lock between exterior and studio. Acoustic transition, guest briefing.
- **Requirements**: Door to exterior, door/curtain to chamber. Total light blocking. Minimal footprint.
- **Systems needed**: Transition lighting (dimmable), speaker for briefing audio.
- **Chassis interface**: 1 electrical circuit, 1 lighting mount point, entry door.

### Studio / Experience Chamber (~16')
- **Purpose**: The primary space. LED walls for immersive content or broadcast backdrop, multi-camera ceiling grid, immersive audio.
- **Floor area**: ~115 sq ft (10.7 m²) at 7'2" × 16' (D002)
- **Audience density**: 11.5-19.2 sq ft per person (6-10 people)
- **Requirements**: Total blackout capability, acoustic isolation (room-within-a-room), climate control, LED panels on both long walls.
- **Systems needed**: LED panels (×2 walls), multi-camera ceiling grid, immersive audio (min 4-channel), climate (supply + return), emergency lighting, emergency exit.
- **Chassis interface**: Multiple high-amperage circuits, structural mounting for LED panels on both long walls, ceiling grid mounting points, HVAC supply and return, ceiling mounting for audio and emergency systems.
- **This zone drives chassis design.**

### Control Room (~4')
- **Purpose**: Operator station, Container OS hardware, streaming/broadcast console, network equipment.
- **Requirements**: Standing workstation, rack or shelf for compute hardware, pre-wired streaming console, display for Container OS, cable routing to chamber.
- **Systems needed**: Standard electrical, network, small HVAC supply for equipment cooling.
- **Chassis interface**: 1-2 electrical circuits, cable routing to adjacent zones.

### Mechanical (~4')
- **Purpose**: HVAC equipment, ERV unit, electrical panel, audio amplifiers, power distribution.
- **Requirements**: Acoustic isolation from chamber (HVAC/ERV noise can't bleed into the studio). Access panels for maintenance. Ventilation for heat-generating equipment.
- **Systems needed**: Chassis HVAC + ERV live here. Cartridge adds audio amps and compute power supplies.
- **Chassis interface**: This zone IS part of the chassis (HVAC/ERV equipment location). Cartridge adds studio-specific gear.
- **Open question**: Does mechanical share space with control room to free up length for the chamber?

## LED Panel Layout (To Be Defined in B009)

### Display Technology & Surface (explored 2026-06-16 — B009 will finalize)

**Primary display surface: the back/end wall** (~7'2"–7'6" wide × 8' tall ≈ 60 sq ft / 5.6 m² wall opening; the 6-tile COB build below covers ~54 sq ft of it). Mounting the main display on the **end** wall is deliberate — its depth eats interior **length** (abundant, 16' chamber), not **width** (the scarce binding dimension). This reframes the original "flat panels on both long walls" wraparound concept: true COSM-style wraparound is **off the table** (16–38 kW and a 26'-wide surface can't exist in an 8'-wide, no-CDL, 50A box), so Content Node's realistic display is a **focal back wall** — plus, for immersive installs, secondary **"window" displays on the long walls** (see below). *Resolved direction (2026-06-16, Jay): immersive / Time Machine installs add long-wall window displays; broadcast-only installs may leave the long walls acoustic/neutral.*

Two technology options, both validated to fit the chassis power/heat/weight budgets:

| | **Option A — COB all-in-one DVLED** | **Option B — UST laser projection** |
|---|---|---|
| Example unit [vendor specs, unverified] | Panasonic TL-55LV12AW (3-in-1 COB, 1.26mm, 800 nits, 10,000:1, 156–172 W/tile, 40 lb/tile) | Hisense PX4-PRO (3,500 ANSI lm UST, dynamic iris, 6000:1, 1ms/VRR) |
| Back-wall build | 6 tiles, 3×2 portrait → ~6.75'×8', ~1620×1920 (~2K) | Single UST + high-contrast screen |
| **Power (operating)** | **~0.6–1.0 kW** (run dimmed in the dark box) | **~0.4 kW** |
| **Heat to room** | ~3,400 BTU/hr | ~1,400 BTU/hr (ductable) |
| **Weight** | ~300 lb (panels + structure) | ~80 lb |
| **Cost (est.)** | ~$25–40k | ~$3–5k |
| Blacks in dark room | **True (emissive)** | Gray (projector black on screen) |
| Lights the talent | **Yes** | No |
| Talent shadows | **None** | Yes (body blocks the throw) |
| Fleet serviceability | **All-in-one swappable tiles, no field calibration** | Single unit |

**Decision rule (2026-06-16):**
- **COB is the primary bet** for the broadcast / virtual-production backdrop — it solves exactly what projection can't (true blacks, lights the subject, no shadows, fleet-serviceable). It is the default for any premium build.
- **Projection is a budget-only fallback**, justified solely by its ~10× lower cost — and only for **audience-viewing** layouts where no camera is involved (so gray blacks / shadows / no subject-lighting don't matter).
- **If the display budget exceeds ~$50k, commit to COB outright.** Projection's *only* advantage is cost; once you're spending at that tier the compromise isn't worth it. (Jay, 2026-06-16)

**Power/heat is not the constraint here.** Either option is a rounding error against the chassis budget — ~0.4–1.0 kW vs the ~6,450 W cartridge allowance (B005), and ≤3,400 BTU/hr vs the 3-ton HVAC. The power/heat wall only ever existed at COSM wraparound scale, which a focal back wall avoids entirely. Mounting weight (~300 lb COB over its ~54 sq ft active area ≈ 5.5 psf) sits comfortably under B004's ≥10 psf wall provision — noting that provision is OSB-derived (ESR-4524) and pending FRP-supplier restatement (Weight Strategy), but the ~2× margin holds either way.

### Secondary "Window" Displays — Long Walls (immersive / Time Machine installs)

For immersive installs, the long side-walls carry secondary displays that function as **virtual windows** onto the Time Machine environment (the period/weather/place scene), deepening immersion beyond the focal back wall. These serve the **immersive Theater / Corridor layouts (B012)** — not the broadcast backdrop. **Size and quantity: TBD (Jay, 2026-06-16)**; the levers below will size them.

- **Width is the binding cost here — the opposite of the back wall.** The back wall's depth ate abundant *length*; long-wall windows protrude into the scarce ~7'2" clear *width*, and ×2 (both walls). The panel-depth budget above applies directly (2" → 6'10", 4" → 6'6"). **Keep them thin, or nest them.**
- **Nest the window depth inside the acoustic/service wall buildout (B010), not protruding past it** — so the windows cost *no width beyond what acoustic treatment already spends*. This is the move that lets windows and clear-width coexist, and **the ≥5'6" clear-width margin above assumes nesting.** The thin surface-mount OLED (~1.5") fallback (if there's no cavity to nest into) sits *on top of* acoustic treatment and **re-opens the width budget** — re-derive ≥5'6" in B010 if the fallback is used.
- **Power/heat fits, but stop treating displays as free.** Illustratively [size/qty TBD], ~4–4.5 m² of window display ≈ another ~0.8–1 kW → total display (back wall + windows) **~2 kW ≈ ⅓ of the ~6,450 W cartridge envelope (B005)** — *before* compute, audio, lighting, cameras, and Container OS. It's not "well under"; it's a third already spent. Reconcile against the full itemized load in B011 — the 50A service, not the display, is the binding cap.
- **Acoustic tension → B010.** The long walls are *also* the prime candidates for room-within-a-room acoustic mass (the "Taycan-quiet" goal). A rigid glass display is reflective, low-mass, and a potential flanking/leak path — so the windows must be acoustically detailed (isolated mounts, mass-loaded backing, no through-wall penetration). **Reconcile windows-vs-isolation in B010.**
- **Platform note.** The chassis provides the long-wall hard points, power, and interface; *populating* them with window displays is a Content Node immersive-cartridge choice, not a chassis feature — other cartridges (Sanctuary, Sportsbook, Lounge) need not.

### Geometry
- **Configuration**: Primary display on the **back/end wall** + secondary **"window" displays on the long walls** for immersive / Time Machine installs (see Display Technology above). Full-coverage wraparound on the long walls is infeasible; the long-wall displays are discrete windows, sized to nest within the acoustic buildout (B009/B010).
- **Wall available width**: ~16' (4877mm) per side (chamber length)
- **Wall available height**: TBD (interior clear height, minus any baseboard/crown clearance)
- **Panel mounting surface**: Interior face of SIP wall assembly (or acoustic decoupling layer)

### Panel Sizing Constraints
- Panel width (horizontal dimension mounted on wall): limited by chamber length
- Panel height (vertical dimension): limited by interior clear height minus clearances
- Panel depth (projection from wall): **critical** — every inch of panel depth subtracts from the 7'2" clear width (D002)
  - At 2" (50mm) panel depth × 2 walls = 4" (100mm) total lost width
  - Remaining audience width: ~6'10" (2083mm)
  - At 4" (100mm) panel depth × 2 walls = 8" (200mm) total lost width
  - Remaining audience width: ~6'6" (1981mm)
- **Panel depth is still the constraint to watch, but D002's +6" interior gives real breathing room** — even at 4" panels + acoustic treatment, the ≥5'6" target now holds with margin.

### Mounting Requirements
- Panel weight per sq ft: TBD
- Total panel weight per wall: TBD
- **Mounting type: rail/ledger system through-bolted to chassis hard points** — per chassis B004, LED rails must land on embedded Type L lumber splines / ledgers, **never on bare SIP skin** (foam+OSB won't hold the load). Ledger heights are a chassis interface coordinate finalized in B007; LED layout (B009) must align panel mounting to those lines. Design to the chassis ≥10 psf wall hung-load provision.
- Serviceability: individual panels must be removable without removing adjacent panels
- Cable routing: power and data to each panel, routed behind panel or through SIP chase

## Acoustic Treatment (To Be Defined in B010)

### Isolation Requirements
- **Exterior → Interior**: Exterior noise must not be audible during studio use. Broadcast-grade silence. Target STC rating TBD.
- **Interior → Exterior**: Studio audio must not be audible at property boundary. Target TBD.
- **Mechanical → Chamber**: HVAC/ERV noise must not be audible in chamber. Target NC rating TBD.
- **Room-within-a-room**: Acoustic decoupling from chassis structure for broadcast-grade isolation.

### Treatment Impact on Clear Width
- Acoustic treatment adds thickness to interior wall surfaces
- Every 1" of acoustic treatment × 2 walls = 2" total lost width
- Must be budgeted alongside LED panel depth
- **Combined panel + acoustic depth per wall is a critical dimension**

### Budget: Wall Thickness from Clear Width
Starting interior width is now validated by the chassis contract (B003 + D002): 6½" GPS SIP walls at the 102" exterior yield **~7'3" (2210mm) as-built**, with **7'2" (2184mm) as the cartridge design target** (the extra inch is tolerance margin, not buildable space). Content Node builds against 7'2".
```
Starting interior width (design):  7'2"   (2184mm)  ← chassis B003 + D002
Minus acoustic treatment (×2):     -TBD"
Minus LED panel depth (×2):        -TBD"
Minus any air gap / mounting (×2): -TBD"
═══════════════════════════════════════════════════
Remaining audience clear width:     TBD
```
**Target: maintain ≥5'6" (1676mm) clear width between LED panel faces** [ASSUMED — minimum for 2 people to pass comfortably]

## Electrical & Thermal Loads (To Be Defined in B011)

### Electrical Load Estimate
| Component | Qty | Watts Each | Total Watts |
|-----------|-----|-----------|-------------|
| Back-wall display | 1 wall | — | **~600–1,000 W (COB) / ~400 W (projection)** — see Display Technology (B009) |
| Long-wall "window" displays (immersive installs) | TBD | — | **~800–1,000 W [ASSUMED — size/qty TBD]** — see Secondary "Window" Displays (B009/B010/B011) |
| Compute hardware | TBD | TBD | TBD |
| Audio amplifiers | TBD | TBD | TBD |
| Streaming/broadcast console | 1 | TBD | TBD |
| Camera system | TBD | TBD | TBD |
| Experience lighting | TBD | TBD | TBD |
| Container OS hardware | 1 | TBD | TBD |
| HVAC + ERV (chassis-provided) | 1 | TBD | TBD |
| **Total** | | | **TBD** |

### Thermal Load
- All electrical power eventually becomes heat
- Additional: audience body heat (10 people ≈ 4,500 BTU/hr — ~250 sensible + ~200 latent each, ASHRAE light activity)
- Chamber is sealed and dark — no solar gain through openings, no natural ventilation
- **Cooling is the dominant HVAC concern**, not heating (even in winter, internal heat generation exceeds losses in a passive house envelope)
- **Validated against chassis B005**: chassis provides **3 tons (36,000 BTU/hr)** cooling + **150 cfm** enthalpy-wheel ERV. Worst-case Content Node cooling load ≈ **29,200 BTU/hr (~2.4 tons)** — fits with margin.

> **⚠️ Binding cross-constraint — the 50A service caps the equipment load (chassis B005).** All studio equipment heat is rejected by the 3-ton AC, but the AC + ERV draw ~3,150 W from the *same* 50A/9,600 W-continuous service. After HVAC + ERV, **Content Node equipment (LED + compute + audio + lighting + control) must fit within ~6,450 W continuous** (~22,000 BTU/hr). The naive full-white LED draw (~14 kW) is physically unsupplied by the service — B011 must itemize the load to live within the power-and-thermal budget, or the LED walls must run dimmer/diverse. **The 50A service, not the HVAC tonnage, is the binding limit on studio brightness.** Reconcile in B011 and chassis B006.

## Studio / Experience Layout Options (To Be Defined in B012)

Three candidate layouts for the chamber, all within the same physical envelope:

### Option A: Broadcast Studio
- Fixed camera positions, talent area, LED backdrop walls
- Duration: continuous operation
- Capacity: 2-4 talent + crew
- Requires: pre-wired streaming console, ceiling camera grid, controlled lighting
- Primary use: Content Node's namesake function

### Option B: Immersive Corridor (Walk-Through)
- Audience moves linearly through the space between LED walls
- Duration: 5-8 minutes per session
- Capacity: 6-8 flowing through
- Requires: clear floor, guided path, possible one-way flow
- Chair/fixture requirements: none

### Option C: Immersive Theater (Seated)
- Audience seated in 1-2 rows, content on both walls
- Duration: 15-30 minutes
- Capacity: 8-10 seated
- Requires: chairs or bench seating within clear width between panels
- Seating depth budget: clear width minus 2× (panel depth + acoustic treatment + air gap)

### Layout Comparison
| Factor | Broadcast | Corridor | Theater |
|--------|-----------|----------|---------|
| Session duration | Continuous | 5-8 min | 15-30 min |
| Capacity | 2-4 | 6-8 | 8-10 |
| Revenue model | Production rental | Mid-price, mid-volume | Higher price, lower volume |
| Setup complexity | High (console, cameras) | Medium (path markers) | Medium (seating) |
| Use case | Content creation | Experiential marketing | Art/entertainment |
