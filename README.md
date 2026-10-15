# 422A / 422AN OEM Hall sensors: SS41F replacement in a BLDC hub motor

**Documented repair:** Nilox X4 electric bicycle, 36 V / 250 W geared BLDC hub motor, original 36 V / 13 A controller (motor/controller date markings suggest May 2018).

The original curved Hall PCB carried two black sensors marked **422A / 733** and a yellow/gold middle sensor marked **422AN / 726**. No reliable manufacturer datasheet for these exact OEM markings was found during this investigation. This repository documents the physical parts and a **successful real-world replacement**, not an authenticated datasheet.

## The key finding

Replacing all three original sensors with **SS41F** devices facing the same way resulted in buzzing and jerking with the original sensored controller. **Physically reversing only the middle SS41F**, while bending/rerouting its leads so that **VCC, GND and OUT remained connected to the correct PCB nets**, restored normal motor operation.

![Completed working Hall PCB: reversed middle SS41F](images/working-middle-SS41F-reversed.jpg)

## Evidence: original OEM parts

| Original yellow/gold 422AN / 726 | Original black 422A / 733 |
| --- | --- |
| ![Yellow OEM 422AN](images/422AN-yellow-OEM.jpg) | ![Black OEM 422A](images/422A-black-OEM.jpg) |

![Original curved Hall PCB](images/original-hall-PCB.jpg)

## Observations and diagnostic reasoning

- All original sensors appeared to be installed facing the same way, despite the different marking and package colour of the middle part.
- The replacement sensors were sold as SS41F; the package label reads `41F-TO92-Bao` (see photo below). This does not independently verify the characteristics of the supplied parts.
- With three identically oriented replacements, the original controller did not commutate the motor correctly.
- A manually recorded Hall-state sequence, in the measurement's **blue / green / yellow** channel order, was `001 → 011 → 111 → 110 → 100 → 000`.
- Mathematically inverting the **middle (green)** bit produces `011 → 001 → 101 → 100 → 110 → 010`. This provided a clue that the effective polarity of the middle channel might be wrong.
- After reversing the physical orientation of the middle replacement sensor **and maintaining the proper electrical connections**, the motor ran normally with the original controller.
- The motor also showed localized evidence of serious winding overheating and had previously run with a sensorless controller, though PAS behaviour was unstable. These are relevant background observations, not proof of the cause of the Hall mismatch.

**Measurement limitation:** the Hall states were read sequentially with a multimeter, not captured simultaneously with a logic analyser. They should not be treated as a verified commutation timing chart or proof of a universal 60°/120° sensor specification.

## What the experiment does—and does not—prove

**Verified for this unit:** the middle replacement Hall channel needed the reversed physical sensing orientation to work with the original controller.

**Plausible but unverified:** the OEM yellow **422AN** may have an opposite magnetic switching response compared with the black **422A** sensors. Without authenticated datasheets or controlled magnetic-pole tests on the OEM parts, this remains a hypothesis. Do **not** assume that every component bearing these markings has the same pinout, magnetic polarity, latch/switch type or electrical parameters.

## Practical replacement precautions

1. Photograph and record the original sensor **markings, position and orientation** before removing anything.
2. Trace **supply, ground and signal** on the actual PCB. Do not infer pin order from package shape or this report.
3. Test all three channels while slowly turning the motor. Prefer an oscilloscope or logic analyser if available.
4. If three identical replacement sensors cause buzzing or jerking, check the **middle channel's magnetic orientation/polarity** as one possible cause—not only phase and Hall wire permutations.
5. **Do not simply flip the package without correcting its lead connections.** Incorrect VCC/GND/OUT wiring can damage the sensor or controller.
6. Independently check winding, wiring and controller health, especially after overheating.

## Replacement packaging

![SS41F replacement sensor packaging](images/SS41F-replacement-packaging.jpg)

## Illustrated technical report

[Read the two-page PDF report](Nilox_X4_422A_422AN_SS41F_repair_report.pdf).

## Search keywords

`422A` · `422AN` · `422AN 726` · `422A 733` · `yellow Hall sensor` · `OEM Hall sensor` · `SS41F` · `BLDC Hall polarity` · `Nilox X4` · `electric bicycle hub motor` · `e-bike Hall sensor replacement`

---

*This is a case study of one repaired motor, not an official component datasheet or a general guarantee of interchangeability.*
