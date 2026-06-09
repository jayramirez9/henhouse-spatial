# Henhouse — Chassis Contract

> **Status**: Draft — B002-B007 will flesh out each section

## Overview

The chassis contract defines what the Henhouse platform provides to any cartridge configuration. It is the spatial equivalent of an API: the chassis is the platform, this contract is the interface, and cartridges are consumers.

A cartridge configuration can validate compatibility by checking its requirements against this contract. If every requirement maps to a chassis provision, the configuration fits.

## Design Principles

1. **Configuration-agnostic.** The chassis doesn't know what goes inside it. It provides structure, climate, and power.
2. **Worst-case sized.** Systems are sized for the most demanding cartridge (Content Node). Simpler configurations use a subset of capacity.
3. **Interface-defined.** Connection points, mounting points, and capacities are explicitly specified. A cartridge designer knows exactly what's available without guessing.
4. **Future-proofed.** Space and conduit reserved for battery bank, V2L, and generator — even though unit #1 ships with shore power only.
5. **Prototyping reveals constraints.** Where a value is assumed rather than validated, it's marked `[ASSUMED]`. Prototyping will confirm or correct.

## Locked Decisions

These decisions are made. They constrain everything downstream.

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Exterior width | 8'0" (2438mm) | No oversize permit, any route, any time. Fleet logistics. |
| Exterior height | 13'6" (4115mm) | Universal max — no state below 13'6" on Interstate. Every inch counts for interior height. |
| Length | 30' (9144mm) | Maximum volume within pickup-towable range |
| Shell construction | SIPs | Structure + insulation in one. Good R-value, fast assembly, minimal thermal bridging. Proven supply chain. |
| Insulation | GPS (graphite EPS) SIP core, **FRP skins** | VIPs deferred — cost prohibitive for unit #1. 6½" GPS walls = R-28 at the 6'8" width target; thicker roof/floor for more R. FRP skins (not OSB) chosen for weight — see Weight Strategy. (B003) |
| Ventilation | ERV with enthalpy wheel | Essential for sealed passive house box. 80% thermal energy recovery. $2-5K, non-negotiable. |
| Primary power | 50A shore power (120/240V split phase) | Covers all cartridge loads. Panel + conduit oversized for future battery expansion. |
| Deployment | ISO corner castings on frame | Cheap to include. Enables Mode A (trailer-locked) and Mode B (crane-off for permanent drops). |
| Frame material | **Aluminum** | Saves ~1,500–2,000 lbs vs steel — required to keep all cartridges (incl. Content Node) under the no-CDL ceiling. (Weight Strategy, 2026-06-09) |
| Towing class | **No-CDL, fleet-wide** | GCWR ≤26,000 lbs for every cartridge — any licensed driver tows any unit. Locked goal; drives the aluminum-frame + FRP-skin spend. (Weight Strategy, 2026-06-09) |

## Exterior Envelope (B002)

### Transport-Legal Dimensions

| Dimension | Value (imperial) | Value (metric) | Source / Notes |
|-----------|-----------------|----------------|----------------|
| Exterior width | 8'0" (96") | 2438mm | Federal no-permit max on all roads. Interstate allows 102" but local/state roads may not. 8'0" chosen for universal deployability. |
| Exterior height | 13'6" (162") | 4115mm | Universal maximum — de facto national standard. No state below 13'6" on Interstate. Height includes trailer deck + box. |
| Length | 30'0" (360") | 9144mm | Practical max for pickup-towable. Standard gooseneck trailer territory. |

### Height Budget

The height budget is the critical calculation: total allowed height minus trailer deck height determines how tall the box can be. Interior clear height then subtracts floor and roof assembly thickness.

| Scenario | Standard deck | Low-profile deck |
|----------|--------------|-----------------|
| Total height limit | 162" (13'6" / 4115mm) | 162" (13'6" / 4115mm) |
| Trailer deck height | 26" (660mm) | 20" (508mm) |
| **Box build height** | **136" (11'4" / 3454mm)** | **142" (11'10" / 3607mm)** |
| Floor SIP (6½", B003) | 6.5" (165mm) | 6.5" (165mm) |
| Roof SIP (8¼", B003) | 8.25" (210mm) | 8.25" (210mm) |
| **Interior clear height** | **~121" (10'1" / 3080mm)** | **~127" (10'7" / 3232mm)** |

> **Refined in B003**: B002 placeholder floor/roof assemblies (~3"/~4") were optimistic. SIP floor (6½") and roof (8¼") are thicker, dropping interior clear height ~8" from the B002 estimate. **Both scenarios still meet the 9–10' target** — low-profile deck (10'7") comfortably, standard deck (10'1") with margin. Roof can flex thinner (6½", recovering ~1.75" of height) if more headroom is wanted at the cost of roof R-value.

**Recommendation**: Target a low-profile deck (20") to maximize interior volume. The 6" difference compounds across every cartridge use case — more headroom for LED panels, camera grid clearance, acoustic treatment at ceiling, and general human comfort in an enclosed space.

**Open question**: Exact deck height depends on trailer manufacturer and configuration. The two scenarios above bracket the likely range. Final number locks when a trailer is selected or spec'd for custom fabrication.

### Trailer Configuration

| Parameter | Value | Notes |
|-----------|-------|-------|
| Hitch type | Gooseneck / 5th-wheel | Required at 30' for towing stability. Bumper-pull not viable at this length. |
| Axle configuration | Dual axle | Required for weight capacity and stability |
| Target GVWR | 14,000 lbs (no-CDL) | Achievable for all cartridges with aluminum frame + FRP skins. Chassis ~8,250 lbs leaves ~5,750 lbs cartridge allowance. (Weight Strategy, 2026-06-09) |
| Tongue/pin weight | ~20% of loaded trailer weight | Standard for gooseneck. At 12,000 lbs loaded = ~2,400 lbs pin weight. |
| Brakes | Electric brakes on both axles | Required above 10,000 lbs GVWR in all states |
| Frame | **Aluminum** | Saves ~1,500–2,000 lbs vs steel. More expensive (~+$8–15K/unit) but required to keep Content Node under the no-CDL ceiling (Weight Strategy). Lift sub-frame for Mode B castings also aluminum. |
| ISO corner castings | 4× on frame | Enables crane-off (Mode B deployment). Low cost, high option value. |

### Weight Budget

| Component | Weight estimate | Notes |
|-----------|----------------|-------|
| Trailer frame + running gear | ~3,750 lbs (1701 kg) | **Aluminum** frame, dual axle, gooseneck (saves ~1,500–2,000 lbs vs steel). Includes Mode-B aluminum lift sub-frame. [ASSUMED — verify against actual trailer spec] |
| SIP shell (walls + roof) | ~2,450 lbs (1111 kg) | 6½" GPS walls (~815 sq ft @ ~2.3 psf) + 8¼" GPS roof (240 sq ft @ ~2.4 psf), **FRP skins**. (B003 + Weight Strategy) |
| Floor assembly | ~550 lbs (249 kg) | 6½" FRP-skinned SIP over trailer deck, 240 sq ft @ ~2.3 psf. |
| Finish + openings | ~900 lbs (408 kg) [ASSUMED] | Entry door, any glazing, interior thermal/ignition barrier, sealing. **No separate exterior cladding — FRP gel-coat skin is the finished exterior.** Refine in B004/B007. |
| ERV unit | TBD | (B005) |
| HVAC system | TBD | (B005) |
| Electrical system | TBD | (B006) |
| **Envelope subtotal** | **~3,900 lbs** | FRP SIP shell + floor + finish/openings. **Before any mechanical/electrical systems.** |
| **Chassis subtotal** | **~8,250 lbs** (incl. ~600 lbs systems est.) | Frame + envelope + ERV/HVAC/electrical (firms up B005/B006). |
| **Cartridge allowance @ 14K** | **~5,750 lbs** | GVWR minus chassis. **Content Node (~3,000–5,000 lbs) fits with ~750–2,750 lbs margin.** |
| | | |
| **Trailer GVWR** | **14,000 lbs (no-CDL)** | Achievable for all cartridges including Content Node. (Weight Strategy) |
| **Payload capacity** | **~10,250 lbs** | GVWR (14,000) minus aluminum frame (3,750). Comfortable for the envelope + systems + any cartridge. |

### ✅ Weight Strategy — RESOLVED (2026-06-09)

The B003 weight finding surfaced a binding constraint; this is the decision that resolves it. **Decision: universal no-CDL, fleet-wide, via aluminum frame + FRP skins.** (Jay, 2026-06-09.)

```
ORIGINAL PROBLEM (steel frame + OSB skins):
  Frame 5,500 + envelope 6,400 = 11,900 lbs before systems
  → only ~1,500 lbs left for Content Node at 14K GVWR → INFEASIBLE

RESOLVED (aluminum frame + FRP skins):
  Frame 3,750 + envelope 3,900 + systems ~600 = ~8,250 lbs chassis
  → ~5,750 lbs cartridge allowance at 14K GVWR
  → Content Node (~3,000–5,000 lbs) FITS, ~750–2,750 lbs margin
```

**What changed:** frame steel → aluminum (−~1,750 lbs); skins OSB → FRP (−~1,580 lbs); FRP gel-coat eliminates separate exterior cladding (−~700 lbs). Net ~4,250 lbs recovered.

**Cost accepted:** ~+$20–35K/unit (aluminum frame ~+$8–15K, FRP-skinned panels ~+$12–20K vs OSB). The deliberate trade: spend on the build to keep *any licensed driver able to tow any unit*, avoiding CDL/hauler logistics across the fleet.

**Downstream consequences to honor:**
- B004 structural numbers are OSB-based (Premier ESR-4524) — **restate from the FRP-panel supplier's ratings**; mounting method (embedded backing) is unchanged.
- FRP fire rating: interior thermal/ignition barrier required for occupied commercial use (open regulatory question).
- Less shell acoustic mass → more interior acoustic mass for Content Node (B010); the ~5,750 lbs allowance covers it.
- Mode B (crane-off) is **retained** — the freed budget makes the aluminum lift sub-frame affordable.

### CDL Avoidance Math

| Vehicle | GVWR | Notes |
|---------|------|-------|
| Tow vehicle (1-ton pickup) | ~12,000 lbs | Ford F-350 / Ram 3500 / Chevy 3500 class |
| Trailer | 14,000 lbs | Target GVWR |
| **GCWR** | **~26,000 lbs** | At the CDL threshold. If either vehicle is rated higher, CDL triggers. Must verify exact ratings. |

Federal CDL required when GCWR exceeds 26,000 lbs **and** towed vehicle GVWR exceeds 10,000 lbs. Both conditions apply here, so GCWR must stay at or below 26,000 lbs.

**Risk**: 14,000 lb trailer GVWR + 12,000 lb truck GVWR = 26,000 exactly. Zero margin. If payload pushes actual weight beyond ratings, or if a higher-rated truck is used, CDL triggers. Consider whether 12,000 lb GVWR trucks actually exist at 1-ton class (many are rated higher). This needs verification against specific truck models.

> **Status after Weight Strategy (2026-06-09)**: The **payload** side is resolved — aluminum frame + FRP skins keep actual loaded weight comfortably under the 14,000 lb trailer GVWR (~5,750 lbs cartridge allowance). **The GCWR-rating side is a separate, still-open item**: CDL keys off *rated* GVWRs, not actual weight, so non-CDL requires a tow vehicle whose GVWR + 14,000 ≤ 26,000 (i.e. truck GVWR ≤ ~12,000 lbs). Many 1-ton trucks are rated above that. **Open: identify specific ≤12,000 lb GVWR tow vehicles, or accept that the truck choice — not the build — becomes the binding no-CDL constraint.**

### Deployment Modes

**Mode A — Trailer-Locked (Rapid Deployment)**
- Unit remains on flatbed trailer
- Deploy: drive to site, level with trailer jacks, connect shore power
- Strike: disconnect power, retract jacks, drive away
- Typical use: events, festivals, weekend deployments, touring circuits
- Floor height above ground: deck height + floor assembly (~23-29" depending on trailer)
- Access: requires steps or ramp at entry door

**Mode B — Architectural Drop (Long-Term Placement)**
- Unit craned or side-loaded off trailer via ISO corner castings
- Deploy: crane onto prepared pad/foundation, connect utilities
- Trailer drives away — reusable for next unit
- Typical use: semi-permanent venues, estate installations, ADU conversions
- Floor height: at grade or on low foundation (much better accessibility)
- Requires: crane access at site, prepared landing pad, utility connections at pad

### Dimensional Summary

```
                          ← 30'0" (9144mm) →
                    ┌─────────────────────────────┐
                    │                             │ ↑
                    │         BOX ON DECK         │ 136-142"
                    │                             │ (11'4"-11'10")
    13'6" ──────── │                             │ ↓
    (4115mm)       ├─────────────────────────────┤ ↑
    total          │    TRAILER DECK + FRAME     │ 20-26"
                   └──┤                       ├──┘ ↓
                      ●─────────────────────●
                    axle                   axle

                    ← 8'0" (2438mm) exterior width →

    Interior clear: ~6'8" wide × ~10'9"-11'3" tall
    (exact width depends on SIP thickness — B003)
    (exact height depends on deck + assembly — lock with trailer selection)
```

## Wall Assembly (B003)

### Selected: SIPs (Structural Insulated Panels), GPS core, OSB skins

SIPs selected over wood stud + mineral wool and over composite/VIP options. Rationale: structure + insulation integrated, minimal thermal bridging, fast assembly, proven supply chain.

All R-values, U-factors, and weights below are from Premier SIPS published technical data (EPS and GPS cores, 7/16" OSB facings). Other manufacturers (Insulspan, FischerSIPS, ACME) are within a point of these. Values confirm vendor-quote-grade once a manufacturer is selected.

### Core Material: EPS vs GPS vs Polyiso

| Core | R per inch (@75°F) | Relative cost | Notes |
|------|-------------------|---------------|-------|
| EPS (standard white) | ~3.85 | Baseline | Proven, cheapest, stable R (no thermal drift). Most common SIP core. |
| **GPS (graphite EPS / Neopor) [SELECTED]** | **~4.3** | +10–20% | ~22% more R at identical thickness. Same panel, same weight, same width — buys R-value for free in the width budget. |
| Polyiso | ~5.6–6.5 (drifts down cold) | +30–50% | Highest R per inch but R drops in cold weather (worst case at design temps), costlier, less common as a structural SIP core. Rejected. |

**Decision**: GPS core. In a unit where interior width is the binding constraint, the lever that matters is **R-value per inch of wall thickness**. GPS delivers ~22% more R than EPS at the same thickness, weight, and cost-per-pound — so it buys thermal performance without spending width or payload. Polyiso's cold-weather R-drift makes it the wrong call for a unit that must hold passive-house performance at design temperature.

### Skin Material: FRP / Fiberglass [SELECTED]

| Skin | Weight (per facing) | Notes |
|------|--------------------|-------|
| **FRP / fiberglass [SELECTED]** | ~0.7–1.0 psf | Lighter (~half of OSB), moisture-proof, road-durable, and the gel-coat exterior face *is* the finished weatherproof skin — no separate cladding needed. The weight lever that makes universal no-CDL achievable (Weight Strategy). |
| 7/16" OSB | ~1.4 psf | Standard structural SIP facing — cheapest, proven, ICC-ES rated (ESR-4524). Rejected on weight: ~+1,580 lbs vs FRP across the shell, which pushes Content Node over the no-CDL ceiling. |
| Steel-faced (IMP-style) | ~1.0–1.4 psf | Finished, durable exterior. Heavier than FRP; structural mounting differs. |
| MgO board | heavier | Fireproof, mold-proof, but brittle under road vibration. |

**Decision**: FRP skins, fleet-wide. Lighter, weatherproof, finished — directly serves the Weight Strategy decision (universal no-CDL).
> **Caveats introduced by FRP skins** (track into B004 and prototyping):
> - **Structural data changes.** Premier's load charts (used in B004) are OSB-faced (ESR-4524). FRP-skinned SIP capacities differ and must come from the **FRP-panel supplier's own ratings** (transport-body / cold-storage / expedition-vehicle panel makers serve this market). The qualitative B004 conclusion (shell grossly over-strong; mounting is the real problem) almost certainly still holds, but the specific plf/psf numbers are OSB-based and need restating once a supplier is chosen.
> - **Fire rating.** FRP needs a thermal/ignition barrier on the interior for occupied commercial use — verify against code (open regulatory question).
> - **Less acoustic mass.** FRP skins give less mass-law isolation than OSB, shifting more of the "Taycan-quiet" burden onto Content Node's interior room-within-a-room (B010). The freed weight budget (~5,750 lbs cartridge allowance) covers the added interior acoustic mass.

### Panel Thickness: Walls 6½" GPS, Roof 8¼" GPS, Floor 6½"

Thickness trades **R-value against the dimension that is scarce for each surface**:
- **Walls** trade against interior **width** (binding constraint) → keep thin, use GPS to recover R.
- **Roof and floor** trade against interior **height**, where B002 shows a surplus (10'+ vs 9–10' target) → go thicker for R.

Wall thickness options (assembly = SIP + 0.5" exterior cladding + 0.5" interior finish per side; ×2 off the 96" exterior):

| Wall SIP | Nominal | R-value @75°F (EPS / **GPS**) | Weight | Per-side assembly | Interior clear width |
|----------|---------|------------------------------|--------|-------------------|----------------------|
| 4½" | 114mm | 15 / **18** | 3.3 psf | 5.5" (140mm) | 85" = **7'1"** (2159mm) |
| **6½" [SELECTED]** | **165mm** | **23 / 28** | **3.5 psf** | **7.5" (191mm)** | **81" = 6'9" (2057mm)** |
| 8¼" | 210mm | 30 / **36** | 3.7 psf | 9.25" (235mm) | 77.5" = **6'5.5"** (1969mm) |

**Decision**: 6½" GPS walls → **R-28**, interior clear width **~6'9" (2057mm)**. This recovers the original ~6'8" target *with a little margin*. Going to 8¼" walls (R-36) would cost ~3.5" of interior width — unacceptable for Content Node, which needs every inch for LED panels + acoustic treatment. Going to 4½" (R-18) buys 4" of width but sacrifices a third of the wall R-value; the GPS 6½" is the better balance.

> **Design target stays 6'8" (2032mm).** As-built is ~6'9", but cartridges should design to 6'8" to absorb finish tolerances, fastener stand-off, and field variance. The extra inch is margin, not buildable space.

**Roof**: 8¼" GPS SIP → **R-36**. Trades against height surplus. Can flex 6½"–10¼" (R-28 to R-45) to trade height-margin against roof R-value.
**Floor**: 6½" SIP over the trailer deck → **R-23**. The steel deck provides structure; the SIP adds insulation and the interior walking surface. Underside is road-exposed, so floor R matters.

### Assembled R-Values (Envelope)

| Surface | Assembly | R-value | Passive-house context |
|---------|----------|---------|----------------------|
| Walls | 6½" GPS SIP | R-28 | Continuous insulation, near-zero thermal bridging. Below a cold-climate PH wall target (R-40+) but strong for a sub-100 sq ft footprint with this surface-to-volume ratio. |
| Roof | 8¼" GPS SIP | R-36 | Good. Can increase to R-45 (10¼") using height surplus if energy modeling demands. |
| Floor | 6½" SIP | R-23 | Adequate over a ventilated/road-exposed underside; verify against cold-floor comfort. |

[ASSUMED] Passive-house *certification* is not yet energy-modeled — these R-values are envelope inputs, not a verified PH result. PHPP/WUFI modeling is a later build (E03 thermal calc, B016). The SIP envelope's value is continuous insulation and airtightness, not headline R alone.

### Weight per Linear Foot (Walls)

With **FRP skins** (~2.3 psf assembled) and an ~11' wall panel height: **~25 lbs per linear foot** of wall, per side (vs ~38.5 plf with OSB skins). The full envelope weight is in the Weight Budget below.

> **Key weight insight: SIP weight is skin-driven, not core-driven.** Panel weight is dominated by the facings, not the light foam core, so it barely changes with thickness — choose wall thickness for R-value and width, *not* weight. **The weight lever is the skin material**, and the Weight Strategy decision (2026-06-09) pulled it: OSB → FRP, saving ~1,580 lbs across the shell and making universal no-CDL achievable.

> Note: the 3.3 / 3.5 / 3.7 psf figures in the thickness table above are Premier's **OSB-faced** values. FRP-faced assemblies run ~2.1–2.4 psf — get exact numbers from the FRP-panel supplier.

### Cost Estimate [ASSUMED — vendor quote pending]

| Item | Rough cost |
|------|-----------|
| FRP-skinned GPS SIP panels (walls + roof + floor, ~1,295 sq ft @ ~$18–25/sq ft) | ~$23,000–32,000 |
| Splines, connectors, CNC cuts for openings, sealants, shipping | ~$3,000–6,000 |
| **SIP shell package** | **~$26,000–38,000** |

The FRP-skin + aluminum-frame choice (Weight Strategy) adds roughly **+$20–35K/unit** over an OSB-skin/steel-frame build — the accepted cost of universal no-CDL. FRP-skinned panels run materially higher than OSB ($18–25 vs ~$11/sq ft); the gel-coat exterior offsets some by eliminating separate cladding.

### Width Budget
```
Exterior width:                      8'0"   (96" / 2438mm)
Minus exterior cladding (× 2):      -1.0"   (0.5" per side)
Minus 6½" GPS SIP (× 2):           -13.0"
Minus interior finish (× 2):        -1.0"   (0.5" per side)
═══════════════════════════════════════════════════════════
Interior clear width (as-built):    81"    (6'9" / 2057mm)
Cartridge design target:            80"    (6'8" / 2032mm)  ← design to this
```

## Structural Grid (B004)

Structural capacities below are from Premier SIPS Load Charts (Rev. Feb 2025), ICC-ES recognized under **ESR-4524**, compliant with 2015/2018/2021 IBC & IRC. Final design requires sign-off by a licensed engineer (the manufacturer's charts cover static building loads, not the transport-dynamic case — see Road-Dynamic Loads below).

> **FRP-skin caveat (Weight Strategy, 2026-06-09):** the numbers in this section are for **OSB-faced** SIPs (ESR-4524). The fleet now uses **FRP-skinned** panels, whose capacities differ — **restate the specific plf/psf values from the FRP-panel supplier's ratings.** The qualitative conclusion (shell grossly over-strong; *local mounting* is the real problem) holds regardless of skin, and the mounting method below (embedded backing, never bare skin) is unchanged — FRP skins, like OSB, won't hold heavy fasteners.

> **Headline finding (B004): the SIP shell is grossly over-strong for this box; the real engineering problem is *local mounting*.** Gross panel capacity exceeds demand by ~15–17×. But the foam core has zero fastener-holding capacity and the 7/16" OSB skin has low withdrawal strength, so **every heavy cartridge load (LED panels, camera grid, rigging) must be pre-planned to land on embedded lumber, not on bare panel.** The structural grid is therefore defined as a map of **where solid backing exists**, not as a stud-spacing schedule.

### Panel & Seam Layout

- **Panel size**: SIPs are available up to 8' × 24'. Use the largest panels practical to minimize seams — long walls run as full-height panels (~11' tall × up to 24' long), so a 30' wall is ~2 panels plus seam. Fewer seams = fewer thermal/air-leak paths and fewer mounting discontinuities.
- **Seams are joined by splines**, and the spline *type* is a structural design lever:

| Spline | Construction | Structural role | Thermal | Use in this chassis |
|--------|-------------|-----------------|---------|---------------------|
| **Type S** (surface spline) | Two 3"-wide OSB strips, nailed through both skins | Connection only | No bridge | Default for all seams that are purely connections |
| **Type L** (lumber spline) | No.2 Hem-Fir 1½"-wide, depth = core, ≥2 members per 48" | Carries concentrated load; serves as a **mounting backer** | Minor thermal bridge | **Place deliberately at LED-rail heights and camera-grid anchor lines** so mounting hardware lands on solid lumber |
| **Type I** (insulated I-spline) | OSB I-section in foam | Structural, low bridge | Near-zero bridge | Roof seams needing structural continuity without bridging |

> **Design principle**: use Type S everywhere by default (preserves the thermal envelope), and Type L *only* on the lines where the cartridge will mount weight. This is the cheapest way to get hard points without bridging the whole envelope.

### Load Paths

**Gravity (Mode A — on trailer):**
```
Roof SIP (8¼") → wall top plate (2× cap plate) → wall panels (axial) →
wall bottom plate → SIP floor → trailer steel deck → frame → axles + gooseneck → tow vehicle
```
Wall axial demand vs. capacity (the over-strength margin):

| | Value |
|---|---|
| Roof dead (8¼" @ 3.7 psf, 4' tributary) | ~15 plf |
| Roof live/snow [ASSUMED 30 psf design] | ~120 plf |
| Ceiling-hung cartridge load (camera grid etc., ~900 lb / 16') | ~56 plf |
| **Estimated wall axial demand** | **~190 plf** |
| **6½" GPS wall capacity @ 12' (Type S, Load Chart #1A)** | **3,373 plf** |
| **Margin** | **~17×** |

Axial point-load capacity (concentrated roof loads): single 2× plate **2,040 lb**, with cap plate **4,678 lb** (Load Chart #2A) — far above any cartridge point load.

**Lift (Mode B — crane-off via ISO castings):**
The road running gear (axles, hitch) stays for transport; the box is craned off, so the 4 ISO corner castings must tie into an **integral steel base sub-frame** that is both the structural floor and the lift interface. The box lifts as a rigid unit on this sub-frame.
> **⚠️ Flag — Mode B costs weight.** An integral lift sub-frame + corner castings adds steel that lands in the [[Weight Finding]] budget. Given weight is the binding constraint, **question whether Mode B (crane-off) earns its weight penalty for unit #1**, or whether it's deferred like the battery bank. Quantify the sub-frame weight before committing. Connects to the no-CDL weight fork.

**Road-dynamic loads (the non-standard case):**
Towing imposes vibration, racking, and dynamic amplification (bumps ≈ 2–3g vertical) that static building codes don't address. The SIP shell is a stressed-skin **diaphragm** — inherently strong in racking/shear (Load Charts #4A/B), which is good. But **seams and mounting points see fatigue that a stationary building never does.**
> [ASSUMED] Design seams and all mounting hardware to a transport/fatigue factor, not just IBC static. This is outside the manufacturer's chart scope — **prototype and instrument before fleet production.**

### Mounting Grid (Cartridge Interface)

The chassis provides these **hard points**. Cartridges must mount weight only to hard points, never to bare panel.

| Surface | Provision | Capacity | Notes |
|---------|-----------|----------|-------|
| **Walls (LED panels)** | Continuous horizontal ledgers/rails through-bolted to embedded **Type L lumber splines** at defined heights (e.g., ~24" and ~96" AFF) | Design to **≥10 psf** hung load per wall (covers LED cabinets ~5–7 psf + rail + service) | LED cabinets ~18 lb each; a 16'×~9' wall ≈ 500–900 lb distributed. **Never fasten LED rails to bare OSB.** |
| **Ceiling (camera grid, lighting, rigging)** | Integral grid (Unistrut/aluminum) anchored to embedded lumber splines or cross-members spanning the 8' width | Rated hard points each **≥250 lb** [ASSUMED]; total ceiling-hung ≤ ~900 lb | Point loads cannot hang from bare roof OSB — embedded backing required at every anchor. |
| **Floor (audience, equipment)** | SIP floor over the trailer steel deck | **≥100 psf** assembly live load (IBC 1607.1) | The **steel deck is the real structural floor**; SIP floor adds insulation + walking surface + diaphragm. Equipment-rack point loads bear through to the deck. |

**Fastener rule**: fasteners must penetrate OSB skin ≥¼"; bare-OSB withdrawal is low (see Premier withdrawal tables for 7/16"/⅝"/¾"). Any load above light-duty requires embedded lumber/LVL or a Type L spline at the mount line.

> The mounting grid coordinates (exact ledger heights, ceiling hard-point spacing) are finalized in **B007 (cartridge interface)** once Content Node's LED and camera layouts are fixed (B009). B004 establishes the *method*: pre-planned embedded backing at mapped locations.

## HVAC System (To Be Defined in B005)

### Ventilation: ERV with Enthalpy Wheel (Locked)
- Fresh air with ~80% thermal energy recovery
- Required for sealed passive house operation
- Maintains indoor air quality without sacrificing thermal performance
- CO2 monitoring: yes (required for occupied commercial space)

### Sizing Basis: Content Node Worst Case
- LED panel heat generation: TBD BTU/hr
- Audience body heat (10 people): ~4,000 BTU/hr [ASSUMED — ~400 BTU/hr per person]
- Compute hardware heat: TBD BTU/hr
- Audio amplifier heat: TBD BTU/hr
- **Total cooling load**: TBD BTU/hr

### Special Consideration: Heavy-Air Lounge
- Negative pressure operation requires higher air change rate
- HEPA + activated carbon filtration is cartridge-provided, but chassis HVAC must support the airflow volume
- Size ductwork to accommodate this even if Content Node is the thermal worst case

### Zone Layout
- TBD — dependent on whether zones are chassis-defined or cartridge-defined
- Minimum: one supply register and one return per cartridge zone
- HVAC register locations are part of the cartridge interface

## Electrical System (To Be Defined in B006)

### Shore Power (Locked: 50A)
- Connection: 50A (120/240V split phase)
- Standard US RV/trailer park compatible
- 12,000W continuous capacity

### Future Battery Expansion (Designed-For)
- Floor space reserved for LiFePO4 rack
- Conduit oversized for battery interconnect
- Transfer switch location reserved in panel
- V2L inlet reserved (EV truck connection)

### Distribution
- Main panel: TBD amp rating (oversized for future battery)
- Circuit count: TBD
- Dedicated circuits for: HVAC, ERV, cartridge general, cartridge high-load, lighting, control systems

### Connection Points (Cartridge Interface)
- Location and rating of each available circuit at cartridge boundary
- TBD — defined in B006 and formalized in B007

## Cartridge Interface (To Be Defined in B007)

This is the key deliverable — the "API" between chassis and cartridge.

### What the Interface Specifies
- **Clear interior volume**: length × width × height of the buildable space
- **Electrical connection points**: location, circuit number, amperage, voltage
- **HVAC register locations**: supply and return positions, CFM capacity per register
- **Structural mounting grid**: wall, ceiling, and floor mounting points with load ratings
- **Cable routing paths**: chase locations for running cartridge wiring
- **Entry point(s)**: door location, clear opening dimensions
- **Floor**: surface type, load rating, level tolerance
- **Battery bay**: reserved volume and connection point for future expansion

### Interface Rules
1. Cartridge must not exceed total electrical capacity
2. Cartridge must not exceed structural mounting load ratings
3. Cartridge must not block HVAC/ERV airflow paths
4. Cartridge must maintain minimum clearance to entry/egress
5. Cartridge must not penetrate the thermal envelope
6. Cartridge total weight must not exceed weight allowance (total tow weight minus chassis weight)
