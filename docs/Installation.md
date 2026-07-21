<div align="center">

# Installation & Commissioning

**CONCAP** · Control de Captación

<sub><a href="../README.md">← Back to README</a> · <a href="Architecture.md">Architecture</a> · <a href="SystemOverview.md">System Overview</a> · <a href="UserGuide.md">User Guide</a> · <a href="ProjectHighlights.md">Project Highlights</a></sub>

</div>

---

> [!IMPORTANT]
> **This is not a build guide.**
> CONCAP is a proprietary, professionally installed system. This document describes the **deployment process and site requirements** so that a prospective client or evaluator understands what an installation involves. It does not contain firmware, schematics, wiring detail, or assembly instructions, and it does not enable self-installation.
>
> Installation is performed by the engineering team. Contact details are in the [README](../README.md#-contact).

<br/>

---

## 1. Site assessment

No installation proceeds before the site is characterized. The assessment establishes whether CONCAP is the right solution and what configuration the site requires.

| Assessment area | What is evaluated |
|:---|:---|
| **Hydraulic layout** | Intake geometry, existing valve arrangement, available bypass path, pipe diameters and materials. |
| **Water behavior** | Baseline turbidity, magnitude and duration of rainfall-driven excursions, seasonal patterns. |
| **Solar viability** | Daily irradiance, shading from canopy or terrain, panel orientation and mounting options. |
| **Radio path** | Distance and obstructions between the sensing point and the control cabinet location. |
| **Connectivity** | Cellular or network coverage at the control cabinet for the MQTT uplink. |
| **Physical access** | Route for equipment, maintenance access, and security of the installation. |
| **Operator context** | Who will supervise the system, their availability, and their technical familiarity. |

> [!NOTE]
> The radio path assessment frequently determines cabinet placement. The ESP-NOW link removes the need for infrastructure, but it does not remove the need for a viable path between the two nodes.

<br/>

---

## 2. Deployment phases

```mermaid
flowchart LR
    P1["1 · Site<br/>assessment"] --> P2["2 · Configuration<br/>& provisioning"]
    P2 --> P3["3 · Mechanical<br/>installation"]
    P3 --> P4["4 · Electrical<br/>& energy"]
    P4 --> P5["5 · Link &<br/>connectivity"]
    P5 --> P6["6 · Calibration<br/>& tuning"]
    P6 --> P7["7 · Validation<br/>testing"]
    P7 --> P8["8 · Operator<br/>handover"]
    P8 --> P9["9 · Monitored<br/>operation"]

    classDef pre fill:#161b22,stroke:#484f58,color:#e6edf3
    classDef field fill:#0b2a45,stroke:#0A66C2,stroke-width:2px,color:#e6edf3
    classDef val fill:#2d1b0d,stroke:#F2A900,stroke-width:2px,color:#e6edf3
    classDef done fill:#0d2818,stroke:#2ea44f,stroke-width:2px,color:#e6edf3

    class P1,P2 pre
    class P3,P4,P5 field
    class P6,P7 val
    class P8,P9 done
```

<br/>

### Phase 1 — Site assessment
Characterization as described above. Produces the site configuration specification.

### Phase 2 — Configuration & provisioning
Nodes are configured, provisioned, and bench-verified **before** leaving the workshop. Devices arrive at the site already paired and ready. Field time is expensive and weather-dependent; nothing that can be done indoors is left for the intake.

### Phase 3 — Mechanical installation
- Sensing unit mounted at the water contact point with the probe correctly submerged and oriented.
- Motorized valve assemblies coupled to V1 and V2 at the junction.
- IP66 enclosures mounted, sealed, and glanded.
- Solar array mounted and oriented per the assessment.

### Phase 4 — Electrical & energy
- Battery bank and charge regulation installed and verified.
- Load budget confirmed against measured consumption.
- Transient and surge protection fitted on all field wiring.
- Grounding and bonding established.

### Phase 5 — Link & connectivity
- ESP-NOW peer link verified in situ with margin measurement, not just a pass/fail.
- Wi-Fi uplink and MQTT session established.
- Presence and telemetry confirmed end to end on the mobile application.

### Phase 6 — Calibration & tuning
- Turbidity channel calibrated against the site's actual water using reference measurements.
- Operating threshold set from the site's baseline and excursion behavior.
- Hysteresis band and dwell time tuned to the source's response characteristics.

> Calibration is site-specific. A threshold that works at one intake is not transferable to another; source geology and catchment behavior differ.

### Phase 7 — Validation testing
| Test | Purpose |
|:---|:---|
| **Induced turbidity event** | Confirm the full detection → diversion → alarm chain under controlled conditions. |
| **Recovery** | Confirm return to normal service when levels are restored. |
| **Link-loss** | Confirm local control continues with the broker unreachable. |
| **Power-loss** | Confirm safe state on shutdown and correct valve referencing on restart. |
| **Stall protection** | Confirm the drive cuts and latches on an obstructed valve. |
| **Solar autonomy** | Confirm the energy budget across a full day/night cycle. |

### Phase 8 — Operator handover
Training on the mobile application, alarm interpretation, manual override, and the maintenance schedule. Written handover documentation is provided.

### Phase 9 — Monitored operation
An initial period under close remote monitoring, with threshold refinement as real seasonal behavior is observed.

<br/>

---

## 3. Site prerequisites

What the client must have in place before installation begins.

| Prerequisite | Requirement |
|:---|:---|
| **Bypass path** | A hydraulic route to divert flow away from the aqueduct — typically returning to the watercourse. |
| **Valve junction** | A point where V1 and V2 can be fitted to separate the aqueduct and bypass paths. |
| **Solar exposure** | An unshaded mounting location with adequate daily irradiance. |
| **Radio path** | A viable path between the sensing point and the cabinet location. |
| **Network coverage** | Cellular or network service at the cabinet for remote supervision. |
| **Access** | Maintenance access to both nodes and the solar array. |
| **Designated operator** | An identified person responsible for responding to alarms. |
| **Permissions** | Authorization from the aqueduct administration for works on the intake structure. |

<br/>

---

## 4. Maintenance

| Interval | Activity |
|:---|:---|
| **Continuous** | Automatic remote health monitoring — link status, battery state, node presence. |
| **Monthly** | Review alarm history and telemetry trends remotely. No site visit required. |
| **Quarterly** | Physical inspection: probe cleaning, valve operation, enclosure seal integrity, solar panel cleaning. |
| **Annual** | Calibration verification against reference measurements, battery capacity assessment, full functional validation. |
| **Post-event** | Inspection after severe weather, flooding, or any latched fault alarm. |

> [!WARNING]
> The turbidity probe is an optical instrument. **Biofilm and sediment accumulation on the optical path degrade readings over time** and will eventually cause the system to under-report turbidity. Quarterly cleaning is not optional — it is the single most important maintenance task, because a fouled probe fails toward "water looks clean."

<br/>

---

## 5. What is not covered here

Consistent with the [LICENSE](../LICENSE), this document deliberately omits:

- Firmware flashing, build configuration, and provisioning procedures
- Wiring diagrams, terminal assignments, and connector pinouts
- Component values, part selection rationale, and sourcing
- Calibration equations, coefficients, and characterization procedure
- MQTT broker configuration, topic structure, and credentials
- Mechanical drawings and mounting hardware specification

These form the proprietary engineering package and are provided only under a commercial agreement.

<br/>

---

<div align="center">

<sub><a href="../README.md">← Back to README</a></sub>

<sub><b>CONCAP</b> — <i>Control de Captación</i> · Proprietary. All rights reserved.</sub>

</div>
