# Laser Turret — Living Project State

**Canonical source of truth for this project. Read this file first in every new Laser Turret chat. Update it when the user says `wrap`.**

**Repository:** `david-steinbroner/laster-toy-turret`  
**Last updated:** 2026-09-15  
**Current phase:** Pre-CAD / fit-test definition  
**V1 target:** Wall-powered 2-axis pan/tilt cat laser turret using the user's removable rechargeable laser pointer. A future battery upgrade must be possible **without reprinting the core turret**.

---

## Session protocol

### Starting a new chat
If the user says **“continue Laser Turret”**:
1. Fetch and read this `PROJECT_STATE.md` first.
2. Treat it as authoritative over older chats, memories, concept images, and the web visualization.
3. Inspect relevant files in `cad/`, `prints/`, `references/`, and `web/` as needed.
4. Continue from **Current next steps**, not from scratch.

### Ending a chat
If the user says **“wrap”**:
- update this file with new measurements,
- decisions,
- files/artifacts,
- test/print results,
- blockers,
- exact next steps.

The user should not need to copy/paste prior chat history.

---

# Latest checkpoint — 2026-09-15

## What changed this session
- Set up GitHub as the persistent engineering record.
- Established this `PROJECT_STATE.md` as the living project document.
- Initialized repo areas for future work: `cad/`, `prints/`, `references/`, `web/`.
- Confirmed repo path: `david-steinbroner/laster-toy-turret`.
- Repo is currently public. This does not block the project; visibility can be changed later if desired.
- Confirmed that the existing Vercel/Three.js model is reference-only. Further web-polishing should not delay real CAD.

## No manufacturing artifact completed yet
- No real parametric CAD yet.
- No fit-test STL yet.
- No physical fit test yet.
- No servo horn selected yet.

## Current next steps
1. Start **parametric fit-test CAD**, not more concept illustration.
2. Build an **SG90 fit coupon** using supplied servo dimensions with sensible clone clearance.
3. Build a **laser cradle fit coupon** around the confirmed 16.1 mm body, informed by the prior successful ~15.45 mm spring-clip fit.
4. Select/measure the actual SG90 horn and make a **horn-to-platform interface test**.
5. Build a **passive-pivot tolerance test**.
6. After fit tests are validated, build the upper mechanism.
7. Then build the modular wall-powered base with the battery-upgrade interface already included.

---

# 1. Product intent

Build a compact 3D-printable turret that automatically pans and tilts the user's existing rechargeable laser pointer.

Locked product requirements:
- Laser remains **fully removable** for handheld play.
- **Never solder to or permanently modify the laser.**
- V1 is **wall powered only**.
- Future battery power must be an add-on/replacement module that mates to V1's existing interface; **do not require reprinting the core turret/base**.
- Both axes use **SG90** micro servos.
- Design should be compact, serviceable, and not over-engineered.
- Target printer/material: **Bambu A1, regular PLA**.
- Printable parts should remain separate/editable where practical.
- Final deliverables should eventually include editable parametric CAD, individual STLs, a combined 3MF with meaningful parts kept separate, and small fit-test parts before large prints.

---

# 2. Locked mechanical architecture

Architecture is inspired by the supplied OpenMV pan/tilt assembly, but geometry must be purpose-built for this laser.

## Pan axis
- One **SG90** sits vertically inside the base.
- Its horn drives a rotating upper platform.
- The entire upper assembly rotates with it: tilt fork, tilt SG90, passive pivot, cradle, laser.
- Keep upper mass low and reasonably balanced.
- Use gentle software acceleration.
- Physically validate SG90 pan torque during prototype testing.

## Tilt axis
- U-shaped fork on rotating pan platform.
- One **SG90** mounted on one side.
- Opposite side uses a **passive pivot / bushing / bearing feature**.
- Laser cradle spans the fork.
- Laser centerline should align with the tilt axis so the laser rotates in place rather than sweeping through solid fork walls.
- Passive side supports the cradle so the tilt servo shaft is not acting as a cantilever.

## Laser cradle
- Removable / quick release.
- Must not block the slide switch.
- Must leave rear micro-USB charging port accessible.
- Should account for pocket clip/lanyard geometry if those remain attached.
- No permanent electrical connection to laser.

---

# 3. Confirmed laser measurements

| Item | Value |
|---|---|
| Main body diameter | **16.1 mm** |
| Overall length | **96.5 mm** |
| Switch type | **Sliding switch**, not push button |
| Slide-switch assembly | **14.5 mm × 7.5 mm** |
| Switch start location | Begins **26.4 mm from beam/front end** |
| Charging connector | **Micro-USB** |
| Charging-port location | **Centered on rear/end face** |
| Permanent modification | **Not allowed** |

Reference photos also show:
- pocket clip,
- rear lanyard attachment,
- sliding multifunction switch,
- centered rear micro-USB port.

Still useful before final cradle CAD:
- pocket-clip protrusion/location if clip stays installed,
- lanyard clearance if lanyard hardware stays installed,
- approximate laser mass for servo-load sanity check.

### Prior successful laser fit
Earlier **Laser Clip V3** reportedly fit this pointer:
- pointer nominal OD: 16.1 mm,
- spring clip ID about **15.45 mm**,
- screw slots **26 mm apart**.

Treat 15.45 mm as empirical spring-clip information, not automatically the final cradle ID.

---

# 4. Servos

## Locked servo choice
**Pan = SG90. Tilt = SG90.**

Supplied SG90 diagrams suggest approximately:
- body width: **22.5 mm**,
- body depth: **11.8–12 mm**,
- body height: about **22.7–22.8 mm**,
- mounting-ear overall span in one diagram: **31.8 mm**,
- standard 3-wire connector.

SG90 clone housings vary. Do not make a tight final cavity based only on generic internet dimensions.

### Required validation
Either:
1. measure the exact SG90s in hand, or
2. print an SG90 fit coupon using the supplied drawings and modest clearance.

### Horn
Exact horn is **not locked**. Need to select the actual horn and validate:
- type,
- thickness,
- effective diameter / arm length,
- hole pattern,
- center screw clearance.

---

# 5. Power architecture

## V1
**Wall powered only.**

Concept:

```text
wall power
   |
power-input / power module
   |
   +---- regulated 5 V ----> pan SG90
   |                     -> tilt SG90
   |
   +---- controller power
            |
            +-- pan signal
            +-- tilt signal
```

Rules:
- Do not route servo current through a tiny controller's onboard regulator.
- Servos and controller share ground.
- Provide enough 5 V current headroom for two SG90 transient loads.
- Exact wall-power connector/cable is not locked yet.

## Future battery requirement
V1 must include a standardized **power/battery expansion interface**.

```text
CORE TURRET  <-- remains unchanged
    |
    +-- V1 wall-power insert/module
    |
    +-- future battery/power module
```

Possible form: rear cartridge, bottom drawer, bolt-on pod, or removable service/power bay. Exact form may be chosen during CAD. The non-negotiable requirement is that V1 already contains the mechanical mounting interface and wire pass-through.

---

# 6. Controller

A full Arduino Uno is considered unnecessary for the final product.

Leading concept: **Seeed XIAO ESP32-C3** because it is tiny and leaves room for future wireless control. Not purchased/locked yet.

Controller needs:
- 2 servo signal outputs,
- program storage for autonomous movement,
- convenient programming/update path,
- compact footprint,
- no direct servo-current burden.

---

# 7. Soldering and serviceability

- User owns a soldering gun and is open to soldered turret wiring.
- Laser itself must never be soldered into the turret.
- Likely final approach: soldered internal harnesses with removable connectors.
- Servos, controller, and power module should remain replaceable.

---

# 8. Laser charging and activation

## Charging stretch goal
If practical, allow the laser to charge while mounted:
- centered rear **micro-USB**,
- short removable charging lead,
- preferably only when turret is wall powered.

Do not let this delay a functional V1.

## Beam switching
Laser uses a **manual sliding multifunction switch**.

Current design does not electronically switch the beam because the pointer is not being modified. V1 must simply keep the slider accessible.

Automatic beam control later would require either:
1. a small mechanical actuator that moves the slider, or
2. electrical modification of the laser, which is currently outside requirements.

The “Show Beam” control in the web prototype is visualization only.

---

# 9. Expected printed parts

Likely V1 parts:
1. **Base enclosure** — lower SG90 mount, controller/power routing, future battery interface.
2. **Service lid / access cover**.
3. **Rotating pan platform** — interfaces to lower SG90 horn.
4. **Tilt fork** — SG90 on one side, passive pivot on the other.
5. **Removable laser cradle** — 16.1 mm pointer, switch + charging access.
6. **Passive pivot / bushing piece**.
7. **V1 wall-power module / insert** — removable/replaceable.
8. **Future battery module** — later, same interface, no core reprint.

Possible extras:
- charge-cable keeper,
- wire clips / strain relief,
- servo-horn adapter.

---

# 10. Legacy work worth preserving

## Laser Clip V3
- Successful 16.1 mm pointer fit.
- ~15.45 mm clip ID worked.
- Screw slots 26 mm apart.

## Lower servo/base Option C V7
Reported working:
- open-top SG90 cradle,
- rear cable exit,
- shorter ~13 mm towers.

## Older sideways upper-servo bracket
Previously: `sg90_sideways_bracket_editable_parts_v1.3mf`
- horizontal SG90,
- open horn side,
- walls/floor as separate editable Bambu objects,
- unresolved rear wire-notch location.

**Superseded by the current U-fork architecture. Do not revert unless explicitly requested.**

## Arduino Uno base
Earlier Uno peg-position work is likely obsolete because the final controller should be much smaller.

---

# 11. OpenMV / GrabCAD reference

Supplied package: `pan-tilt-assembly-1.snapshot.9.zip`

Useful source parts include STEP/STL files for base, arm, tray, stand/adaptors and assembly-guide images.

Use only as a **mechanical topology reference**:
- vertical pan servo,
- rotating upper stage,
- U-fork,
- side-mounted tilt servo,
- opposite passive pivot.

Do **not** simply scale the camera assembly. The laser design should be smaller, lighter, and purpose-built.

---

# 12. Interactive concept model

Latest live visualization:
`https://laser-turret-v3-davidsteinbroner-2472.vercel.app`

Features:
- touch orbit / pinch zoom,
- pan/tilt sliders,
- auto motion,
- beam visualization,
- mechanism/exploded modes,
- multiple views.

History:
- early versions had laser clipping through geometry,
- later versions improved hierarchy,
- mechanism/exploded views remain imperfect,
- further polishing is lower priority than actual CAD.

**Never treat the Three.js model as manufacturing-authoritative geometry.**

---

# 13. Print-readiness adversarial review

A technical drawing and adversarial redline were created. Conclusion:

**NOT READY TO PRINT YET**

Outstanding manufacturing issues:
- exact dimensions missing on some features,
- tolerances/fit clearances not defined,
- horn/spline interface not finalized,
- screw sizes/hole diameters not finalized,
- wall thickness/minimum feature sizes not locked,
- new cradle retention not validated,
- passive pivot fit incomplete,
- wire-routing clearances not verified,
- service-lid mounting not finalized,
- pan-load margin not physically validated,
- print orientations/support strategy not defined,
- chamfers/fillets/elephant-foot allowances not finalized,
- no final watertight CAD solids yet.

Resolved since that review:
- laser length = **96.5 mm**,
- laser OD = **16.1 mm**,
- slide switch substantially defined,
- charging connector/location known,
- both servo models = **SG90**,
- V1 = wall powered,
- battery upgrade = modular.

---

# 14. Remaining genuine unknowns

High priority before final manufacturing CAD:
1. Actual SG90 fit / mounting-ear geometry on the exact servos.
2. Exact SG90 horn choice and dimensions.
3. Pocket-clip/lanyard clearance if those remain installed while mounted.
4. Approximate laser mass.
5. Desired pan and tilt limits, unless selected during engineering.

Can be chosen during design:
- base diameter/height,
- wall thickness,
- platform thickness,
- PLA tolerances/clearances,
- screw strategy,
- service-lid fastening,
- print orientation,
- chamfers/fillets,
- cable routing,
- battery-interface geometry.

Electronics still to lock:
- controller model,
- wall-power connector/cable,
- power-distribution method,
- optional mounted-laser charging lead.

---

# 15. Build sequence

## Phase 1 — fit coupons
Print/test:
1. SG90 cavity / mounting-ear coupon.
2. Laser cradle ring/clip coupon.
3. Passive-pivot tolerance samples.
4. Horn-to-platform interface test.

## Phase 2 — upper mechanism
Print:
- tilt fork,
- cradle,
- passive pivot,
- rotating platform.

Validate:
- laser insertion/removal,
- switch access,
- micro-USB access,
- tilt sweep,
- wire clearance,
- wobble/backlash.

## Phase 3 — pan base
Print:
- base enclosure,
- service lid,
- wall-power insert/module.

Validate:
- lower SG90 fit,
- platform concentricity,
- pan torque,
- wire routing,
- controller fit,
- serviceability.

## Phase 4 — complete V1
Combine upper mechanism and wall-powered base.

## Phase 5 — battery module
Design later against the interface already built into V1. Core turret remains unchanged.

---

# 16. CAD/output requirements

Move next into **parametric CAD**.

Rules:
- dimensions should be variables, not scattered magic numbers,
- each printable component should be a separate solid/body,
- export individual STLs,
- export combined 3MF with meaningful parts separate,
- retain editable source,
- generate fit-test STLs separately.

Suggested parameters:

```text
laser_diameter = 16.1
laser_length = 96.5
laser_switch_length = 14.5
laser_switch_width = 7.5
laser_switch_from_front = 26.4

servo_body_w = [verify actual SG90]
servo_body_d = [verify actual SG90]
servo_body_h = [verify actual SG90]

wall = [design value]
fit_clearance = [design value]
cradle_interference = [derive from prior ~15.45 mm fit]
pan_range = [TBD]
tilt_min = [TBD]
tilt_max = [TBD]
```

Source structure must allow controller replacement and future battery module without redesigning the upper turret.

---

# 17. Design principles that must not accidentally change

- Both servos are **SG90**.
- Laser OD is **16.1 mm**.
- Laser length is **96.5 mm**.
- Laser remains easily removable.
- Never solder or permanently wire the laser into the turret.
- Keep slide switch accessible.
- Keep rear micro-USB accessible.
- V1 is wall powered.
- Future battery module is additive/replaceable; **no core-turret reprint**.
- Lower servo pans the entire upper assembly.
- Tilt servo + passive pivot support laser from both sides.
- Keep upper mass low enough for SG90 pan duty.
- Prefer modular/serviceable parts over sealed monolithic construction.
- Target Bambu A1 / regular PLA.
- Concept images and web model are not dimensionally authoritative CAD.
