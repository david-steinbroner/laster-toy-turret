# Laser Turret — Living Build Tracker

**LATEST SEPTEMBER 17, 2026: READ `SESSION_HANDOFF_2026-09-17.md` FIRST.** User's preferred full V4 inspection assembly is `Turret_V4.3mf` (identical to `Laser_Turret_V4_Observatory.3mf`). Preserve this version as the baseline. User received the tiny `Turret_V4_Minimal_Fit_Kit.3mf` and will return with its print and fit results; NONE REPORTED YET. Original binary files are not confirmed committed to GitHub; user received a portable archive in chat containing models and complete handoff. Older 2026-09-16 handoff and historical PROJECT_STATE checkpoints are superseded for current progress.

## Physically validated
- Removable laser clip nominal ~15.45 mm ID fits actual 16.1 mm laser; laser length 96.5 mm.
- Smallest SG90 body-fit coupon (~22.4 mm nominal) fits.
- Passive pivot selected ~3.35 mm bore with 3.0 mm peg.
- Straight double-sided servo horn selected; earlier initial holes aligned physically. V6 horn disc with **16 mm mounting holes center-to-center WORKS**, per user. Its outer diameter 24 mm, thickness 4 mm, hub-only recess 11 mm diameter x 1 mm depth. NO horn arm grooves. Supersedes V5 14.5 mm holes.
- Original cradle blocks broke on handling due to ~0.5 mm root overlap. Reinforced V4 core CAD broadens connections to ~3 mm and braces, but no report of full loaded durability. Do not imply confirmed strength.

## Current BEST version: V4 mini observatory
- `Turret_V4.3mf` is an inspection assembly, NOT a print-ready plate. Exactly TWO servo references: tilt immediately beside laser, lower pan servo vertical. Upper dome ~120 mm OD mostly contains horizontal 96.5 x 16.1 mm laser, SINGLE front slit, rear closed, nominal screwless 3-lug twist lock. Round base ~84 mm OD x ~46 mm tall. Actual-reference servo/horn STEP models used.
- Base includes *estimated, nonprintable* XIAO ESP32-C3 controller and two lever connectors (+5V and ground), not verified holders: footprints ~21x17x13 and 20x13x12 each. Need physical connector/header/USB/wire clearance, retention, routing, strain relief and future battery interface.
- Outstanding: pan load-bearing support and harness twist/stops, full V4 closed-rear laser tilt sweep, dome tab tolerances/stops and removal, fastening access, assembled servo retention, printability, electronic packaging. Previous V3 sampled +/-25 degree movement DOES NOT establish V4 rear-closed clearance.

## Current next print: miniature fit kit
- `Turret_V4_Minimal_Fit_Kit.3mf`: FIVE selectable objects: XIAO footprint gauge, one lever footprint gauge for either identical bay, ring-lock curved sector, matching skirt/tab curved sector, and 16mm-spacing pan hole gauge. Six standalone STL filenames existed because 5V/GND gauges were duplicated. Read `Turret_V4_Minimal_Fit_Kit_READ_ME.txt` in portable archive.
- Footprint guides only check XY, with 0.35 mm per-side clearance, NOT USB/header/lever-open/wire clearance or secure mounting.
- Dome-sector ring coupon corrects observed **0.2 mm nominal deck/dome interference** by trimming backing rib to radius 57.2 mm; propagate to full V4 CAD AFTER test. Curved sectors alone cannot prove full dome latch or stops.
- Pan coupon tests hole pattern: 26mm disc, two 2.3mm nominal holes spaced 16mm centers, 3.4mm center opening. Does NOT establish spline drive, screw length, servo thrust or wobble.
- User will print/test kit and report next session. Recommended regular PLA on Bambu A1, 0.20mm layers, 3 walls, supports off if sliced preview permits; brim narrow dome sectors as needed.

## Next action after user's report
1. Record outcome of each gauge, including unprinted pieces. Request photo or measurements only to diagnose a failed fit. Do not invent results.
2. Fix only affected dimensions; propagate 0.2mm lock correction when confirmed. Measure real electronics incl. header height, opened levers, USB plug and wire bends.
3. Check mechanism and closed-rear laser sweep, safe pan wire routing and load path, full dome twist-lock/collision/laser-removal access.
4. Produce **V4.1** as NEW print-ready individual STLs and separate-object printable 3MF excluding nonprintable hardware; preserve V4 inspection baseline. Inspect Bambu sliced toolpaths/material and print only after validation.

## Locked broader requirements
Compact mini-observatory rather than gun/barrel look; only one forward dome opening; screwless easy-removal top and removable laser, robust clip and structural roots; two SG90s; XIAO ESP32-C3 with headers and Dupont/lever connectors, 5V wall adapter external, servos from separate 5V power distribution with shared ground (not controller regulator). Future battery interface without reprinting core. No permanent laser modification. Keep models modular, small and editable.
