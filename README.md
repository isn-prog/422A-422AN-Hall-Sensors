# 422A / 422AN OEM Hall Sensors — BLDC Motor Repair with SS41F

## Verified repair

This case documents a successful repair of a **Nilox X4** electric bicycle's **36 V / 250 W geared BLDC hub motor**. Its original curved Hall-sensor PCB carried two black sensors marked **422A / 733** and one yellow/gold middle sensor marked **422AN / 726**. No reliable datasheet for these exact OEM markings was found during the investigation.

**Key finding:** replacing all three sensors with identically oriented **SS41F** Hall sensors caused buzzing and jerking with the original **36 V / 13 A** controller. **Physically turning over only the middle SS41F**, while rerouting its leads so that VCC, GND and OUT remained correctly connected, **restored normal motor operation**.

## Hardware and symptoms

- Vehicle: Nilox X4 e-bike.
- Motor: 36 V, 250 W geared BLDC hub motor.
- Controller: original 36 V, 13 A unit; controller and motor markings suggest approximately May 2018.
- Original Hall sensors: black **422A (733)** on the outer positions; yellow/gold **422AN (726)** in the middle, all apparently facing the same direction.
- Replacement sensors: **SS41F**, supplied in packaging marked `41F-TO92-Bao`.
- The motor had signs of localized winding overheating. It had previously run with a sensorless controller, although PAS behaviour was unstable.

## Hall signal investigation

A manually observed Hall output sequence (blue / green / yellow channel order) was:

```text
001 → 011 → 111 → 110 → 100 → 000
```

Inverting the **middle (green) channel** mathematically yields:

```text
011 → 001 → 101 → 100 → 110 → 010
```

This pointed toward a different effective magnetic response in the middle channel. The measurements were made sequentially with a multimeter, not captured simultaneously using a logic analyser, so the sequence is a diagnostic observation rather than a full timing characterization.

The middle SS41F was then physically reversed, **with its electrical connections correctly rerouted**. The motor ran normally using the original controller. No electronic inverter circuit was required.

## What this proves — and what it does not

**Confirmed for this motor/controller:** three same-facing SS41F sensors failed to commutate correctly; reversing only the middle sensor, with correct wiring, solved the problem.

**Hypothesis:** the original yellow **422AN** sensor may have had an opposite magnetic switching response compared with the black **422A** devices. The repair strongly supports a middle-channel polarity mismatch, but **does not prove a universal specification for 422AN**. Pinout, latching behaviour, switching polarity and other parameters of components bearing these markings still require independent verification.

## Guidance for similar repairs

1. Photograph original sensor markings, physical orientation and PCB wiring before removal.
2. Determine the actual **VCC, GND and OUT** nets; do not assume pinout from a similar-looking package.
3. Check the three Hall outputs while slowly rotating the wheel. A multichannel logic analyser or oscilloscope is preferable to manual readings.
4. If identical replacement sensors cause buzzing/jerking, investigate magnetic orientation and Hall-channel polarity, in addition to phase/Hall wiring combinations.
5. **Never simply turn a sensor over without checking and rerouting its leads**: supply and signal pins must remain correctly connected.
6. Investigate unrelated winding and controller damage as needed.

## Supporting evidence

Five photographs document the original yellow **422AN / 726**, original curved sensor PCB, black **422A / 733**, SS41F replacement packaging, and completed working installation with the middle SS41F reversed. A two-page illustrated PDF technical report was also prepared. **These images and the PDF are not yet uploaded to this repository.**

## Keywords

`422A` · `422AN` · `422AN 726` · `422A 733` · `yellow Hall sensor` · `OEM Hall sensor` · `SS41F` · `BLDC Hall polarity` · `Nilox X4` · `e-bike hub motor`

---

*This is a documented single-unit repair, not an OEM datasheet or a guarantee of interchangeability.*
