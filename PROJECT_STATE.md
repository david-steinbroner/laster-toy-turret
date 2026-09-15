# Laser Turret — Living Project State

**Canonical project record.** Read this file first whenever continuing the Laser Turret project. Update this file at the end of a work session or whenever a meaningful design decision, measurement, test result, or artifact changes.

**Repository:** `david-steinbroner/laster-toy-turret`  
**Last updated:** 2026-09-15  
**Current phase:** Pre-CAD / fit-test definition  
**V1 goal:** Wall-powered, 2-axis pan/tilt laser turret for cat play, with a removable rechargeable laser pointer and a future battery add-on that does **not** require reprinting the core turret.

---

## Working protocol

### Start of a new ChatGPT session
User can simply say:

> continue Laser Turret

Assistant should:
1. Fetch and read this `PROJECT_STATE.md` first.
2. Treat it as the source of truth over older chat summaries or concept images.
3. Inspect relevant repo files created since the last session before making changes.
4. Continue from **Current next steps** rather than redesigning the project from scratch.

### End of a session
User can simply say:

> wrap

Assistant should update this file with:
- new measurements,
- decisions made,
- files/artifacts created,
- test results,
- current blockers,
- the exact next steps.

The user should not need to copy/paste chat history between sessions.

---

# 1. Product intent

Build a compact 3D-printable laser turret that automatically pans and tilts the user's existing rechargeable laser pointer.

Core product requirements:
- The laser pointer must remain **fully removable** for handheld play.
- **Nothing may be soldered to or permanently modify the laser pointer.**
- V1 is **wall powered only**.
- The physical design must anticipate a future **battery module**.
- Adding the battery later must require printing only the new battery/power module, **not the entire turret/base again**.
- Both motion axes use small hobby servos.
- The design should be compact and serviceable, not over-engineered.
- Target printer/material: **Bambu A1, regular PLA**.
- Printable parts should remain modular and independently editable where practical.
- Final manufacturing deliverables should eventually include:
  - editable parametric CAD source,
  - individual STLs,
  - combined 3MF with meaningful parts kept separate,
  - small fit-test STLs before large prints.

---

# 2. Locked mechanical architecture

The architecture is inspired by the OpenMV pan/tilt assembly, but it must be redesigned around this laser pointer and the user's SG90 servos.

## Pan axis
- One **SG90** sits vertically inside the base.
- Its output horn drives a rotating upper platform.
- The **entire upper assembly** rotates with that platform:
  - tilt fork,
  - tilt SG90,
  - passive pivot,
  - laser cradle,
  - laser pointer.
- Keep the upper assembly light and reasonably balanced so an SG90 can drive pan without excessive load.
- Use gentle acceleration in software.
- Pan torque/load should be validated physically during prototype testing.

## Tilt axis
- A U-shaped fork mounts on the rotating pan platform.
- One **SG90** is mounted on one side of the fork.
- The opposite side uses a **passive pivot / bushing / bearing feature**.
- The laser cradle spans between the two sides.
- The laser centerline should align with the tilt axis so the pointer rotates in place instead of sweeping through the fork walls.
- The passive side supports the cradle so the tilt-servo shaft is not carrying the whole assembly as a cantilever.

## Laser cradle
- Laser remains removable.
- Cradle must not block:
  - the slide switch,
  - the centered rear micro-USB charging port,
  - pocket clip / lanyard hardware if those stay installed.
- No permanent electrical connection to the laser.
- A future short removable charging lead may plug into the laser while it is mounted.

---

# 3. Confirmed laser-pointer measurements

These values supersede provisional numbers from earlier concept drawings.

| Item | Confirmed value / requirement |
|---|---|
| Main body diameter | **16.1 mm** |
| Overall length | **96.5 mm** |
| Switch type | **Sliding switch**, not a push button |
| Sliding-switch assembly size | **14.5 mm × 7.5 mm** |
| Switch start position | Begins **26.4 mm from the beam/front end** |
| Charging connector | **Micro-USB** |
| Charging connector location | **Centered on rear/end face** |
| Laser modification allowed | **None**; laser must remain removable |

Reference-product image also shows:
- pocket clip,
- lanyard attachment at rear,
- sliding multifunction switch,
- micro-USB port on the rear face.

### Still useful to measure before final cradle CAD
- Exact pocket-clip protrusion/location if it stays attached while mounted.
- Lanyard hardware clearance if it stays attached while mounted.
- Approximate laser weight for servo-load sanity checking.

### Legacy fit-test knowledge
Earlier **Laser Clip V3** reportedly fit this pointer successfully:
- nominal pointer OD: **16.1 mm**,
- successful clip internal diameter: about **15.45 mm**,
- two screw slots: **26 mm apart**.

Treat 15.45 mm as empirical spring-clip information, not automatically as the final cradle ID.

---

# 4. Servo selection and reference geometry

## Locked servo choice
**Both pan and tilt servos are SG90 micro servos.**

User supplied SG90 dimension diagrams. Useful reference dimensions shown include approximately:
- body width: **22.5 mm**
- body depth: **11.8–12 mm**
- body height: about **22.7–22.8 mm**
- mounting-ear overall span shown in one diagram: **31.8 mm**
- servo lead length shown: about **0.25 m**
- standard 3-wire servo connector

SG90 clones vary. Do **not** create a tight final cavity from internet dimensions alone.

### Required validation approach
Before final base/fork CAD:
1. Measure the actual SG90s in hand, or
2. Print a simple SG90 fit coupon based on the supplied diagrams.

### Servo horn
The exact horn is not yet locked.
Need to select the actual horn from the user's supplied horn set and validate:
- horn type,
- thickness,
- effective diameter/arm length,
- mounting-hole pattern,
- center screw clearance.

---

# 5. Power architecture

## V1
**Wall powered only.**

The core turret must have a modular power interface from the beginning.

Conceptual electrical architecture:

```text
wall power
   |
   v
power input / power module
   |
   +---- regulated 5 V servo power ----> pan SG90
   |                                  -> tilt SG90
   |
   +---- controller power
            |
            +---- pan signal
            +---- tilt signal
```

Important:
- Do not power servo current through a tiny controller's onboard regulator.
- Servos and controller share common ground.
- Need adequate 5 V current headroom for two SG90s and transient loads.
- Exact wall-power connector/cable is not locked yet.

## Future battery module requirement
V1 must include a standardized **battery/power expansion interface**.

Desired physical logic:

```text
CORE TURRET  <--- never reprinted for the battery upgrade
    |
    +-- V1 wall-power insert/module
    |
    +-- future battery/power module
```

Possible forms:
- rear cartridge,
- bottom drawer,
- bolt-on lower pod,
- removable service/power bay.

The exact form is still a design choice. The non-negotiable requirement is that the core base contains the mounting interface and wire pass-through from V1 onward.

---

# 6. Controller

A full Arduino Uno is considered unnecessarily large for the finished turret.

Leading concept discussed:
- **Seeed XIAO ESP32-C3** because it is tiny and preserves future options like wireless controls.

Other tiny boards were discussed, but **no controller is purchased/locked yet**.

Controller requirements:
- at least two servo signal outputs,
- enough program memory for the movement routine,
- easy programming/update path,
- compact enough to fit the base,
- should not directly supply servo current.

---

# 7. Soldering / serviceability

- User owns a soldering gun and is open to soldering turret wiring.
- Laser itself must **never** be soldered into the turret.
- Preferred final approach is likely soldered turret wiring with removable connectors for service.
- Servos, controller, and power module should remain replaceable.

---

# 8. Laser charging and activation

## Charging stretch goal
Desired if practical:
- Allow the laser to be charged while mounted.
- Laser connector: **micro-USB**, centered on rear face.
- Prefer a short removable charging lead.
- Most sensible to allow mounted-laser charging while turret is plugged into wall power.
- This should not block a working V1 if it makes the first mechanism unnecessarily complex.

## Beam on/off
The laser uses a **manual sliding multifunction switch**.

Current physical design does **not** include electronic beam switching because the pointer is not being modified.

Therefore V1 must keep the slider accessible.

If automatic beam switching is desired later, options are:
1. add a small mechanical actuator to move the laser slider, or
2. modify the laser electrically, which is currently against the project requirement.

Any “Show Beam” control in the web visualization is only a visualization feature, not a physical actuator design.

---

# 9. Current printable-part concept

Likely V1 parts:

1. **Base enclosure**
   - lower SG90 mount,
   - controller/power routing,
   - future battery-module interface.

2. **Service lid / access cover**
   - electronics and lower servo remain serviceable.

3. **Rotating pan platform**
   - interfaces with lower SG90 horn,
   - carries tilt fork.

4. **Tilt fork**
   - tilt SG90 on one side,
   - passive pivot on the other.

5. **Removable laser cradle**
   - for 16.1 mm laser body,
   - leaves slide switch and rear charging port accessible.

6. **Passive pivot / bushing piece**
   - supports non-servo side of tilt axis.

7. **V1 wall-power module / insert**
   - removable/replaceable.

8. **Future battery module**
   - not required for V1,
   - designed later to mate to the same expansion interface.

Potential extras:
- charge-cable keeper,
- wire clips / strain relief,
- servo-horn adapter if needed.

---

# 10. Legacy design work worth preserving

These are useful historical tests but several are superseded by the selected OpenMV-style architecture.

## Laser Clip V3
- Successful fit on 16.1 mm laser.
- About 15.45 mm ID reportedly worked.
- Screw slots 26 mm apart.

## Lower servo/base — Option C V7
Reported as working:
- open-top SG90 cradle,
- rear cable exit,
- shorter ~13 mm towers.

## Older upper SG90 bracket
File previously called:
`sg90_sideways_bracket_editable_parts_v1.3mf`

Features:
- upper SG90 horizontal/on its side,
- horn side mostly open,
- walls/floor separated into editable Bambu Studio bodies,
- unresolved rear wire-notch position.

**This bracket is largely superseded by the new U-fork design. Do not revert to it unless explicitly requested.**

## Arduino Uno base
Earlier peg-position work for an Uno base is likely obsolete because the finished design is moving to a much smaller controller.

---

# 11. OpenMV / GrabCAD reference assembly

Reference package previously supplied:
`pan-tilt-assembly-1.snapshot.9.zip`

Useful parts included:
- `Pan Tilt Base.stl/.step`
- `Pan Tilt Arm.stl/.step`
- `Pan Tilt Tray.stl/.step`
- stand/adaptor files
- assembly-guide images

Use this as a **mechanical topology reference only**:
- vertical pan servo in base,
- rotating upper stage,
- U-shaped fork,
- side tilt servo,
- opposite passive pivot.

Do **not** simply scale/copy the OpenMV camera geometry. The laser version should be smaller, lighter, and purpose-built.

---

# 12. Interactive concept model

Latest live concept URL:

`https://laser-turret-v3-davidsteinbroner-2472.vercel.app`

It includes:
- touch orbit / pinch zoom,
- pan/tilt sliders,
- auto motion,
- beam visualization,
- mechanism mode,
- exploded view,
- front/side/rear/top views.

Feedback/history:
- early web version had unrealistic geometry and laser clipping through structure,
- later versions improved mechanical hierarchy,
- mechanism/exploded views are still imperfect,
- user decided continued web-model polishing is less important than moving into real CAD.

**The Three.js/web model is visual reference only and is not manufacturing-authoritative CAD.**

---

# 13. Technical drawing / adversarial review status

Technical concept sheets were created with:
- assembled views,
- orthographic views,
- exploded assembly,
- part breakdowns,
- base cutaway,
- provisional dimensions,
- adversarial redline review.

The adversarial review conclusion was:

**NOT READY TO PRINT YET**

Main issues identified at that time:
- exact dimensions missing on many features,
- fit tolerances/clearances undefined,
- servo horn/spline interface not finalized,
- screw sizes/hole diameters not finalized,
- wall thickness/minimum printable features undefined,
- new cradle retention not yet validated,
- passive pivot geometry/fit incomplete,
- wire-routing clearances not verified,
- service-lid mounting method not finalized,
- pan-axis load margin not physically validated,
- print orientations/support strategy not defined,
- final chamfers/fillets/elephant-foot allowances not defined,
- no final watertight CAD solids yet.

### Items resolved since that review
- laser length: **96.5 mm**
- laser diameter: **16.1 mm**
- switch type/size/location: substantially defined
- charging connector type/location: known
- servo model for both axes: **SG90**
- V1 power: explicitly **wall powered**
- battery upgrade: explicitly **modular**

---

# 14. Remaining measurements / choices before final manufacturing CAD

## Genuine high-priority unknowns
1. Actual SG90 fit on the user's specific servos, especially mounting ears.
2. Exact servo horn to use and its geometry.
3. Laser pocket-clip/lanyard clearances if they remain installed while mounted.
4. Approximate laser mass.
5. Desired pan and tilt motion limits, unless chosen during design.

## Can be chosen during engineering rather than measured by user
- base diameter/height,
- fork wall thickness,
- platform thickness,
- PLA clearances/tolerances,
- screw strategy,
- service-lid fastening method,
- print orientation,
- chamfers/fillets,
- cable routing,
- modular power-interface geometry.

## Electronics still to lock
- controller model,
- wall-power connector/cable,
- power distribution method,
- optional laser-charging lead implementation.

---

# 15. Recommended build sequence

Do not jump directly to one large monolithic print.

## Phase 1 — fit coupons
Create and print:
1. SG90 cavity / mounting-ear fit coupon.
2. Laser cradle ring/clip coupon.
3. Passive-pivot tolerance samples.
4. Chosen horn-to-platform interface test.

## Phase 2 — upper mechanism
Print:
- tilt fork,
- cradle,
- passive pivot,
- rotating platform.

Manually validate:
- laser insertion/removal,
- slide-switch access,
- micro-USB access,
- tilt sweep,
- wire clearance,
- wobble/backlash.

## Phase 3 — pan base
Print:
- base enclosure,
- service lid,
- V1 wall-power insert/module.

Validate:
- lower SG90 fit,
- rotating-platform concentricity,
- pan torque,
- wire routing,
- controller fit,
- serviceability.

## Phase 4 — full V1
Combine upper mechanism and wall-powered base.

## Phase 5 — battery module
Design the battery upgrade around the expansion interface already built into the V1 core. The core turret stays unchanged.

---

# 16. CAD requirements

The next engineering work should move into **parametric CAD**.

Requirements:
- use variables/parameters for important dimensions,
- each printable component is its own body/solid,
- retain editable source,
- export individual STLs,
- export combined 3MF with meaningful parts separate,
- create fit-test STLs separately,
- design for Bambu A1 / PLA,
- do not treat concept images as exact geometry.

Suggested starting parameters:

```text
laser_diameter = 16.1
laser_length = 96.5
laser_switch_length = 14.5
laser_switch_width = 7.5
laser_switch_from_front = 26.4

servo_body_width = [verify actual SG90]
servo_body_depth = [verify actual SG90]
servo_body_height = [verify actual SG90]

wall = [engineering choice]
fit_clearance = [engineering choice]
cradle_interference = [derive from prior 15.45 mm fit result]
pan_range = [TBD]
tilt_min = [TBD]
tilt_max = [TBD]
```

---

# 17. Design principles that should not be accidentally changed

- Both servos are **SG90**.
- Laser OD is **16.1 mm**.
- Laser length is **96.5 mm**.
- Laser remains removable for handheld use.
- Never solder or permanently wire the laser into the turret.
- Keep the slide switch accessible.
- Keep rear micro-USB accessible.
- V1 is wall powered.
- Future battery module must be addable without reprinting the core turret.
- Lower servo pans the entire upper assembly.
- Tilt servo + passive pivot support the laser from both sides.
- Keep upper mass low enough for SG90 pan duty.
- Prefer modular/serviceable parts over sealed monolithic parts.
- Target printer/material: **Bambu A1 / PLA**.
- Old sideways-servo bracket is superseded.
- Web model and concept drawings are not dimensionally authoritative CAD.

---

# 18. Current next steps

1. Choose/measure the exact SG90 horn to use.
2. Either measure actual SG90 housing/ear geometry or build an SG90 fit coupon from the supplied diagrams.
3. Build the first four fit-test CAD parts:
   - SG90 fit coupon,
   - laser cradle coupon,
   - passive-pivot tolerance test,
   - horn/platform interface test.
4. Once those are validated, begin the parametric upper mechanism and modular base.
5. Keep the future battery interface in the base design from the first printable V1.

---

# 19. Session log

## 2026-09-15 — Repository initialization
- Established this file as the canonical living project record.
- Confirmed both servos are SG90.
- Confirmed laser dimensions and switch/charging-port data.
- Locked V1 as wall powered.
- Locked requirement that future battery upgrade must not require reprinting the core turret.
- Next work should be fit-test CAD, not more concept-only visualization.
