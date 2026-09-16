# Laser Turret — Living Build Tracker

**Last updated: September 16, 2026, 01:51 Austin time. Current status: quick tilt prototype PRINTING, NOT yet confirmed finished or assembled.**

**START NEXT CHAT HERE:** [Precise next-session handoff](SESSION_HANDOFF_2026-09-16.md). For full requirements read [PROJECT_STATE.md](PROJECT_STATE.md), but its earlier coupon-pending status is outdated; this tracker and handoff supersede that section. On future user-confirmed progress, update this tracker and the handoff, not just the chat.

## Calibration / components
- [x] Laser clip physically tested, nominal 15.45 mm ID fits 16.1 mm laser body.
- [x] Smallest servo fit coupon ~22.4 mm nominal fits SG90.
- [x] Passive pivot fit coupon printed/tested: second largest is nominal 3.35 mm hole paired with nominal 3.0 mm peg.
- [x] SG90 STEP, SolidWorks parts and assembly, image of double-arm horn supplied; user owns all horns. **Do not ask them to re-supply or remeasure these without first inspecting CAD.**
- [ ] Horn mounting geometry and printed cradle connection physically verified.

## Four-piece quick tilt prototype (v0.1)
- [ ] `01_fork_base.stl` print success confirmed. **PRINTING** as last reported.
- [ ] `02_passive_upright.stl` print success confirmed. **PRINTING** as last reported.
- [ ] `03_servo_upright.stl` print success confirmed. **PRINTING** as last reported.
- [ ] `04_laser_cradle_horn_TEST_FIT.stl` print success confirmed. **PRINTING** as last reported; horn interface is only a test fit.
- [ ] Remove from cooled plate, inspect and identify 4 parts.
- [ ] Fit both upright supports into slots in fork base; check alignment/snugness with no glue.
- [ ] Install cradle between supports; 3 mm passive peg rotates in 3.35 mm hole without binding/wobble.
- [ ] Mount SG90 and physically validate horn-to-cradle attachment and fastening.
- [ ] Insert laser OFF; verify switch access, rear charging port access, tilting clearance and balance.
- [ ] Revise any imperfect print geometry, then conduct powered tilt test and build pan stage.

Bambu Studio initially flagged overlapping first-layer paths between 03 and 04; user was advised to Arrange/re-slice and then reported print started. No verified end result or 1-hour print-time measurement. Existing ZIP `laser_turret_quick_tilt_test_v01.zip` was previously delivered in chat but **NOT confirmed stored in GitHub**; don't invent cross-session sandbox links.

## Simple assembly visual (schematic, not exact geometry)
```text
        [user's removable laser — OFF for fit tests]
                          |
               [04 LASER CRADLE]
                 /             \
         horn mount            passive 3 mm peg
              |                       |
      [03 SERVO UPRIGHT]       [02 PASSIVE UPRIGHT]
          + SG90                3.35 mm hole
              |                       |
              +---- [01 FORK BASE] ---+
                          |
                 PAN STAGE (later)
                          |
              ELECTRONICS BASE (later)
```

An earlier generated infographic in the conversation **incorrectly labeled the four print parts complete**. The authoritative status is printing. Its graphics are illustrative, not a verified dimensional assembly drawing. This markdown schematic is the durable visual.

## Exact next-chat handoff
User plans to identify printed parts and assemble frame before returning. First confirm **whether** that happened, then inspect frame fit and alignment; next guide insertion of cradle and passive peg, then off-power SG90 horn alignment, then laser-off clearances. One step at a time, no unjustified claim of ready-to-power status. See [handoff](SESSION_HANDOFF_2026-09-16.md) for details.

## Existing hardware and constraints
Four SG90 servos, pointer, wall supply, PLA, assorted screws owned. XIAO ESP32-C3 with pre-soldered headers, Dupont wires, lever connectors ordered but not confirmed arrived. Bambu A1 regular PLA; modular fast prints; removable/unmodified laser; separate servo 5 V power distribution and common ground; future battery upgrade without reprinting core turret.