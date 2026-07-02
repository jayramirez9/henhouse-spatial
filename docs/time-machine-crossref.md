# Cross-Reference: Time Machine ↔ Henhouse ADU

Both projects live in the `~/henhouse` monorepo (independent git repos). Paths below are monorepo-relative; agents working in either project can read across via `../`.

## The relationship

**Time Machine** (`../time-machine`) is the immersive experience software — weather/world-state engine, historical environment reconstruction, audio, Unreal rendering. **Henhouse ADU** (this project) is the physical platform that hosts it: the Content Node fit-out turns the ADU into the venue Time Machine renders into — displays as architectural windows, multi-zone audio, one workstation running one Unreal process.

The ADU is the **"first room"** — the physical milestone that Time Machine's year-1 review recommends year 2 converge on. Time Machine's PRD defines its MVP as a venue (windows + directional audio + operator + calibration); this project is where that venue physically exists.

## What to read in Time Machine (from here)

| Doc | Why it matters to the ADU |
|-----|---------------------------|
| `../time-machine/docs/roadster-trailer-hardware.md` | Concept-trailer/ADU compute, display, audio, and install (electrical/thermal/rack) spec — written for this build |
| `../time-machine/docs/review-year1-2026-07.md` | Year-1 review; §1 ("first room" recommendation) and the year-2 sequence directly shape this project's Content Node work |
| `../time-machine/PRD.md` §12–13 | Window model (position/orientation/specs per window) and speaker topology (4-zone N/E/S/W min, 8-zone preferred + sub) — the physical requirements the ADU must satisfy |
| `../time-machine/PRD.md` §16, §19 | Operator UX / health / recovery, and the MVP definition the venue must meet |
| `../time-machine/PRD.md` §17 (Topology) | First install collapses Master/Render/Audio onto **a single workstation running one Unreal process** — free frame sync, no genlock |
| `../time-machine/CLAUDE.md` | Engine quick reference: daemon (`tm-engine.js`, HTTP/WebSocket on :3000), routes/dispatch to Unreal |

## What Time Machine needs from the ADU (open decisions this project owns)

These are Time Machine PRD §24 "near-term architecture decisions" that only the physical space can answer:

1. **Canonical window layout** — count, size, placement, cardinal mapping of the display-windows in the ADU (bounded by interior clear width ~7'2"/2184mm design target).
2. **Canonical speaker topology** — 4-zone vs 8-zone + subwoofer, and where zones physically mount.
3. **Power/thermal envelope for the render workstation** (5090-class GPU) — feeds the tiered load budget (B006 electrical spec) and HVAC sizing.
4. **Room lighting integration** — Time Machine's "it still feels like TV" risk (PRD §21) is mitigated in the physical room: black levels, window trim, ambient light control.

Record answers in `contracts/` / `configs/content-node.md`; Time Machine consumes them as its venue profile.

## Connection points

- **Fit-out spec (this repo):** `configs/content-node.md` — the cartridge that hosts Time Machine.
- **Control plane:** Container OS (`../container-os`) controls the physical systems modeled here; Time Machine drives content, not HVAC.
- **Engine integration:** Time Machine's daemon exposes WorldState over HTTP/WebSocket; the ADU's AV chain is a consumer, not a modifier (One Universe law).
