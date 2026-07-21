<div align="center">

# Changelog

**CONCAP** · Control de Captación

</div>

---

All notable changes to the CONCAP system and to this documentation repository are recorded here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

> [!NOTE]
> Version numbers refer to the **system release**, not to the documentation. Entries marked *(docs)* affect only this repository.

<br/>

---

## [Unreleased]

### Planned

- Commissioning of expansion sensor channels on a live site.
- Over-the-air firmware update pipeline for field nodes.
- Historical time-series storage with analytics and reporting.
- Web supervision console complementing the mobile application.
- Multi-intake fleet management.

<br/>

---

## [1.0.0] — 2026

Initial field-deployed release. The system entered continuous operation at a rural community aqueduct.

### Added

- **Two-node distributed architecture** separating sensing from actuation, isolating the high-current motor stage from the precision analog measurement chain.
- **Turbidity acquisition subsystem** — optical probe coupled to a 24-bit delta-sigma analog front-end with programmable gain.
- **Autonomous diversion control** — hysteretic policy driving the V1 / V2 valve pair between normal service and diversion states.
- **ESP-NOW field link** — connectionless peer-to-peer radio between the sensing and control nodes, removing the need for Wi-Fi infrastructure at the intake.
- **MQTT telemetry pipeline** — live measurement publishing, retained state topics, and alarm event emission.
- **Flutter mobile application** — live dashboard, valve status, alarm log, remote threshold configuration, manual override, and system health indicators.
- **Solar power subsystem** — panel array, battery bank, and charge regulation sized for unattended off-grid operation.
- **IP66 outdoor enclosure** — sealed housing with cable glanding and transient protection on all field wiring.
- **Fail-safe behavior** — defined safe states on power loss, radio link loss, and sensor fault.

### Deployed

- Installation, sealing, and commissioning completed at the intake site.
- Solar subsystem startup and load budget validation under field conditions.

<br/>

---

## Documentation history

### [docs-1.1.0] — 2026-07-21

#### Changed

- Removed ambient temperature and humidity from the described deployed configuration. The DHT22 was withdrawn from the hardware table, the architecture diagram, and the communication sequence diagram.
- Reframed the feature previously listed as *Environmental Telemetry* into **Expandable Sensing Architecture**, describing the acquisition layer as channel-agnostic rather than tied to a fixed sensor set.
- Updated the mobile application description so the live dashboard no longer advertises temperature and humidity channels.

#### Added

- **Sensor Expansion** section documenting eight parameters integrable through standard commercial modules — ambient temperature and humidity, water temperature, pH, conductivity / TDS, flow rate, water level, rainfall, and barometric pressure — with their interfaces and the operational value each provides.
- Explicit note clarifying that the expansion table documents *integration capability*, not the currently deployed configuration.
- Repository governance files: `LICENSE`, `CONTRIBUTING.md`, `SECURITY.md`, `CHANGELOG.md`, `.gitignore`.
- Extended documentation set under `docs/` — architecture, system overview, installation, user guide, and project highlights.
- Asset placeholder structure under `images/`, `videos/`, and `assets/`.

### [docs-1.0.0] — 2026-07-21

#### Added

- Initial `README.md` establishing the repository as a proprietary technical showcase.
- System architecture, control strategy, and communication flow diagrams.
- Hardware and software overview at subsystem level of abstraction.
- Intellectual property notice enumerating explicitly excluded material.

<br/>

---

<div align="center">

<sub><b>CONCAP</b> — <i>Control de Captación</i></sub>

<sub>Security researchers who report findings under <a href="SECURITY.md">SECURITY.md</a> are credited in this file unless they prefer anonymity.</sub>

</div>
