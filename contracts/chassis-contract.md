# Henhouse — Chassis Contract

> **Status**: Draft — B002–B006 complete; B007 will compile the cartridge interface

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
| Exterior width | **8'6" (102" / 2591mm)** | Georgia's statewide legal max — **no oversize permit** for GA-local delivery [ASSUMED — pending GDOT confirmation]. Buys +6" interior over 8'0" while keeping R-28 walls. Trades the universal "any state, any road" margin for the wider box; 12'-lane caveat on narrow final approaches. (D002, 2026-06-16) |
| Exterior height | 13'6" (4115mm) | Universal max — no state below 13'6" on Interstate. Every inch counts for interior height. |
| Length | 30' (9144mm) | Maximum volume within pickup-towable range |
| Shell construction | SIPs | Structure + insulation in one. Good R-value, fast assembly, minimal thermal bridging. Proven supply chain. |
| Insulation | GPS (graphite EPS) SIP core, **FRP skins** | VIPs deferred (see Wall Assembly → VIP note) — not just cost: the cooling load is power-capped, so envelope R barely binds. 6½" GPS walls = R-28 at the 7'2" width target; thicker roof/floor for more R. FRP skins (not OSB) chosen for weight — see Weight Strategy. (B003) |
| Ventilation | ERV with enthalpy wheel, ~150 cfm | Essential for sealed passive house box. 80% thermal energy recovery. Sized for 10-occupant CO2 control (not just code minimum). $2-5K, non-negotiable. (B005) |
| Supplemental HVAC | 3-ton (36,000 BTU/hr) variable-capacity ducted mini-split heat pump | Cooling governs (LED/equipment heat); inverter mandatory for the empty-box→full-studio turndown. Cooling load is power-capped by the 50A service, which self-sizes this at 3 tons. (B005) |
| Primary power | 50A shore power (120/240V split phase) | **12,000 W nameplate / 9,600 W continuous** (NEC 80%). HVAC+ERV reserve ~3,150 W first → **~6,450 W continuous for the cartridge.** 100A busbar + EMS load-shed (HVAC/control protected) + reserved ATS/conduit for future battery/V2L. The service is a hard ceiling on studio brightness/volume. (B006) |
| Deployment | ISO corner castings on frame | Cheap to include. Enables Mode A (trailer-locked) and Mode B (crane-off for permanent drops). |
| Frame material | **Aluminum** | Saves ~1,500–2,000 lbs vs steel — required to keep all cartridges (incl. Content Node) under the no-CDL ceiling. (Weight Strategy, 2026-06-09) |
| Towing class | **No-CDL, fleet-wide** | GCWR ≤26,000 lbs for every cartridge — any licensed driver tows any unit. Locked goal; drives the aluminum-frame + FRP-skin spend. (Weight Strategy, 2026-06-09) |

## Exterior Envelope (B002)

### Transport-Legal Dimensions

| Dimension | Value (imperial) | Value (metric) | Source / Notes |
|-----------|-----------------|----------------|----------------|
| Exterior width | 8'6" (102") | 2591mm | Georgia's statewide legal max (O.C.G.A. § 32-6-23) — no oversize permit for GA-local delivery [ASSUMED — pending GDOT confirmation]. Was 8'0"/96" (universal federal no-permit) until D002 adopted 102" for +6" interior. See Regulatory: Transport Width below. |
| Exterior height | 13'6" (162") | 4115mm | Universal maximum — de facto national standard. No state below 13'6" on Interstate. Height includes trailer deck + box. |
| Length | 30'0" (360") | 9144mm | Practical max for pickup-towable. Standard gooseneck trailer territory. |

### Regulatory: Transport Width (D002, 2026-06-16)

**Working basis [ASSUMED — pending GDOT permit-office confirmation].** Georgia's statewide legal maximum vehicle/load width is **102 inches (8'6")** under **O.C.G.A. § 32-6-23** — on *all* public roads, not only Interstates (web-sourced, not yet confirmed with GDOT). On that basis, at or under 102" **no oversize/width permit is required** anywhere in Georgia, including local delivery in **Atlanta, Fayetteville, Peachtree City, and Newnan**; over 102" triggers an oversize permit (§ 32-6-28). **Confirm with the GDOT permit office before relying on this for a booked delivery.**

**The one operational catch — the 12-foot-lane rule.** A 102"-wide vehicle may only travel on roads with **12-foot travel lanes**. Highways and arterials (I-75/85, US-29, GA-74/85/54/34) qualify; the risk is the **final approach** — residential streets, rural Coweta/Fayette connector roads, event-site driveways/lots that may have narrower lanes. This is a **per-venue route check**, not a statewide blocker.

**Fine print.**
- 102" is the *load* width; mirrors/safety devices are excluded, but trim, skins, or awnings that push the *box itself* past 102" tip into permit territory — **build to 102" with margin, not exactly 102".**
- This is the GA statute as of 2026-06; for fleet ops, confirm with the **GDOT permit office** and check posted local bridge/lane restrictions per route. [ASSUMED — not re-verified per delivery]

**Decision (D002).** Adopt **8'6" (102")** exterior width for the GA-metro fleet. The +6" of exterior goes straight to interior width (now ~7'3" as-built / 7'2" design vs. 6'9"/6'8" at 8'0"), **with walls unchanged at 6½" GPS SIP (R-28 retained)** — so the width win costs no thermal performance, unlike the alternative of thinning walls. The accepted trade is the **loss of the universal "any state, any road" margin** that 8'0"/96" gave: 102" is permit-free in Georgia and most states, but a few jurisdictions cap local roads at 96", so out-of-state delivery is no longer guaranteed permit-free. Justified by the Atlanta-south-metro local delivery model.

**Open item.** Validate **12-foot-lane / final-approach clearance** for each booked venue before delivery. If the fleet later expands beyond GA-local, re-check destination-state local-road width rules.

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
| ERV unit | ~80 lbs (36 kg) | Enthalpy-wheel ERV, ~150 cfm. (B005) |
| HVAC system | ~200 lbs (91 kg) | 3-ton inverter ducted mini-split: condenser ~140 + air handler ~60. Excludes duct/register weight (in finish/cartridge). (B005) |
| Electrical system | ~300 lbs (136 kg) | Panel + EMS + wiring/conduit + shore inlet/cordset + reserved ATS/DC conduit. ~20 lbs under the 320 lbs budgeted. (B006) |
| **Envelope subtotal** | **~3,900 lbs** | FRP SIP shell + floor + finish/openings. **Before any mechanical/electrical systems.** [D002: 102" width adds ~90 lbs envelope (wider roof/floor/end walls) — within the cartridge allowance; fold into the subtotal at B007.] |
| **Chassis subtotal** | **~8,250 lbs** (incl. ~580 lbs systems firm: HVAC+ERV ~280 lbs, electrical ~300 lbs) | Frame + envelope + ERV/HVAC/electrical. Systems now firm through B006; ~20 lbs under the ~600 lbs estimate. |
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

                    ← 8'6" (2591mm) exterior width →

    Interior clear: ~7'3" wide × ~10'1"-10'7" tall
    (width per B003 wall assembly + D002 102" exterior)
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

**Decision**: FRP skins, fleet-wide. Lighter, weatherproof, finished — directly serves the Weight Strategy decision (universal no-CDL). It's also the **road-durability** choice: an FRP-foam sandwich is the proven transport-body / expedition / marine construction (see B004 → Road-Dynamic Loads) — so source a **transport-grade** panel, not a building-grade SIP.
> **Caveats introduced by FRP skins** (track into B004 and prototyping):
> - **Structural data changes.** Premier's load charts (used in B004) are OSB-faced (ESR-4524). FRP-skinned SIP capacities differ and must come from the **FRP-panel supplier's own ratings** (transport-body / cold-storage / expedition-vehicle panel makers serve this market). The qualitative B004 conclusion (shell grossly over-strong; mounting is the real problem) almost certainly still holds, but the specific plf/psf numbers are OSB-based and need restating once a supplier is chosen.
> - **Fire rating.** FRP needs a thermal/ignition barrier on the interior for occupied commercial use — verify against code (open regulatory question).
> - **Less acoustic mass.** FRP skins give less mass-law isolation than OSB, shifting more of the "Taycan-quiet" burden onto Content Node's interior room-within-a-room (B010). The freed weight budget (~5,750 lbs cartridge allowance) covers the added interior acoustic mass.

### Panel Thickness: Walls 6½" GPS, Roof 8¼" GPS, Floor 6½"

Thickness trades **R-value against the dimension that is scarce for each surface**:
- **Walls** trade against interior **width** (binding constraint) → keep thin, use GPS to recover R.
- **Roof and floor** trade against interior **height**, where B002 shows a surplus (10'+ vs 9–10' target) → go thicker for R.

Wall thickness options (assembly = SIP + 0.5" exterior cladding + 0.5" interior finish per side; ×2 off the **102" exterior** (D002)):

| Wall SIP | Nominal | R-value @75°F (EPS / **GPS**) | Weight | Per-side assembly | Interior clear width |
|----------|---------|------------------------------|--------|-------------------|----------------------|
| 4½" | 114mm | 15 / **18** | 3.3 psf | 5.5" (140mm) | 91" = **7'7"** (2311mm) |
| **6½" [SELECTED]** | **165mm** | **23 / 28** | **3.5 psf** | **7.5" (191mm)** | **87" = 7'3" (2210mm)** |
| 8¼" | 210mm | 30 / **36** | 3.7 psf | 9.25" (235mm) | 83.5" = **6'11.5"** (2121mm) |

**Decision**: 6½" GPS walls → **R-28**, interior clear width **~7'3" (2210mm)** at the D002 102" exterior. This clears the original 6'8" target by ~7" — the width win comes from the wider exterior, *not* from thinning walls, so R-28 is retained. Going to 8¼" walls (R-36) still costs ~3.5" of interior width for marginal R; going to 4½" (R-18) sacrifices a third of the wall R-value for width Content Node no longer needs. The GPS 6½" remains the best balance.

> **Design target: 7'2" (86" / 2184mm).** As-built is ~7'3" (87"), but cartridges should design to 7'2" to absorb finish tolerances, fastener stand-off, and field variance. The extra inch is margin, not buildable space.

**Roof**: 8¼" GPS SIP → **R-36**. Trades against height surplus. Can flex 6½"–10¼" (R-28 to R-45) to trade height-margin against roof R-value.
**Floor**: 6½" SIP over the trailer deck → **R-23**. The steel deck provides structure; the SIP adds insulation and the interior walking surface. Underside is road-exposed, so floor R matters.

### Assembled R-Values (Envelope)

| Surface | Assembly | R-value | Passive-house context |
|---------|----------|---------|----------------------|
| Walls | 6½" GPS SIP | R-28 | Continuous insulation, near-zero thermal bridging. Below a cold-climate PH wall target (R-40+) but strong for a sub-100 sq ft footprint with this surface-to-volume ratio. |
| Roof | 8¼" GPS SIP | R-36 | Good. Can increase to R-45 (10¼") using height surplus if energy modeling demands. |
| Floor | 6½" SIP | R-23 | Adequate over a ventilated/road-exposed underside; verify against cold-floor comfort. |

[ASSUMED] Passive-house *certification* is not yet energy-modeled — these R-values are envelope inputs, not a verified PH result. PHPP/WUFI modeling is a later build (E03 thermal calc, B016). The SIP envelope's value is continuous insulation and airtightness, not headline R alone.

### Vacuum Insulation Panels (VIP) — evaluated, deferred (2026-06-21)

Panasonic ADVANC-R VIP (~R-66 at 0.94" ≈ **R-70/inch** — ~16× GPS foam [ASSUMED — vendor center-of-panel; effective installed R runs lower at edges/seams and ages down as the vacuum degrades]; glass-wool core in a vacuum-sealed aluminum-laminate bag; FM/Intertek certified) was re-evaluated after the original B001.1 cost-based deferral. **The mechanism that makes it buildable for us:** encapsulate VIP inserts *inside the GPS foam core* (the foam is the protective sandwich, per Panasonic's between-protective-layers demo), tiled into the **non-structural field bays** and kept clear of the Type L lumber-spline mounting lines (B004) — so no fastener ever pierces a vacuum panel. This neutralizes the puncture / road-fragility objection.

**Still deferred — it attacks a constraint we don't have:**
- **Not R-constrained.** Content Node's cooling load is *power-capped* (B005): envelope conduction is only ~2,000 of ~29,200 BTU/hr (~7%). Going R-28 → R-50+ saves ~0.08 ton of 3 — negligible. VIP's one superpower (R per inch) aims at the wrong wall; the **50A service binds, not the envelope.** Same logic for off-grid kWh (equipment-dominated, not envelope-dominated).
- **Not width-constrained.** D002 (102" exterior) already won the interior width — Content Node holds the ≥5'6" target with margin (conditional on B010 acoustic-nesting per `configs/content-node.md`; the 5'6" figure is itself [ASSUMED]). No need to buy width back with a thinner wall.
- **Weight near-neutral/negative.** SIP weight is skin-driven, not core-driven (see below), so thinning the core saves ~nothing while the VIP laminate adds mass. [ASSUMED — not modeled]
- **Semi-custom panel.** VIPs can't take the SIP co-press heat/pressure, so the core must be molded/cut around pre-made inserts — NRE + single-source risk. The original cost-prohibitive reason holds, now with a supply tail.

**The one revisit trigger — the 96" reclaim play.** An encapsulated VIP-SIP wall is the only lever that yields a ~7'2" interior inside a *narrower 96" exterior* — buying back the universal "any state, any road" transport margin that D002 traded away. If the fleet expands past GA-local delivery and 102" becomes a liability, this is the card to play. Until then: GPS-core FRP-SIP stays.

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
Exterior width:                      8'6"   (102" / 2591mm)  ← D002
Minus exterior cladding (× 2):      -1.0"   (0.5" per side)
Minus 6½" GPS SIP (× 2):           -13.0"
Minus interior finish (× 2):        -1.0"   (0.5" per side)
═══════════════════════════════════════════════════════════
Interior clear width (as-built):    87"    (7'3" / 2210mm)
Cartridge design target:            86"    (7'2" / 2184mm)  ← design to this
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
Towing imposes vibration, racking, and dynamic amplification (bumps ≈ 2–3g vertical [ASSUMED — not yet measured]) that static building codes don't address. **This is where SIP decisively beats stick frame for a unit that moves like a commercial trailer — not a move-once tiny home.** The enemy is *racking* and *fatigue at connections*, not gross strength:
- **Stick frame is hundreds of discrete fastened connections** — every nail a fatigue site. Racking resistance comes from sheathing nailing that *loosens* under cyclic load, and hygroscopic wood shrinks/swells and works connections loose. This is why move-once tiny homes arrive with cracked corners and rattled-loose trim.
- **A SIP is a stressed-skin sandwich — a monocoque, not an assembly.** The skin is bonded continuously across the whole face (diaphragm action, Load Charts #4A/B), distributing load instead of concentrating it at fasteners. Far fewer discrete joints = far fewer fatigue-initiation sites.
- **Precedent settles it.** Reefer/box-truck bodies, expedition campers, high-end RV shells, and many marine hulls are FRP-skinned foam sandwich — the same family as our FRP-SIP — precisely because they survive continuous road duty. Our wall *is* transport-body construction, insulated to Passivhaus. (A second, independent reason the FRP-skin choice was right — see Weight Strategy.)

> **The win is conditional — cash it in, don't assume it.** A sandwich panel's failure mode is **delamination** (skin peels from core → catastrophic stiffness loss), so the transport advantage holds *only* with a **transport-grade panel** (adhesive + skin qualified for road fatigue), **not a building-grade SIP** (Premier/Insulspan ESR-4524 panels are qualified for *static building* loads). Source from the transport-body / cold-storage / expedition FRP-panel suppliers (already the Weight-Strategy direction). And the fatigue concentrates at the **seams, mounting hardware, and box-to-frame connection** — not the panel field.
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

## HVAC System (B005)

> **Headline finding (B005): cooling — not heating — governs, and the cooling load is bounded by the electrical service, not the envelope.** Content Node's heat is dominated by its LED/compute/audio load, and that load is physically capped by the 50A shore service. HVAC, the heat it must reject, and the power service are therefore **circularly coupled**: the AC + ERV draw from the same 9,600 W continuous budget the cartridge competes for. The 50A service is effectively the *governor* on how hot the studio can run — so a **3-ton (36,000 BTU/hr) variable-capacity heat pump + a 150 cfm enthalpy-wheel ERV** is the self-consistent sizing. A bigger AC would be starved of both load and power.

### Design Conditions

| Parameter | Value | Notes |
|-----------|-------|-------|
| Indoor design (cooling) | 72°F / 22°C, 45–55% RH | Broadcast comfort; RH band controls condensation on LED/camera gear |
| Outdoor design (cooling) | 95°F db / 76°F wb (35°C / 24°C) | ASHRAE ~1% hot-climate point. Fleet tours hot markets — adjustable per deployment. [ASSUMED] |
| Outdoor design (heating) | 20°F / −7°C | Heating is a non-problem (see below); hyper-heat unit covers colder. [ASSUMED] |
| Sealed/dark chamber | No glazing, opaque FRP | No solar gain through openings; sol-air roof/wall gain only. No natural ventilation — mechanical is the *only* air path. |

### Cooling Load — Content Node Worst Case (power-constrained)

Almost all electrical power consumed inside the envelope becomes sensible heat (LED light, compute, audio amps all end up as heat in the room). So the in-envelope equipment heat **cannot exceed the service feeding it.** With NEC 80%-continuous derating, a 50A/240V service delivers **9,600 W continuous**; HVAC + ERV reserve ~3,150 W (~3,000 W compressor [ASSUMED — firm at unit selection] + 150 W ERV), so the cartridge equipment is capped at **~6,450 W (~22,000 BTU/hr)**.

| Source | Load | Basis |
|--------|------|-------|
| Cartridge equipment (LED + compute + audio + lighting + control) | ~22,000 BTU/hr | ≤6,450 W continuous = 9,600 W service − ~3,150 W HVAC+ERV draw. **Power-capped, not LED-spec-capped.** Itemized in B011. |
| Occupants (10 people) | ~4,500 BTU/hr | ~250 sensible + ~200 latent per person, light activity (ASHRAE) |
| Ventilation (150 cfm fresh, post-ERV) | ~700 BTU/hr [ASSUMED] | Assumes ~80% total (sensible+latent) recovery at design wet-bulb — optimistic for a real wheel at 76°F wb; refine with selected ERV's rated effectiveness. |
| Envelope conduction + sol-air solar | ~2,000 BTU/hr [ASSUMED] | Engineering estimate, not yet modeled (R-28 walls / R-36 roof / R-23 floor); the passive envelope makes this nearly negligible. Firm in B016 (PHPP/WUFI). |
| **Total cooling load** | **~29,200 BTU/hr (~2.4 tons)** | **Self-consistent with the 50A power budget.** |
| **Selected capacity** | **36,000 BTU/hr (3 tons)** | Margin for simultaneity, pull-down from a heat-soaked box, and degraded-condenser days. |

> **The naive worst case is a trap.** Two long LED walls (~256 sq ft / 23.8 m²) at full-white ~600 W/m² would draw ~14,000 W and imply a ~4-ton load. **The 50A service cannot supply that** (it can't even power the LEDs and the 4-ton AC at once). The service governs; 3 tons is correct. *If* a future battery bank / V2L / generator lifts the power ceiling (designed-for, B006), the studio's heat output and the required HVAC rise **together** — revisit tonnage when that power arrives, not before.
>
> **Cross-constraint flag → B006 / B011.** This load math assumes the studio equipment lives within ~6,450 W continuous *after* HVAC + ERV. B006 must allocate the panel so HVAC + ERV reserve their draw before the cartridge, and B011 must itemize Content Node to fit the remainder. If B011 needs more equipment power than ~6,450 W continuous, the binding constraint is the **50A service**, not the HVAC.

### Heating (secondary)

Passive-house envelope + internal gains make heating trivial. Empty-box conduction loss at 20°F design (ΔT ~52°F) is only **~2,000 BTU/hr** — two orders below the cooling case. The heat pump covers pre-conditioning and unoccupied freeze protection; once occupied, internal gains heat the box. **Cooling sizes the equipment; heating capacity is free.**

### Selected Equipment

| Unit | Spec | Power | Weight | Notes |
|------|------|-------|--------|-------|
| **Supplemental HVAC** | Ducted **variable-capacity (inverter) mini-split heat pump**, 36,000 BTU/hr (3-ton), hyper-heat class | ~3,000 W cooling / ~3,500 W heating | ~200 lbs (91 kg) — outdoor condenser ~140 lbs + indoor air handler ~60 lbs | **Inverter is mandatory**, not optional: the load swings from a near-empty idling box to a full studio. A single-stage 3-ton would short-cycle and fail to dehumidify at part load. ~1,200 cfm recirc (~400 cfm/ton). |
| **ERV** | **Enthalpy-wheel** ERV, ~150 cfm (70 L/s) nominal, ~80% total energy recovery | ~150 W | ~80 lbs (36 kg) | Sized for **CO2 control of 10 occupants** (~15 cfm/person), which exceeds ASHRAE 62.1 minimum (~86 cfm) — CO2, not code minimum, governs. Wheel recovers latent (humid-climate friendly). CO2 sensor required (occupied commercial). |
| **HVAC + ERV subtotal** | | ~3,150 W operating | **~280 lbs (127 kg)** | Fits within the ~600 lb chassis systems estimate; leaves ~320 lbs for electrical (B006). |

> **Condenser heat rejection is an exterior problem.** The 3-ton condenser dumps ~45,000 BTU/hr (cooling + compressor work) to outdoor air and **cannot reject into a sealed mechanical bay** — it mounts on the exterior (end wall or roof) with unobstructed airflow, or the mechanical bay gets large louvered intake/exhaust to outdoor air. Packaging location locks in B007. [ASSUMED — exterior end-wall mount]

### Zone Layout & Equipment Location

- **Single thermal zone.** At ~200 sq ft the box doesn't justify multi-zone control; the chamber is the load and gets the conditioned air. Control room takes a small branch register for equipment cooling.
- **Mechanical zone (~4', cartridge end).** Air handler, ERV, and (B006) electrical panel live here, acoustically isolated from the chamber. This zone *is* chassis-provided — Content Node's mechanical zone is this space. The condenser hangs on the exterior of this end.
- **Open question (from Content Node B008):** whether mechanical shares the ~4' end with the control room to recover chamber length. HVAC equipment footprint (air handler + ERV + clearances) is the constraint on combining them — resolve in B008.

### Duct Routing & Register Locations (Cartridge Interface)

| Element | Provision | Notes |
|---------|-----------|-------|
| Supply | 2–3 high-sidewall/ceiling supply registers along the 16' chamber | Cold supply drops over equipment + occupants. **Low face velocity (<500 fpm)** to hold register noise down — see acoustic constraint. |
| Return | 1–2 returns at the chamber end opposite supply | Promotes end-to-end sweep; filter at return. |
| Recirc duct | ~1,200 cfm trunk, low-velocity (large cross-section) | **Depth penalty:** low-velocity ducting is bulky even in the wider 7'3" box — competes with LED + acoustic depth at the ceiling/sidewall. Budget it against clear height/width. |
| ERV ducts | Independent fresh-supply + exhaust pair to/from occupied zone | Keep separable from recirc so ventilation runs without the compressor; interlock for CO2-driven boost. |

> Exact register coordinates, CFM-per-register, and trunk routing are finalized in **B007 (cartridge interface)** once Content Node's LED/acoustic depth (B009/B010) fixes the available ceiling/sidewall envelope. B005 establishes capacity, equipment, and method.

### Acoustic Constraint (→ B010)

Mechanical noise must not bleed into the chamber — the "sealed premium-car-cabin quiet" benchmark (D001). **Target ≤ NC-25 in the chamber** during HVAC operation. [ASSUMED — broadcast-grade]. Levers: isolate equipment in the mechanical zone, **low duct/register face velocity** (drives larger ducts → the depth penalty above), lined/baffled ducts, and vibration-isolated condenser/air-handler mounts. The variable-capacity unit also helps — it idles at low fan speed at part load instead of cycling on/off. **This couples HVAC duct sizing to the acoustic and width/height budgets — carry into B010.**

### Special Consideration: Heavy-Air Lounge

The Lounge runs **negative pressure** (exhaust > supply) at a higher air-change rate to clear cigar smoke, with cartridge-provided HEPA + activated-carbon filtration. Content Node is the *thermal* worst case, but the Lounge may be the *airflow* worst case. **Size chassis ductwork and the ERV exhaust path for the greater of (Content Node recirc airflow, Lounge ventilation airflow)** so the duct envelope reserved in B007 serves both. Quantify Lounge ACH in E10 (B-series TBD) and reconcile against the duct cross-sections reserved here. [ASSUMED — Lounge airflow not yet specified]

## Electrical System (B006)

> **Headline finding (B006): the 50A service is a hard power ceiling, and the panel's primary job is to *protect* it — reserve HVAC + ERV first, then ration the remainder to the cartridge.** A 50A/240V split-phase shore service delivers **12,000 W nameplate / 9,600 W continuous** (NEC 80%). HVAC + ERV reserve **~3,150 W** of that *before* any cartridge circuit energizes, leaving **~6,450 W continuous for the entire cartridge** (the B005 budget). Because Content Node can naively demand far more than that (a full-white LED wall alone is ~14 kW — B005), the electrical system **cannot rely on conservative breaker sizing alone**: branch breakers protect *wires*, not the *service*, so the sum of cartridge breakers is deliberately larger than 50A for placement flexibility. The service is instead protected by an **energy-management scheme that holds HVAC + ERV as a non-sheddable priority tier** and sheds/dims cartridge load before the 50A main trips. The panel busbar, conduit, and transfer-switch location are oversized *now* so a future battery / V2L can lift the ceiling — but per B005, **when the ceiling rises, the studio load *and* the required HVAC tonnage rise together.**

### Service Definition

| Parameter | Value | Notes |
|-----------|-------|-------|
| Shore connection | **50A, 120/240V split phase** (NEMA 14-50R / RV-style 50A inlet) | Standard US RV park / event shore power. Two 120V legs (L1, L2), 240V across both. |
| Nameplate capacity | **12,000 W** (50A × 240V) | Both-legs-loaded ceiling, not a single aggregate trip threshold — the 2-pole main trips on >50A in *either pole*. |
| **Continuous capacity** | **9,600 W** (NEC 80% derate) | The real working budget. All sizing below is against this number, **not** the 12,000 W nameplate. |
| Per-leg continuous | ~4,800 W each (L1, L2) | Split-phase balance matters — a leg can trip at 50A while the other idles. Cartridge 120V circuits are distributed across legs; **final steady-state balance is reconciled in B011** once actual draw is itemized (HVAC is 240V, inherently balanced). |
| Shore cordset | 50A RV cordset, 30–50 ft | Heavy (~1.5 lb/ft) — folded into the weight budget below. |

### Load Budget — Priority Tiers

The service is allocated top-down. Tier 1 reserves before Tier 2 sees any power.

| Tier | Load | Continuous draw | Running budget |
|------|------|-----------------|----------------|
| **Tier 1 — Chassis life-support (non-sheddable)** | HVAC heat pump (compressor + air handler) | ~3,000 W [ASSUMED — firm at unit selection] | |
| | ERV | ~150 W | |
| | **Tier 1 subtotal (reserved first)** | **~3,150 W** | 9,600 − 3,150 |
| **Tier 2 — Cartridge (managed)** | LED/display + compute + audio + lighting + control + convenience | **≤ 6,450 W continuous** | **= ~6,450 W remaining** |

> **This is the binding cross-constraint carried from B005 and into B011.** ~6,450 W continuous (~22,000 BTU/hr of eventual heat) is the *entire* Content Node electrical envelope after the chassis takes its share. B011 must itemize every Content Node component to live within it. The naive full-white LED draw is physically unsuppliable — the LED walls run dimmed/diverse by design, not by accident.

### Main Panel & Circuit Schedule

**Main load center: 100A busbar, 50A main breaker.** The busbar is oversized to 100A (2× the present 50A main) so a future battery/V2L source can feed it through the transfer switch **without replacing the panel.** Present shore main is 50A.

Circuits are **capacity provisions at the cartridge boundary**, not a promise that all may draw at once. Total branch-breaker capacity intentionally exceeds 50A — breakers size to protect their wire; the *service-level* draw is what the energy-management scheme caps at 9,600 W. The L1/L2 column shows **capacity placement, not balanced steady-state load** — the UPS-backed always-on cores (compute, control) are placed on opposite legs, but final leg balance is reconciled in **B011** against itemized draw.

| # | Circuit | Breaker | Leg | Cont. cap | Tier / Notes |
|---|---------|---------|-----|-----------|--------------|
| 1 | HVAC heat pump | 30A / 240V 2-pole | L1+L2 | ~3,000 W op | **Tier 1.** Dedicated; MCA per selected inverter unit. |
| 2 | ERV | 15A / 120V | L1 | ~150 W op | **Tier 1.** Runs independent of compressor (CO2 boost). |
| 3 | Display / LED — A | 20A / 120V | L1 | 1,920 W | Tier 2. Back-wall COB or long-wall window bank. |
| 4 | Display / LED — B | 20A / 120V | L2 | 1,920 W | Tier 2. Second display bank (immersive installs). |
| 5 | Compute / broadcast rack | 20A / 120V | L2 | 1,920 W | Tier 2. UPS-backed (clean shutdown). |
| 6 | Audio amplifiers | 20A / 120V | L1 | 1,920 W | Tier 2. |
| 7 | Experience lighting | 20A / 120V | L2 | 1,920 W | Tier 2. Dimmable; entry/transition lighting branches here. |
| 8 | Control / Container OS / network | 15A / 120V | L1 | 1,440 W | Tier 2. **UPS-backed, isolated** — never sheds. |
| 9 | General convenience + service | 20A / 120V | L2 | 1,920 W | Tier 2. GFCI. First to shed. |
| 10 | Spare (future cartridge) | 20A / 120V | L1 | — | Tier 2. Capped/landed for the next cartridge variant. |

### Energy Management (the service-protection scheme)

Because Tier 2 breaker capacity (~13 kW) far exceeds the ~6,450 W actually available, **something must prevent a full studio from tripping the 50A main.** Spec a **shore-power energy-management system (EMS)** — RV/marine-class automatic load management — with this priority logic:

1. **HVAC + ERV are protected** (Tier 1) — never shed. Comfort and dehumidification hold even at peak.
2. **Container OS / control (circuit 8) is protected** — the venue must not lose its brain.
3. **Remaining Tier 2 circuits shed in reverse priority** (convenience → spare → lighting → audio → displays-dim) to keep total draw ≤ 9,600 W continuous / ≤ 50A/leg instantaneous.

> **Container OS is the natural load manager.** Per the system architecture, Container OS is the software control plane for physical venue systems — making power allocation a Container OS responsibility (dim the LED walls, throttle non-critical circuits) closes the loop the B005 thermal math depends on. The EMS hardware is the fail-safe backstop; Container OS is the intelligent layer. Defines a real protocol surface for the Container OS integration.

### Future Battery / V2L Expansion (Designed-For)

Unit #1 ships shore-only, but the panel is built so battery/V2L is a bolt-on, not a rebuild. Per the power-independence exploration (2026-06-16), off-grid is an **energy (kWh × weight)** problem, not the power (kW) problem the 50A service already solves — so what's reserved here is the *interface*, sized for the ranked paths (EV-truck V2L ≈ 9.6 kW best fit; onboard LiFePO4 for short events; solar = trickle only).

| Reserved | Provision |
|----------|-----------|
| Transfer switch | **Automatic transfer switch (ATS) location** reserved between shore inlet and main, pre-wired landing. |
| Busbar headroom | 100A busbar (above) accepts combined shore + battery/V2L without panel replacement. |
| Battery bay | Floor/under-floor volume reserved in the mechanical zone for a **modular LiFePO4 rack** (~10 lb/kWh — weight, not space, caps capacity). |
| V2L inlet | Second exterior inlet location reserved for **EV tow-vehicle V2L** (~9.6 kW — the truck *is* the power plant, best-fit path). |
| Inverter/charger | Location reserved in the mechanical zone; **oversized DC conduit** run (or pull-string) between battery bay and inverter/panel. |
| Bonding transition | An inverter is a **separately derived system** — when added, the system bonding jumper moves to the inverter. Anticipated in the ATS design now (see Grounding). |

> **⚠️ B005 coupling — raising the ceiling is not free.** A battery/V2L lifts the 9,600 W continuous ceiling, but Content Node's heat output and therefore the required HVAC tonnage **rise with it** (B005's circular coupling). Reserved conduit/space buys *power*; spending it costs *cooling*. Re-size HVAC when the power actually arrives, not before.

### Grounding & Bonding (mobile structure)

| Item | Spec |
|------|------|
| Neutral–ground bond | **At the shore source (pedestal), not in the trailer panel.** The trailer load center is wired as a sub-panel — isolated neutral and ground bars (NEC Art. 551 mobile-structure practice). |
| Equipment grounding | EGC bonds the **aluminum frame**, condenser, all metal enclosures, and the ATS to one ground reference. |
| GFCI / AFCI | GFCI on receptacle/convenience circuits (occupied commercial, wet-adjacent exterior shore); AFCI per occupancy code. |
| Battery transition | When the inverter (separately derived system) is added via the ATS, the **system bonding jumper moves to the inverter** — design the ATS landing for this now. |

### Weight Budget (~320 lbs budgeted — B005 carryover)

| Item | Weight | Notes |
|------|--------|-------|
| Load center + breakers + EMS module | ~45 lbs | 100A panel, 10 circuits, smart load-management module. |
| Branch wiring + conduit | ~150 lbs [ASSUMED] | **Copper branch circuits; aluminum feeders for heavy main runs** (weight lever, consistent with the aluminum frame). |
| Shore inlet + 50A cordset | ~35 lbs | Cordset dominates (~1.5 lb/ft). |
| ATS landing + future DC conduit (empty) | ~30 lbs | Reserved/empty now; conduit + pull-strings only. |
| Grounding, bonding, junctions, devices | ~40 lbs | Receptacles, boxes, EGC, bonding hardware. |
| **Electrical subtotal** | **~300 lbs** | **~20 lbs under the 320 lbs budgeted** — fold the firm number into the chassis subtotal at B007. |

### Regulatory / Code [ASSUMED — open item]

A mobile commercial venue straddles two electrical regimes: **NEC Art. 551** (RV / shore-power side, governs the inlet, cordset, and mobile-structure bonding) and **commercial occupancy electrical code** when deployed and occupied by the public. The inspection authority is unclear — state electrical board at build, or local AHJ at each venue? **This needs an electrical engineer's stamp and an AHJ determination before fleet production**, alongside the open FRP fire-rating and transport-width items. [ASSUMED — not yet confirmed]

### Connection Points (Cartridge Interface)

Cartridge circuits land at a **labeled junction/sub-panel at the mechanical-zone boundary** — each circuit's physical location, breaker, voltage, and leg assignment per the schedule above. Exact coordinates are formalized in **B007 (cartridge interface)** once Content Node's zone layout (B008) fixes equipment positions. B006 establishes the service, the panel, the tiered budget, and the circuit method.

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
