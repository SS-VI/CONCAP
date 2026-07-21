<div align="center">

# Project Highlights

**CONCAP** · Control de Captación

<sub><a href="../README.md">← Back to README</a> · <a href="Architecture.md">Architecture</a> · <a href="SystemOverview.md">System Overview</a> · <a href="Installation.md">Installation</a> · <a href="UserGuide.md">User Guide</a></sub>

</div>

---

> This document is written for **technical evaluators** — recruiters, hiring engineers, and prospective clients — who want to understand the engineering depth behind CONCAP without reading the full documentation set.

<br/>

---

## The one-paragraph version

CONCAP is a solar-powered, two-node industrial IoT system that monitors water turbidity at a rural aqueduct intake and autonomously diverts flow away from the community network when the source becomes contaminated. It spans the full stack — analog sensor conditioning, embedded firmware, RF communications, motor control, cloud telemetry, and a cross-platform mobile application — and it is **deployed and operating in the field**, not a prototype on a bench.

<br/>

---

## Engineering decisions worth discussing

These are the points where the design could have gone another way, and the reasoning that settled it.

### 1. Splitting sensing from actuation

**The problem.** The turbidity signal is a microvolt-level analog measurement. The valve actuators are DC gear motors drawing high inrush current through H-bridges. Putting both on one board means the measurement chain lives next to a switching load several orders of magnitude larger.

**The conventional approach** is careful PCB partitioning: separate ground planes, star grounding, filtering, shielding, timing the ADC conversions to avoid motor switching windows.

**The decision** was to eliminate the coupling structurally rather than mitigate it — two physically separate nodes with independent power and no shared conductor. The only link between them is a radio.

**The trade-off** is a second enclosure, a second MCU, a second power feed, and a radio link that must be reliable. That cost buys a measurement chain that cannot be corrupted by actuation, and a sensing node with no control authority — meaning a sensing fault can never cause unintended valve movement.

<br/>

### 2. ESP-NOW instead of Wi-Fi, LoRa, or wire

| Option | Why it was rejected |
|:---|:---|
| **Wi-Fi AP at the intake** | Maintaining an access point would have dominated a solar-constrained power budget. |
| **LoRa** | Excellent range, but unnecessary at this distance and with higher latency than the control loop wanted. |
| **Wired RS-485** | Requires trenching and protecting a cable between two outdoor points — and reintroduces a conductor between the two domains we just separated. |
| **ESP-NOW** ✅ | Connectionless, low power, low latency, no infrastructure, and native to the ESP32-S3 already in the design. |

The wired option is the interesting rejection: it was ruled out not on cost but because it would have undone the isolation that motivated the two-node split in the first place.

<br/>

### 3. Keeping the control decision local

The decision to divert is taken on Node 2, from data received directly from Node 1. The broker, the internet, and the mobile application are **not in the control path**.

This is the difference between an IoT product and a control system. Putting the decision in the cloud would have simplified the firmware and made the logic easier to update — at the cost of introducing an internet outage as a failure mode with physical, water-safety consequences.

Cloud connectivity in CONCAP is a **supervision channel**. Losing it costs visibility, never protection.

<br/>

### 4. Hysteresis instead of a bare threshold

A naive implementation compares turbidity to a setpoint and actuates. In the field, a signal hovering near that setpoint produces continuous valve cycling — mechanically destructive to the gearboxes, and an alarm flood that trains the operator to ignore notifications.

The implemented policy uses a hysteresis band with a dwell requirement. This is unglamorous and it is what makes the system usable over months rather than days.

<br/>

### 5. Designing the sensing layer to be extended

Turbidity is the control variable, but the acquisition layer was built channel-agnostic. Node 1 transmits engineering units, not raw counts, so Node 2 never needs to know how a sensor is characterized.

The consequence: pH, conductivity, flow, level, rainfall, or water temperature can be added as [expansion channels](../README.md#sensor-expansion) using standard commercial modules, without modifying the transport layer, the control logic, or the telemetry contract.

<br/>

### 6. Fail-safe as a first-class requirement

Every fault mode has a defined outcome, enumerated in [Architecture §7](Architecture.md#7-fail-safe-philosophy). The governing rule:

> **Absence of evidence that water is safe is treated as evidence that it is not.**

When the radio link drops, Node 2 does not assume the water is clean because no alarm arrived. When the probe stops responding, the system holds its last safe configuration and alarms rather than continuing on stale data. This inverts the convenient default and is the correct posture for a system whose failure mode affects a community's drinking water.

<br/>

---

## Breadth of the stack

A single engineer carried this from problem statement to operating installation.

| Domain | Work performed |
|:---|:---|
| **Analog electronics** | Sensor interfacing, precision front-end design, noise management, 24-bit acquisition. |
| **Power electronics** | H-bridge motor drive, current limiting, stall protection, transient suppression. |
| **Energy systems** | Solar sizing, battery bank specification, load budgeting, low-power scheduling. |
| **Embedded firmware** | Dual-node architecture, layered design, state machines, fault arbitration. |
| **RF communications** | ESP-NOW peer management, retry and link-loss handling, in-situ margin verification. |
| **Network & cloud** | Wi-Fi provisioning, MQTT session lifecycle, reconnection back-off, QoS and retained state. |
| **Mobile development** | Cross-platform Flutter application with real-time data, push alarms, and remote configuration. |
| **Mechanical** | Valve coupling, enclosure selection, IP66 sealing, cable glanding, outdoor mounting. |
| **Field engineering** | Site assessment, installation, on-site calibration, validation testing, operator training. |
| **Technical writing** | Architecture documentation, operator guide, commissioning procedure. |

<br/>

---

## What "deployed" means here

This distinction matters when evaluating embedded projects, because most portfolio systems stop at the bench.

| Bench prototype | CONCAP |
|:---|:---|
| Works under controlled conditions | Operates through rain, heat, and seasonal change |
| Powered from a lab supply | Runs on a solar energy budget it must not exceed |
| Reset by hand when it hangs | Must recover unattended, or a community loses water |
| Faults are debugging opportunities | Faults have defined safe outcomes, specified in advance |
| Used by its designer | Used by an operator who did not build it |
| Success is a working demo | Success is months of uneventful operation |

The last row is the real measure. A system like this succeeds by being boring.

<br/>

---

## Context: why this problem is worth solving

Rural community aqueducts serve populations that fall outside municipal utility coverage. They are typically administered by the community itself, operate with minimal budget, and have no instrumentation whatsoever.

The turbidity problem is well understood and the mitigation is simple — close the intake when the source is dirty. What is missing is not knowledge but **presence**: someone at a remote intake, at night, during a storm, within minutes of the event.

CONCAP substitutes an instrument for that presence. The engineering value is not novelty; it is delivering industrial-grade reliability under rural constraints — no grid, no network, no on-site technician, and no budget for either.

<br/>

---

## Discussion topics

If you are evaluating this work, these are the areas with the most substance behind them:

- Noise management strategy in the analog acquisition chain
- Trade-off analysis behind the ESP-NOW field link and its in-situ margin verification
- Solar energy budget derivation and duty-cycle scheduling
- Fail-safe state enumeration and arbitration between automatic and manual control
- Site-specific calibration methodology and why thresholds are not transferable between intakes
- Telemetry contract design that allowed the sensing set to remain extensible

> [!NOTE]
> Implementation specifics — code, schematics, calibration models — remain proprietary per the [LICENSE](../LICENSE). The reasoning, trade-offs, and results are open for discussion in a technical conversation.

<br/>

---

<div align="center">

<sub><a href="../README.md">← Back to README</a> · <a href="../README.md#-contact">Get in touch</a></sub>

<sub><b>CONCAP</b> — <i>Control de Captación</i> · Proprietary. All rights reserved.</sub>

</div>
