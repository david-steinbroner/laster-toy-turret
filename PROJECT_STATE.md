# Laser Turret — Living Project State

**Canonical source of truth for this project. Read this file first in every new Laser Turret chat. Update it when the user says `wrap`.**

**Repository:** `david-steinbroner/laster-toy-turret`  
**Last updated:** 2026-09-15  
**Current phase:** Physical fit validation / Phase 1 coupons  
**V1 target:** Wall-powered 2-axis pan/tilt cat laser turret using the user's removable rechargeable laser pointer. Future battery power must be possible **without reprinting the core turret**.

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

# Latest checkpoint — 2026-09-15 late session

## Physical validation completed / underway
- **Laser spring-clip coupon printed and physically tested: FITS.**
- Coupon geometry used the previously successful approximately **15.45 mm internal spring-clip diameter** around the confirmed **16.1 mm laser body**.
- This is now a validated baseline for the removable laser cradle. Do not reopen this fit unless the full cradle geometry introduces a new interference.
- **SG90 clearance coupon is currently printing.** It contains three candidate body clearances:
  - A = **+0.20 mm per side**
  - B = **+0.35 mm per side**
  - C = **+0.50 mm per side**
- User will report which is the smallest clearance that allows the SG90 to insert/remove by hand without force or rattle.
- First passive-pivot coupon had a modeling defect: printed pegs were floating/not attached. **Do not use that file.**
- Corrected pivot-only STL was generated as `Laser_Turret_Passive_Pivot_Coupon_v2.stl` with:
  - 3.0 mm diameter × 7.0 mm tall pegs,
  - pegs fused to 4.0 mm bases,
  - hole sizes 3.15 / 3.25 / 3.35 / 3.45 mm,
  - thin breakaway bridges between samples.
- Passive-pivot v2 still needs to be printed/tested.

## Servo reference locked for CAD
- User supplied the GrabCAD Tower Pro SG90 model and uploaded the actual CAD package:
  - `SG90 - Micro Servo 9g - Tower Pro.STEP`
  - SolidWorks assembly/part files as supplemental references.
- Use the **uploaded STEP model as the authoritative nominal SG90 mechanical reference** for CAD rather than asking the user to remeasure generic servo body dimensions.
- Still validate real printed fit against the user's physical servos because SG90 clone tolerances vary.
- User already owns **4 SG90 servos**. Do not suggest buying more for V1 unless a servo fails.

## Additional turret reference uploaded
- User uploaded `Laser Turrent 1.0.f3d` plus screenshot of a compact pan/tilt design.
- Design review conclusion: borrow the **compact upper tilt geometry** idea, especially side-mounted tilt servo + opposite passive support + low centered payload, but **do not copy the large geared base**.
- Preferred hybrid architecture remains:
  - simple direct-drive SG90 pan stage below,
  - compact fork/upright upper mechanism,
  - side-mounted tilt SG90,
  - passive pivot opposite,
  - purpose-built removable laser cradle,
  - modular electronics/power base.

## Electronics / shopping decisions
User wants to avoid soldering where practical.

Already owned before this session:
- **4× SG90 servos**,
- **5 V wall supply**,
- PLA,
- assorted small machine screws/hardware,
- soldering equipment if absolutely necessary.

User has now **ordered the remaining prototype electronics/wiring items** discussed this session:
- **1× Seeed Studio XIAO ESP32-C3 with pre-soldered headers**,
- **Dupont jumper wires**,
- **lever-style wire connectors** suitable for stranded wire, used as no-solder 5 V / ground distribution.

Power-distribution concept:
- one multi-port lever connector for **+5 V**,
- one multi-port lever connector for **GND**,
- wall supply feeds both rails,
- both SG90 servos receive 5 V directly from the distribution rail,
- controller shares ground,
- do **not** route servo load current through the XIAO regulator.

Current no-solder-first preference:
- pre-soldered XIAO headers,
- Dupont jumpers for signal/prototyping,
- lever connectors for low-voltage power distribution,
- only solder if later packaging/reliability truly requires it.

## Material
- **Regular PLA** remains the default target material for Bambu A1.
- PLA+ is not required for V1 unless a particular snap-fit or impact-loaded part later proves brittle.

## Budget expectation
- Original project goal of roughly **$25 in new electronics/hardware** remains valid because the user already owned servos, wall supply, screws, and filament.
- Do not expand the shopping list with speculative bearings, gears, JST kits, special fasteners, etc. unless testing demonstrates a need.

## Current next steps
1. **Wait for SG90 clearance coupon result.** Record whether A / B / C is best.
2. Print/test **passive-pivot coupon v2** and choose the smallest hole that rotates freely with minimal wobble.
3. User will provide **laser pointer weight** when convenient. Use it for balance / torque sanity checking, but it does not block current fit testing.
4. Select/inspect the actual SG90 horn to lock the horn-to-platform interface. The uploaded SG90 CAD may help, but use the user's actual supplied horn style if there is any mismatch.
5. Once laser fit + SG90 fit + passive pivot are validated, move immediately into the **first recognizable upper turret assembly**, not more abstract concept work:
   - compact tilt fork/uprights,
   - side-mounted SG90,
   - passive pivot opposite,
   - removable cradle using the validated 15.45 mm spring-clip behavior,
   - rotating pan platform interface.
6. Keep prints small/modular so the user can see progress quickly and avoid long failed prints.
7. After upper mechanism validation, build the direct-drive pan base and electronics/service bay with future battery-module interface preserved.

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
- Prefer multiple small printable parts/plates over one huge print job; user wants fast visible progress and early assembly.
- Final deliverables should eventually include editable parametric CAD, individual STLs, a combined 3MF with meaningful parts kept separate, and small fit-test parts before large prints.

---

# 2. Locked mechanical architecture

Architecture is inspired by supplied OpenMV / GrabCAD / Fusion pan-tilt references, but geometry must be purpose-built for this laser.

## Pan axis
- One **SG90** sits vertically inside the base.
- Its horn drives a rotating upper platform directly unless testing proves a reduction stage is necessary.
- The entire upper assembly rotates with it: tilt fork, tilt SG90, passive pivot, cradle, laser.
- Keep upper mass low and reasonably balanced.
- Use gentle software acceleration.
- Physically validate SG90 pan torque during prototype testing.
- Avoid a large geared ring/base unless direct drive proves inadequate.

## Tilt axis
- Compact U-shaped fork/uprights on rotating pan platform.
- One **SG90** mounted on one side.
- Opposite side uses a **passive pivot / bushing feature**.
- Laser cradle spans the fork.
- Laser centerline should align closely with the tilt axis so the laser rotates in place rather than sweeping through solid fork walls.
- Passive side supports the cradle so the tilt servo shaft is not acting as a cantilever.
- Favor the compact upper-mechanism proportions seen in the uploaded Fusion reference, not its large geared lower base.

## Laser cradle
- Removable / quick release.
- Must not block the slide switch.
- Must leave rear micro-USB charging port accessible.
- Should account for pocket clip/lanyard geometry if those remain attached.
- No permanent electrical connection to laser.
- Validated spring-clip baseline: approximately **15.45 mm ID** around the **16.1 mm laser body** fits the actual pointer.

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
| Validated spring-clip ID | **~15.45 mm fits actual laser** |

Reference photos also show:
- pocket clip,
- rear lanyard attachment,
- sliding multifunction switch,
- centered rear micro-USB port.

Still useful before final cradle CAD:
- pocket-clip protrusion/location if clip stays installed,
- lanyard clearance if lanyard hardware stays installed,
- approximate laser mass for servo-load sanity check.

---

# 4. Servos

## Locked servo choice
**Pan = SG90. Tilt = SG90.**

User already owns **4 physical SG90 servos**.

Nominal reference is now the uploaded Tower Pro SG90 STEP model. Previously supplied drawings suggested approximately:
- body width: **22.5 mm**,
- body depth: **11.8–12 mm**,
- body height: about **22.7–22.8 mm**,
- mounting-ear overall span in one diagram: **31.8 mm**,
- standard 3-wire connector.

SG90 clone housings vary, so real physical fit still wins over nominal CAD.

### Current validation
SG90 body clearance coupon is printing with:
- A = +0.20 mm per side,
- B = +0.35 mm per side,
- C = +0.50 mm per side.

Use the smallest one that inserts/removes without force and does not rattle.

### Horn
Exact horn interface is **not locked yet**. Need to validate:
- actual supplied horn style,
- thickness,
- effective diameter / arm length,
- hole pattern,
- center screw clearance.

---

# 5. Power architecture

## V1
**Wall powered only.** User already owns a suitable 5 V wall supply.

Concept:

```text
wall supply 5 V
   |
   +---- +5 V lever-connector rail ----> pan SG90
   |                                  -> tilt SG90
   |                                  -> controller power as appropriate
   |
   +---- GND lever-connector rail ----> pan SG90
                                      -> tilt SG90
                                      -> controller GND

XIAO GPIO ----------------------------> pan servo signal
XIAO GPIO ----------------------------> tilt servo signal
```

Rules:
- Do not route servo current through the XIAO regulator.
- Servos and controller share ground.
- Provide enough current headroom for two SG90 transient loads.
- Favor no-solder lever connectors / jumper wiring during prototype phase.

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

**Seeed Studio XIAO ESP32-C3 with pre-soldered headers** is now the selected V1 controller and has been ordered.

Reasons:
- tiny footprint,
- enough GPIO for two servo signals,
- USB-C programming,
- Wi-Fi/Bluetooth available for future control,
- pre-soldered headers support the user's preference to avoid soldering.

---

# 7. Soldering and serviceability

- User prefers **not to solder** if a practical no-solder route exists.
- Prototype wiring should therefore use pre-soldered XIAO headers, Dupont jumpers, and lever connectors.
- Laser itself must never be soldered into the turret.
- Servos, controller, and power module should remain replaceable.
- Soldering remains a fallback only if final compact packaging/reliability requires it.

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

---

# 9. Expected printed parts

Likely V1 parts:
1. **Base enclosure** — lower SG90 mount, controller/power routing, future battery interface.
2. **Service lid / access cover**.
3. **Rotating pan platform** — interfaces to lower SG90 horn.
4. **Tilt fork / compact uprights** — SG90 on one side, passive pivot on the other.
5. **Removable laser cradle** — validated clip fit, switch + charging access.
6. **Passive pivot / bushing piece**.
7. **V1 wall-power module / insert** — removable/replaceable.
8. **Future battery module** — later, same interface, no core reprint.

Possible extras:
- charge-cable keeper,
- wire clips / strain relief,
- servo-horn adapter.

---

# 10. Legacy work worth preserving

## Laser Clip V3 / current fit coupon
- 16.1 mm pointer.
- ~15.45 mm spring-clip ID.
- This geometry has now been **revalidated physically in the current fit coupon**.

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

**Superseded by the current compact U-fork/upright architecture. Do not revert unless explicitly requested.**

## Arduino Uno base
Obsolete for final V1 because controller is now XIAO ESP32-C3.

---

# 11. Reference models

## OpenMV / GrabCAD reference
Use only as mechanical topology reference:
- vertical pan servo,
- rotating upper stage,
- U-fork,
- side-mounted tilt servo,
- opposite passive pivot.

## Tower Pro SG90 GrabCAD model
User supplied the GrabCAD link and uploaded the STEP/SolidWorks files. Treat the uploaded STEP as the nominal servo reference.

## Uploaded Fusion turret (`Laser Turrent 1.0.f3d`)
Useful ideas to borrow:
- compact upper tilt assembly,
- side-mounted servo near load,
- passive support opposite,
- low centered payload,
- triangular/braced uprights if useful.

Do not copy its large geared base unless direct-drive pan fails testing.

---

# 12. Interactive concept model

Latest live visualization:
`https://laser-turret-v3-davidsteinbroner-2472.vercel.app`

Reference only. **Never treat the Three.js model as manufacturing-authoritative geometry.**

---

# 13. Current manufacturing status

Phase 1 is actively underway.

Completed:
- laser dimensions substantially defined,
- SG90 nominal CAD reference supplied,
- laser clip fit physically validated,
- first fit-test STLs created,
- corrected passive-pivot STL created after first peg-attachment defect was caught.

Still unresolved before upper-mechanism CAD is locked:
- SG90 printed clearance selection,
- passive-pivot printed clearance selection,
- horn-to-platform interface,
- approximate laser mass / balance sanity check,
- pocket clip / lanyard interference in the full cradle,
- final wire routing and service details.

---

# 14. Build sequence

## Phase 1 — fit coupons
1. **Laser cradle ring/clip coupon — DONE, fits.**
2. **SG90 cavity clearance coupon — PRINTING / awaiting A-B-C result.**
3. **Passive-pivot tolerance samples v2 — generated, needs print/test.**
4. Horn-to-platform interface test — next after actual horn style is confirmed.

## Phase 2 — upper mechanism
As soon as coupon results are known, build:
- compact tilt fork/uprights,
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
- XIAO + lever-connector fit,
- serviceability.

## Phase 4 — complete V1
Combine upper mechanism and wall-powered base.

## Phase 5 — battery module
Design later against the interface already built into V1. Core turret remains unchanged.

---

# 15. CAD/output requirements

Move from fit tests into **parametric CAD** as soon as the SG90/pivot results are known.

Rules:
- dimensions should be variables, not scattered magic numbers,
- each printable component should be a separate solid/body,
- export individual STLs,
- export combined 3MF with meaningful parts separate,
- retain editable source,
- generate fit-test STLs separately,
- prefer small/fast validation prints before committing to large prints.

Current parameter set:

```text
laser_diameter = 16.1
laser_length = 96.5
laser_switch_length = 14.5
laser_switch_width = 7.5
laser_switch_from_front = 26.4
cradle_clip_id_validated = 15.45

servo_nominal_reference = uploaded Tower Pro SG90 STEP
servo_fit_clearance = [await A/B/C physical result]

passive_pivot_pin = 3.0
passive_pivot_hole = [await 3.15/3.25/3.35/3.45 physical result]

laser_mass = [user will provide]
pan_range = [TBD]
tilt_min = [TBD]
tilt_max = [TBD]
```

Source structure must allow controller replacement and future battery module without redesigning the upper turret.

---

# 16. Design principles that must not accidentally change

- Both servos are **SG90**.
- User owns **4 SG90s** already.
- Laser OD is **16.1 mm**.
- Laser length is **96.5 mm**.
- ~15.45 mm spring-clip ID is now physically validated on the actual laser.
- Laser remains easily removable.
- Never solder or permanently wire the laser into the turret.
- Keep slide switch accessible.
- Keep rear micro-USB accessible.
- V1 is wall powered from user's existing 5 V supply.
- XIAO ESP32-C3 with pre-soldered headers is selected/ordered.
- Prototype wiring should avoid soldering where practical.
- Future battery module is additive/replaceable; **no core-turret reprint**.
- Lower SG90 pans the entire upper assembly.
- Tilt SG90 + passive pivot support laser from both sides.
- Keep upper mass low enough for SG90 pan duty.
- Prefer direct-drive pan unless testing proves otherwise.
- Prefer modular/serviceable parts over sealed monolithic construction.
- Prefer multiple small prints / fast visible progress over one huge print.
- Target Bambu A1 / regular PLA.
- Concept images and web model are not dimensionally authoritative CAD.
