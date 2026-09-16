# Laser Turret — Build Tracker

Last updated: 2026-09-16, user reports quick tilt prototype is PRINTING (not yet complete).

## Status key
- [x] Confirmed by physical test / user report
- [ ] Not yet confirmed
- IN PROGRESS explicitly means not completed.

## Calibration completed
- [x] Laser clip fit: nominal 15.45 mm internal spring clip fits 16.1 mm laser body.
- [x] Servo body fit: smallest approximately 22.4 mm coupon fits user's SG90. Note that this is a coupon nominal dimension, not necessarily an exact measured servo body.
- [x] Passive pivot coupon v2 printed/tested: second-largest hole, nominal 3.35 mm, fits best around nominal 3.0 mm peg.
- [x] SG90 STEP/SolidWorks CAD files and visual reference provided by user; horn design shown in reference.
- [ ] Horn-to-printed-cradle screw/hole geometry validated on physical assembly. CAD supplied, but do not claim finished physical verification.

## Upper tilt prototype: quick_tilt_test_v01
Four STLs provided previously in laser_turret_quick_tilt_test_v01.zip:
- `01_fork_base.stl`: IN PROGRESS printing; no print success confirmed.
- `02_passive_upright.stl`: IN PROGRESS printing; inferred name based on four-part arrangement, verify precise ZIP filename if needed.
- `03_servo_upright.stl`: IN PROGRESS printing; no print success confirmed.
- `04_laser_cradle_horn_TEST_FIT.stl`: IN PROGRESS printing; not a verified final horn mount.

Bambu Studio initially warned of intersecting print paths between 03 and 04. User subsequently reported 'ok printing'; assume rearrangement resolved enough to print, but final plate outcome not confirmed. Do not claim print quality, functional assembly or an under-one-hour print time.

### Intended assembly (schematic, not verified assembly drawing)
```
              LASER (owned; clip test fits)
                       ||
                [04 TILT CRADLE]
                 o             o
                 |             |
      [03 SERVO UPRIGHT]   [02 PASSIVE UPRIGHT]
          SG90 + horn         3.35 mm hole
                 \             /
                  [01 FORK BASE]
                        |
                 [PAN STAGE: FUTURE]
                        |
             [ELECTRONICS BASE: FUTURE]
```
The exact horn-to-cradle connection and assembly of all four parts must be checked physically. Don't power servo or laser during initial fitting; never aim laser at people or pets' eyes.

## Next physical test, when print finishes
- [ ] Allow plate to cool, remove 4 pieces, photograph them laid out.
- [ ] Check any failed/warped/floating elements before fitting; do not sand/glue prematurely.
- [ ] Dry-fit two uprights in fork base.
- [ ] Dry-fit cradle and passive peg/hole, verify free tilting with minimal wobble.
- [ ] Install SG90 and compare real horn with cradle interface; document missing fastening details and identify screws needed.
- [ ] Clip laser OFF into cradle; ensure switch and USB access, range of motion and balance.
- [ ] Revise CAD based on actual fit. Only after validated mounting, move to powered tilt test and then direct-drive pan base.

## Already owned / procured
User owns 4 SG90 servos, rechargeable laser pointer, wall supply, PLA, assorted screws. Has ordered Seeed XIAO ESP32-C3 with pre-soldered headers, Dupont jumpers and lever connectors; delivery/arrival not yet confirmed. Core architecture is two-axis SG90, removable laser, wall-powered V1 and future battery interface without reprinting core.

When user requests progress, update this file with user-confirmed results; do not mark printing as completed until they report it. Refer to PROJECT_STATE.md for full design constraints and measurements.