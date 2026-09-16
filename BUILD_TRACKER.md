# Laser Turret — Living Build Tracker

**Last updated: September 16, 2026 ~16:17 Austin. CURRENT: horn recess coupon V2 provided; user was just instructed how to add a brim; V2 print/result NOT reported.** Start with [latest handoff](SESSION_HANDOFF_2026-09-16.md). `PROJECT_STATE.md` includes an older September 15 checkpoint with now-obsolete 'coupons printing' claims; this tracker and handoff supersede those statuses. Do not mistake a prior assistant's claims of mesh verification for independently verified printability.

## Confirmed tests and components
- [x] Removable laser clip fits: nominal 15.45 mm clip ID, laser 16.1 mm diameter and 96.5 mm length.
- [x] Smallest SG90 body-fit coupon (~22.4 mm nominal) fits user's servo.
- [x] Second-largest passive pivot coupon chosen: nominal 3.35 mm bore with 3.0 mm peg.
- [x] User owns four SG90 servos and multiple physical horn styles; servo CAD previously supplied.
- [x] Straight double-sided horn selected as prototype candidate. User **physically confirmed two horn mounting holes line up with cradle disc holes.** Short single horn too short. Long horn may need later clearance/trim test; DO NOT cut yet.
- [x] Horn's raised central circular boss (~0.5 mm tall by user estimate) prevents horn arms sitting flush on original flat cradle disc. Recess is REQUIRED; boss diameter and correct recess fit still UNVERIFIED.

## Four-piece quick upper tilt prototype
Files previously supplied in chat, NOT confirmed committed to repo: `01_fork_base.stl`, `02_passive_upright.stl`, `03_servo_upright.stl`, `04_laser_cradle_horn_TEST_FIT.stl` and cradle test-fit 3MF.
- [x] At least one fork base physically printed successfully: user said its two sides were good; user proceeded to print another. Exact count of satisfactory bases not independently established.
- [x] At least one upright physically printed, but underside facing support has rough/ugly surface.
- [x] User physically handled fork/cradle parts, demonstrated cradle has passive peg on ONE side, horn disc on OTHER side. Single peg is intentional. Photo shows several printed parts. Do not infer whole assembly complete.
- [ ] Servo upright final print success / full frame fit and squareness verified.
- [ ] Cradle passive pivot installed between complete uprights and free motion checked.
- [ ] Horn fastened flush to cradle, center servo screw access checked, servo installed and powered test completed.
- [ ] Laser OFF inserted; switch, charging port, clearance/balance checked.

**Upright CAD design defect:** protruding narrow rail is the only build-plate contact in current orientation; broad body hangs over plate and needs supports, leaving ugly supported underside. Earlier assistant incorrectly advised 'lay broad face flat', but that is not possible with this geometry. Redesign the upright's geometry/orientation or split rail into separate printable piece rather than pretending support adjustments fix the root cause. Until reworked, supported surface may be rough. Previous suggested 0.20 mm top Z support gap at 0.20 layer, 3 top interface layers; these were suggestions, not proven successful.

## Horn-interface test coupons
- V1 `horn_disc_recess_coupons.stl` / `.scad` previously delivered via chat; user reports print result: 1 entirely spaghetti, 1 OK, 2 half spaghetti. DO NOT call V1 successful.
- V2 `horn_disc_recess_coupons_v2.stl` / `.scad` previously delivered via chat; NOT confirmed copied into GitHub and NOT yet reported printed. Claimed design changes: four separately numbered discs; disc outer diameter 20→24 mm; thickness 3.2→4 mm; gap between discs 5→10 mm; hub recess diameters increased 1 mm; arm channels widened from 5.5 to 6.5–7.2 mm and tapered; enlarged recessed ID numbers 1–4. These values are prior assistant-reported and need actual source/STL inspection if regenerating; no guarantee of successful printing. Previous assistant asserted 'watertight' without a verified sliced toolpath/physical print.
- V2 nominal center recess variations (from earlier V1 values +1 mm) may be 6.5, 7.5, 8.5, 9.5 mm, but inspect CAD before claiming exact geometry; arm recess and hub dimensions varied together so test doesn't isolate variables.
- [ ] V2 successfully prints / adhesion verified.
- [ ] User tests actual horn on numbered coupons, reports which allows both arms flush and center boss clear, holes align, no interference; then update cradle disc CAD with chosen result. Do not assume success or screw cradle before verification.

## Bambu A1 / regular PLA print recipe for V2 coupons (latest user question was HOW TO ADD BRIM)
In Bambu Studio **Prepare → Process: Global** (all four discs) → **Others → Bed Adhesion**: Brim type **Outer brim only**; Brim width **5 mm**; Brim-object gap **0.1 mm**. Then Slice Plate → Preview and verify brim surrounds EACH disc, disks lay flat with numbered faces up, no supports. Layer height 0.20 mm, 3 wall loops, 15% infill. Clean build plate first. Brims may merge if close; use Arrange/spread if needed. This is a proposed mitigation for adhesion, not a guarantee; if spaghetti repeats get photo and investigate first-layer adhesion, orientation, geometry and slicer preview before another revision.

## Next action
User may return with V2 print results, a photo, or difficulty finding/applying brim. Ask specifically whether V2 printed and which numbered coupon lets straight horn arms sit flush, if the print succeeded. If failure, diagnose from photos/slicer preview. After fit, revise horn-disc/cradle CAD, AND separately redesign rail-balanced upright for support-free printing. Do not call full tilt assembly complete or powered. Keep docs and actual CAD/STL assets synced when accessible; do not invent sandbox links to past-turn attachments.

## Long-term constraints
Bambu A1 regular PLA; compact U-fork; SG90 tilt plus SG90 direct-drive pan; removable laser (OFF during fit), preserve slider/USB; XIAO ESP32-C3 pre-header unit ordered; wall 5 V servo distribution with common ground, not via microcontroller regulator; future battery interface in V1; modular quick prints, verify before claiming success.