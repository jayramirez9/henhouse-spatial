# Forge — Programming System v0.2

**Forge** is a systematic process for building programs. Applies across languages, frameworks, and project types. Iterated over time.

Inspired by DesignOps thinking: a design system for how we build, not just what we build. Named like NYT's "Ink" — Forge refers to the methodology, not any individual product.

---

## Phase 0: Discovery

**Goal**: Understand what we're building and why before touching code.

### Inputs
- What problem does this solve?
- Who is it for? (User, internal team, API consumer, machine)
- What does success look like? (Measurable, not vibes)
- What already exists? (Existing code, APIs, patterns to follow)
- What constraints exist? (Language, platform, security, compliance, timeline)

### Outputs
- **Problem statement**: 1-2 sentences. If you can't state it clearly, you don't understand it yet.
- **User profile**: Who uses this and what do they need to feel/accomplish?
- **Success criteria**: How we'll know it works. These become evals later.
- **Constraint inventory**: Non-negotiables (language, security, accessibility, performance)

### Anti-patterns
- Jumping to implementation before understanding the problem
- Assuming you know the user's need without evidence
- Skipping constraint discovery (leads to rework)

---

## Phase 1: Architecture & API Design

**Goal**: Design the system's shape before building any of it.

### For APIs (internal or external)
- **Contract-first**: Define the interface before implementation
  - REST: Define routes, request/response shapes, status codes
  - Libraries: Define exports, function signatures, return types
  - Data: Define schemas, valid ranges, enum values
  - Events: Define event names, payload shapes
- **Consumer perspective**: Design from the caller's point of view, not the implementer's
- **Error taxonomy**: How does this system fail? What does the consumer see?
- **Versioning strategy**: How will this evolve without breaking consumers?

### For UX/Design
- **Interaction model**: How does the user accomplish their goal? (Steps, not screens)
- **Information hierarchy**: What matters most? What can wait?
- **Feedback loops**: How does the system communicate state? (Loading, success, error, empty)
- **Accessibility from day one**:
  - Semantic HTML / native controls first, custom widgets only when necessary
  - Keyboard navigation: every action reachable without a mouse
  - Screen reader: all content has text alternatives, ARIA only when semantic HTML is insufficient
  - Color: never rely on color alone for meaning. Maintain WCAG AA contrast (4.5:1 text, 3:1 large text)
  - Motion: respect `prefers-reduced-motion`. No flashing >3 times/second
  - Focus management: visible focus indicators, logical tab order
- **Reference-driven**: Find 2-3 examples of great UX for this type of thing. Attach screenshots/code to the prompt.

### For Security
- **Trust boundaries**: Where does trusted input end and untrusted input begin?
- **Authentication & authorization model**: Who can do what?
- **Data classification**: What's sensitive? PII, credentials, financial, health?
- **Input validation**: Validate at system boundaries, trust internal code
- **OWASP Top 10 check**: Injection, XSS, CSRF, SSRF, broken auth — which apply here?
- **Secrets management**: Environment variables, never hardcoded, never committed
- **Dependency policy**: Fewer dependencies = smaller attack surface

### Outputs
- **Architecture sketch**: Modules, data flow, boundaries (can be text, doesn't need to be a diagram)
- **API contract / data schema**: The "WorldState contract" approach — codify what valid looks like
- **Security threat model**: Brief, just the relevant concerns
- **Accessibility requirements**: Which WCAG level, which assistive technologies to support

---

## Phase 2: Planning & Task Breakdown

**Goal**: Break the work into sequenced, evaluable tasks.

### Process
1. **Write the eval first**: Before building a feature, define how you'll know it works
   - Unit tests for logic
   - Contract validation for data shapes
   - Integration tests for system boundaries
   - Visual/UX checks for human-facing surfaces
2. **Sequence by dependency**: Build foundations first (data layer → logic → API → UI)
3. **One task, one concern**: Each task should be completable and testable independently
4. **Document as you plan, not after**: The plan IS the documentation

### Epic & Build Numbering

Work is tracked in **epics** (large feature areas) and **builds** (shippable increments).

#### Epic numbering: `E{NN}-{short-name}`
Epics are major feature areas or workstreams. Numbered sequentially per project.

```
E01-weather-providers     # Weather API integrations
E02-world-state-pipeline  # Timeline → WorldState compilation
E03-audio-engine          # 5-layer audio system
E04-unreal-dispatch       # Unreal Engine remote control
E05-terrain-pipeline      # DEM + imagery + import
E06-eval-system           # Evals and review agent
```

Epics are defined during Phase 1 (Architecture) and refined during Phase 2 (Planning). An epic is never "done" — it can receive new builds over time. Epics map roughly to modules or feature areas in the codebase.

#### Build numbering: `B{NNN}`
Builds are shippable increments within an epic. Numbered globally across the project (not per-epic) so there's one linear timeline of what shipped and when.

```
E05-terrain-pipeline
  B041 — DEM fetcher: bounding box + 3DEP download + GDAL R16 conversion
  B042 — NAIP imagery fetcher: satellite tile download matching terrain extent
  B043 — Import guide: validate files, check Unreal, print Landscape instructions

E06-eval-system
  B044 — WorldState contract module (lib/worldStateContract.js)
  B045 — Golden state tests + route config tests
  B046 — Unified eval CLI (tm-eval.js)
  B047 — GitHub Actions eval workflow
  B048 — Code review agent + review workflow
```

#### Build rules
- A build is **one shippable unit**: it compiles, tests pass, it could be merged
- A build should take **1 session or less** (hours, not days)
- A build has a **clear eval**: how do we know this build works?
- Builds are sequential within an epic but epics can run in parallel
- The build number goes in the **commit message**: `B048: Add code review agent + GitHub Actions workflow`
- Build log lives in `builds.md` at the project root (or in project memory)

#### Build log format (`builds.md`)
```markdown
# Build Log

## B048 — Code review agent (E06-eval-system)
- **Date**: 2026-03-06
- **Epic**: E06-eval-system
- **What**: GitHub Actions workflow + Anthropic API review script
- **Files**: .github/scripts/review-pr.js, .github/workflows/review.yml, .github/review-prompt.md
- **Eval**: Manual — push test PR with ANTHROPIC_API_KEY secret, verify comment posted
- **Status**: Complete

## B047 — GitHub Actions eval workflow (E06-eval-system)
- **Date**: 2026-03-06
- **Epic**: E06-eval-system
- **What**: .github/workflows/eval.yml runs tm-eval.js --json on push/PR
- **Files**: .github/workflows/eval.yml
- **Eval**: Push to branch, verify Actions run passes
- **Status**: Complete
```

### Planning Documents (the "Lazar Stack")
- **masterplan.md**: What we're building, why, for whom. 10,000-foot view
- **implementation-plan.md**: Sequenced phases with dependencies. Lists epics.
- **contracts/**: Data shapes, API schemas, valid ranges (these become runtime validators)
- **tasks.md**: Current epic's build tasks with checkboxes. Agent reads this to know what's next
- **builds.md**: Linear log of all completed builds (the project's history)

### Rules for AI collaboration
- Add project knowledge / rules.md with:
  - "Read all .md files before making changes"
  - "Reference specific files in prompts, don't re-describe"
  - "After fixing a bug, explain what went wrong so I can update rules"
  - Project-specific conventions (naming, patterns, module structure)

---

## Phase 3: Building

**Goal**: Implement one task at a time, test as you go.

### Build cadence
1. **Identify the build**: Which epic does this belong to? What's the build number?
2. **Read before write**: Understand the existing code/module before changing it
3. **One module per prompt**: Keep context focused. Reference specific files
4. **Test immediately**: Run tests after each change, not at the end
5. **Commit at build boundary**: Each build gets a commit with `B{NNN}: description`
6. **Log it**: Update `builds.md` with what was built, what files changed, how to eval it

### Code standards (cross-language)
- **Naming**: Clear, descriptive, consistent with existing patterns
- **Error handling**: At system boundaries. Don't over-handle internal code
- **Logging**: Structured, leveled. Debug info in dev, actionable info in prod
- **Comments**: Only where the "why" isn't obvious from the code
- **No premature abstraction**: Three similar lines > one clever helper used once

### Security during build
- [ ] Input validation at every system boundary (user input, API responses, file reads)
- [ ] Parameterized queries (SQL) / template literals (HTML) — never string concatenation for untrusted data
- [ ] Authentication/authorization checks on every protected route
- [ ] Secrets from environment, never hardcoded
- [ ] HTTPS everywhere, secure headers (CSP, HSTS, X-Frame-Options)
- [ ] Rate limiting on public endpoints
- [ ] Audit logging for sensitive operations

### Accessibility during build
- [ ] Semantic HTML elements (`<button>`, `<nav>`, `<main>`, `<h1>`–`<h6>`)
- [ ] All images have `alt` text (decorative images get `alt=""`)
- [ ] Form inputs have associated `<label>` elements
- [ ] Focus visible on all interactive elements
- [ ] Skip-to-content link on pages with navigation
- [ ] ARIA attributes only when semantic HTML is insufficient
- [ ] Color contrast meets WCAG AA (verify with tools, not eyes)
- [ ] Tested with keyboard-only navigation
- [ ] Tested with screen reader (VoiceOver on Mac)

### Debugging workflow (the "4x4")
1. **Ask the tool to fix it**: Let the agent try first
2. **Add visibility**: Console logs / debug output at key points, feed output back
3. **External consultant**: Different AI context (Codex, separate Claude session) for diagnosis only
4. **Revert and rethink**: Step back, improve the prompt, try again fresh
5. **Learn from it**: Ask "how should I have prompted you better?" → encode answer into rules

---

## Phase 4: Verification

**Goal**: Prove it works before shipping.

### Eval layers
| Layer | What it checks | How |
|-------|---------------|-----|
| **Unit** | Individual functions and logic | Built-in test runners (node:test, pytest) |
| **Contract** | Data shapes and bounds | Schema validators against known-good states |
| **Integration** | Module interactions, API calls | End-to-end tests with mock externals |
| **Security** | Vulnerability surface | OWASP checklist, dependency audit, secrets scan |
| **Accessibility** | WCAG compliance | Automated (axe-core), manual keyboard + screen reader |
| **UX/Visual** | Does it look and feel right? | Screenshots, interaction testing, user feedback |
| **Performance** | Speed, resource usage | Load tests, profiling for hot paths |

### Review (separate context)
- Code review by a different agent/person than the builder
- Reviewer checks: architecture consistency, contract compliance, security, test coverage
- Review prompt encodes project conventions so the reviewer knows the rules

### Eval CLI pattern
Every project should have a single command that answers "is this good?":
```
./eval.js        # or pytest, or make eval
./eval.js --json # CI-friendly structured output
```
Exit 0 = ship it. Exit 1 = fix it.

---

## Phase 5: Ship & Maintain

**Goal**: Get it in front of users, keep it running.

### Pre-ship checklist
- [ ] All evals pass
- [ ] Security review complete (or self-reviewed against checklist)
- [ ] Accessibility tested (keyboard + screen reader minimum)
- [ ] Documentation updated (README, API docs, CLAUDE.md)
- [ ] Error monitoring in place (know when it breaks)
- [ ] Rollback plan exists (can you undo this deployment?)

### Maintenance
- **Dependency updates**: Regular cadence, test after each update
- **Eval regression**: If a bug is found, add an eval that catches it before fixing
- **Documentation drift**: When code changes, docs change in the same commit
- **Rules evolution**: Update rules.md / project knowledge when patterns emerge

---

## Cross-cutting: API Design Principles

Applies to any API (REST, library, CLI, event system):

1. **Predictable**: Same inputs → same outputs. No surprises.
2. **Self-describing**: Names explain purpose. Errors explain what went wrong and how to fix it.
3. **Minimal surface**: Expose what's needed, hide implementation details.
4. **Composable**: Small, focused functions/endpoints that combine well.
5. **Versioned**: Breaking changes get new versions. Non-breaking changes are additive.
6. **Documented by contract**: The schema/types ARE the docs. Runtime validation enforces them.

---

## Cross-cutting: Design & UX Principles

1. **Clarity over cleverness**: If it needs explanation, simplify it.
2. **Progressive disclosure**: Show what's needed now, reveal details on demand.
3. **Feedback always**: Every action gets a visible response (loading, success, error).
4. **Forgiveness**: Undo > "Are you sure?" Recoverable > destructive.
5. **Consistency**: Same patterns for same interactions across the product.
6. **Performance is UX**: A fast, simple thing beats a slow, fancy thing.
7. **Mobile-first responsive**: Design for the smallest screen, enhance for larger.

---

## Process Meta-rules

1. **This document evolves**: Update it when we learn something. Delete what doesn't work.
2. **Skip phases consciously**: For a quick prototype, skip Phase 4 verification — but know you're skipping it.
3. **Scale to the task**: A one-file script doesn't need a masterplan.md. A multi-module system does.
4. **The process serves the work, not the other way around**: If a phase feels like busywork, the process needs fixing.
5. **Encode learnings**: When something goes wrong, update this document or the project's rules. Don't just remember — write it down.

---

*v0.2 — 2026-03-06. Added epic/build numbering. Refine after each project.*
