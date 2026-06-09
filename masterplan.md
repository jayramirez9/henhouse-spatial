# Henhouse Spatial — Masterplan

## What This Is

Henhouse Spatial is the parametric design and simulation environment for the Henhouse mobile micro-venue platform. It models the physical chassis, validates fit-out configurations ("cartridges"), and simulates the building systems that Container OS will control in deployed venues.

The core insight: **the unit is a platform, not a product.** It's a hyper-efficient, Passivhaus-level, towable box on a flatbed trailer. What goes inside — a broadcast studio, a luxury green room, a VIP event suite, a cigar lounge — is a cartridge. The chassis doesn't know or care what's inside it. It provides structure, climate, and power. The cartridge provides purpose.

## The Vision

An operating system for physical space. A fleet of bespoke, towable micro-venues serving B2B clients and high-net-worth B2C customers. These units reject the bloated square-footage arms race of traditional Star Waggons in favor of extreme environmental control, acoustic perfection, and high-end material science.

## The Problem

Henhouse needs to design a single physical chassis that:
1. Meets passive house energy efficiency standards
2. Is towable by a heavy-duty pickup without a CDL
3. Provides excellent ventilation, heating, cooling, and acoustic isolation
4. Accepts multiple interior cartridge configurations without structural changes
5. Supports the most demanding cartridge (Content Node: LED panels, audio, compute, audience) without over-engineering the simplest (Sanctuary: a controlled, quiet box)

These constraints interact in non-obvious ways. Wall thickness affects interior width, which affects cartridge viability. Weight affects towability, which constrains material choices. HVAC capacity must handle Content Node's heat loads without being oversized for a Sanctuary deployment.

**Problem statement:** Henhouse needs a parametric model of the chassis that lets designers explore structural, thermal, and spatial tradeoffs — and validate that specific cartridge configurations satisfy their requirements within the chassis constraints.

## Who It's For

### Primary: Jay (Founder / Designer)
Needs to make design decisions about the chassis: wall assembly, structural system, HVAC sizing, electrical capacity. Needs to see how those decisions affect interior space, weight, cost, and cartridge compatibility.

**Success looks like:** Jay can change wall thickness, see the interior width change, check whether Content Node's LED panels still fit, and see the weight and R-value impact — all in one tool.

### Secondary: Fabrication Partners
When the design is locked, fabrication partners need precise dimensional drawings, material specs, and assembly sequences.

**Success looks like:** The parametric model exports construction-grade specifications that a fabricator can build from.

### Tertiary: Container OS (Machine Consumer)
The simulation defines what physical systems exist in the chassis — HVAC zones, electrical circuits, lighting fixtures, sensor locations. Container OS needs this to know what it's controlling.

**Success looks like:** The spatial model exports a system manifest that Container OS can import as its hardware map.

## Platform Architecture

### The Chassis Provides

| System | What the Chassis Gives Every Cartridge |
|--------|---------------------------------------|
| **Structure** | SIP shell on flatbed trailer frame. Load-bearing, weatherproof, road-legal. ISO corner castings for crane-off capability. |
| **Thermal envelope** | SIPs with mineral wool or rigid foam insulation. Passive house grade airtightness and thermal performance. |
| **Climate** | ERV (enthalpy wheel) for ventilation with 80% thermal energy recovery. HVAC system — heating, cooling, filtration. Ducted to configurable zones. |
| **Electrical** | 50A shore power primary. Panel and conduit oversized for future battery bank expansion. |
| **Entry** | At least one door with weather seal. Location and size per chassis spec. |
| **Floor** | Flat, level, load-bearing interior floor ready for cartridge finish. |

### The Chassis Does Not Provide

- Interior partition walls (cartridge specific)
- Interior finish surfaces (cartridge specific)
- Plumbing (not every cartridge needs it)
- Audio/visual infrastructure (cartridge specific)
- Network infrastructure beyond basic electrical (cartridge specific)
- Specific lighting (cartridge provides its own)
- Battery storage (future upgrade, space and conduit reserved)

### The Cartridge Interface

The chassis exposes a **cartridge interface** — a defined set of connection points, capacities, and spatial allowances that any configuration can use:

- Electrical connection points (location, capacity per circuit)
- HVAC register locations (supply and return)
- Structural mounting points (wall, ceiling, floor — with load ratings)
- Cable/conduit routing paths
- Interior clear dimensions (the buildable volume)

This is the spatial equivalent of an API. The chassis is the platform. The cartridge interface is the contract. The configuration is the consumer.

## Binding Constraints

### Transport (DOT Road-Legal, Pickup-Towable, No CDL)
- **Exterior width**: 8'0" (2438mm) — no oversize permit required
- **Exterior height**: 13'6" (4115mm) including trailer deck height — universal max, no state below this
- **Length**: 30' (9144mm)
- **Tow class**: Heavy-duty pickup or high-torque EV, no CDL required
- **Max tow weight**: ~14,000 lbs [ASSUMED — needs validation against specific truck + trailer ratings]

### Interior Clear Width
After SIP wall assembly (structure + insulation + interior surface), the usable interior width is approximately **6'8" (2032mm)**. This is THE binding spatial constraint for all cartridges. It determines:
- How many people can stand side-by-side
- Whether standard fixtures (appliances, furniture) fit
- LED panel sizing for Content Node
- Aisle width for accessibility [ASSUMED — ADA may require 36" clear aisle for commercial use]

### Passive House Performance Targets
- Airtightness: ≤0.6 ACH50 [ASSUMED — standard passive house requirement]
- Heating demand: ≤15 kWh/m²/year
- Total primary energy: ≤120 kWh/m²/year
- Thermal bridge free construction (SIPs inherently minimize bridging)

## Deployment Modes

### Mode A: Trailer-Locked
Unit remains on the flatbed trailer. Rapid weekend deployments, events, touring.
- Deploy: drive to site, level, connect shore power
- Strike: disconnect, drive away
- Best for: events, festivals, touring circuits

### Mode B: Architectural Drop
Unit craned or side-loaded off trailer via ISO corner castings. Long-term or permanent placement.
- Deploy: crane onto prepared site, connect utilities
- Best for: semi-permanent venues, ADU conversions, estate installations

## Cartridge Configurations

### 1. Content Node (Mobile Studio) — Most Demanding
Dead-silent, broadcast-ready environment for chaotic locations (festivals, paddocks, production sets).
- **Key features**: Room-within-a-room acoustic decoupling, pre-wired streaming console, multi-camera ceiling grid, silent HVAC
- **Drives chassis design**: highest acoustic, electrical, and thermal demands
- **Electrical load**: High — LED panels, compute hardware, audio, lighting
- **Thermal load**: High — equipment heat + audience body heat in sealed space
- **Acoustic requirement**: Highest — broadcast-grade silence

### 2. Sanctuary (High-Performance Green Room)
Biometric recovery and prep zone for talent and executives.
- **Key features**: Circadian-synced lighting, heated mobility floor deck, flush-mounted barista station
- **Electrical load**: Medium
- **Thermal load**: Low-medium
- **Acoustic requirement**: High — quiet, controlled environment

### 3. Pop-Up Sportsbook (Event Bar)
Ultimate VIP tailgating suite.
- **Key features**: Modular LED wall, integrated refrigeration/kegerators on native DC power
- **Deferred feature**: Hydraulic gull-wing wall (second-generation — major structural/weatherproofing complexity)
- **Electrical load**: Medium-high (refrigeration, LED, audio)
- **Thermal load**: Medium (variable — open-air mode changes everything)
- **Acoustic requirement**: Low

### 4. Heavy-Air Lounge (Cigar Club)
Localized negative-pressure environment for high-end cigar events.
- **Key features**: Commercial-grade HEPA and activated carbon scrubbers, negative pressure to prevent smoke bleed
- **Target venues**: Invited Clubs member tournaments, private estates
- **Electrical load**: Medium (scrubbers, HVAC)
- **Thermal load**: Medium
- **Acoustic requirement**: Medium
- **Special HVAC**: Negative pressure operation, high air change rate

## Success Criteria (Evals)

| Criteria | Measurement |
|----------|-------------|
| Parametric model is dimensional | Changing one input (wall thickness) cascades to all dependent values |
| Content Node fits | LED panels + audience + zones fit within chassis clear dimensions |
| Weight is towable | Total chassis weight (worst-case cartridge) is within pickup tow rating, no CDL |
| Passive house targets met | R-values, airtightness, thermal bridge analysis pass thresholds |
| Cartridge interface is clear | Any configuration can determine compatibility from the interface spec |
| HVAC handles worst case | Climate system sized for Content Node heat loads (then everything else is covered) |
| ERV maintains air quality | Fresh air with 80% thermal energy recovery in sealed operation |

## Future Upgrades (Designed-For, Not Built Yet)

These are explicitly deferred but the chassis design reserves space and routing for them:

### Sprint Power Architecture
- **LiFePO4 battery bank**: Floor-mounted, high-density. Space reserved in floor assembly.
- **V2L integration**: Plug into towing EV as secondary power source. Electrical interface reserved.
- **Series hybrid backstop**: Soundproofed micro-generator for off-grid. Mechanical space reserved.
- **Virtual power plant**: Fleet batteries sell power back to grid during peak demand when unrented.

### Hydraulic Gull-Wing Wall
- For Pop-Up Sportsbook cartridge. Structural reinforcement points reserved in chassis design.

### ADU Conversion Path
- "Trojan horse" market: rental clients who want to keep the unit permanently transition to purchase. Mode B (architectural drop) enables this. Plumbing rough-in may be needed for residential conversion.

## Fleet Operations (Future)

### FBO Hub
Centralized climate-controlled warehouse for fleet management: deep cleaning, HEPA filter swaps, Level 3 DC fast-charging turnarounds.

## Open Questions

- [ ] Wall assembly details: SIP panel thickness, core material (EPS vs polyiso vs XPS), skin material
- [ ] Trailer deck height? (Affects total height budget remaining for the box)
- [ ] Single or dual axle? (Affects weight capacity and towing dynamics)
- [ ] Tow vehicle class: 3/4-ton or 1-ton truck? Sets exact weight ceiling
- [ ] Does the chassis need to be self-leveling or does the cartridge handle site adaptation?
- [ ] ADA accessibility requirements for commercial deployments?
- [ ] Fire code / egress requirements for occupied commercial use?
- [ ] Which building code governs? (IRC, IBC, ANSI A119.5 for park trailers, or NFPA 501C?)
- [ ] First cartridge to build — which has the clearest path to revenue?
- [ ] Floor-mounted battery bank space reservation: how much volume to reserve?
