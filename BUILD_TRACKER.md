# Laser Turret — Living Build Tracker

**Last updated September 16, 2026 ~18:40 Austin. CURRENT STOP: V5 hub-only horn test disc delivered, user will print/test and report. NO V5 physical fit result yet.** Read [latest handoff](SESSION_HANDOFF_2026-09-16.md) first and historical requirements in [PROJECT_STATE.md](PROJECT_STATE.md). Historical Sep 15 status in PROJECT_STATE is superseded by these newer records.

## Physically validated
- [x] Removable laser clip fits: nominal 15.45 mm ID; laser diameter 16.1 mm, length 96.5 mm.
- [x] Smallest SG90 body-fit coupon (~22.4 mm nominal) fits.
- [x] Passive pivot: second-largest coupon, nominal 3.35 mm bore with 3.0 mm peg, fits best.
- [x] Straight double-sided servo horn selected; original cradle disc holes aligned physically. One-sided horn too short. Four SG90 servos owned; nominal CAD previously supplied.
- [x] Raised circular horn center boss (~0.5 mm tall user estimate) keeps arms from sitting flush on flat cradle disc.
- [x] V2 four-disc horn recess coupons were printed sufficiently for a fit test; **user reports DISC #2 IS BEST.** Do not infer all four printed perfectly or that #2 is fully flush: the user subsequently requested removing arm channels and enlarging the boss pocket.

## Horn-disc iteration: precise chronology
1. V1 four-disc `horn_disc_recess_coupons.stl/.scad`: user reported 1 full spaghetti, 1 OK, 2 half spaghetti.
2. V2 `horn_disc_recess_coupons_v2.stl/.scad`: prior reported change to 24 mm OD, 4 mm thick, four numbered samples with wider/tapered arm channels and enlarged boss pockets; user physically tested and chose **disc #2**. Earlier recommendation for printing: Bambu A1 regular PLA, 0.20 mm layer, no supports, 3 walls, 15% infill, clean plate; Others > Bed Adhesion > outer brim only 5 mm wide, brim-object gap 0.1 mm. These settings were advised, not independently proven cause of success.
3. V3 single disc `horn_disc_02_hub_only_v3.stl/.scad`: retain #2, REMOVE ALL horn-arm recesses, keep ONLY circular hub/boss pocket. Assistant reported OD 24 mm, thickness 4 mm, boss pocket 7.5 mm diameter x 0.7 mm deep, original two mounting holes, recessed `2H` marker. Fit not reported.
4. V4 `horn_disc_hub_only_10mm_14p5mm_v4.stl/.scad`: user requested hub recess diameter 10 mm and screw holes 14.5 mm center-to-center; no arm channels; OD 24 mm, thickness 4 mm, pocket depth 0.7 mm. Fit not reported.
5. **V5 LATEST** `horn_disc_hub_only_11mm_1mm_v5.stl/.scad`: user requested hub-only circular recess **11 mm diameter x 1 mm deep**, two screw holes **14.5 mm center-to-center**, disc **24 mm OD x 4 mm thick**, NO arm recesses. Assistant provided STL and editable SCAD in chat, asserted single watertight body flat at Z=0. **User says they will report how it prints/fits. V5 is untested physically; do not call it final or integrated into cradle.** Previous-turn file links/attachments are not proof files exist in a future session, and these source/binary files are NOT verified committed to GitHub. Inspect accessible attachments or rebuild/verify if needed.

## Prototype fork / upright / cradle
- [x] At least one fork base printed well on both sides; another fork base planned/attempted, successful total unconfirmed.
- [x] Upright printed but supported underside ugly. **Model flaw:** narrow protruding rail contacts bed while broad panel hovers and requires support. Cannot simply lay broad face flat without modifying CAD. Redesign upright for support-free printing, possibly split rail from panel; preserve servo and pivot dimensions.
- [x] User handled photographed parts and video demonstrated cradle has SINGLE passive peg opposite horn disc, as intended.
- [ ] Complete fork/frame squareness and fit validated.
- [ ] Passive pivot installed/sweep clearance validated.
- [ ] Final horn geometry incorporated into complete laser cradle, screws installed and center servo screw accessible.
- [ ] Laser OFF mounted; slider and rear charging port accessible; clearance and balance confirmed.
- [ ] Powered tilt or pan tested. DO NOT imply full assembly completed.

## Exact next action
Wait for user's **V5 print and fit report**: does it print without spaghetti or warping, does 11 mm x 1 mm center boss recess allow both horn arms to sit FLUSH on otherwise flat disc, do 14.5 mm spaced holes align with chosen physical horn, and is center screw access viable? Ask only for relevant measurements/photos if fit fails. If good, update CAD of COMPLETE cradle with V5 pocket/hole geometry and correct printer orientation; separately redesign rail-balanced upright. Confirm sliced toolpaths and physical testing before assembly/powered claims. Do not buy speculative hardware or repeatedly request supplied SG90 CAD.

## Long-term constraints
Bambu A1, regular PLA, modular quick prints; compact U-fork tilt + SG90 direct-drive pan; removable 16.1 mm laser, never modify laser; SG90 servo supply from separate 5 V rail with shared GND, not controller regulator; XIAO ESP32-C3 ordered with headers, Dupont and lever connectors ordered, 5 V wall supply owned; V1 must leave future battery-module interface without reprinting core. Keep living GitHub docs updated on wrap and distinguish reported fit from CAD assertions.