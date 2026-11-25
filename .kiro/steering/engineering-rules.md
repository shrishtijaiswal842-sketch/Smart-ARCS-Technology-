# Kiro Steering Rules: A.R.C.S. Technologies Engineering, Safety & Simulation Standards

## 1. Scientific & Regulatory Integrity Guardrails
- **Strict Demonstration Disclosure:** Every UI screen, README, and generated output MUST preserve the `DEMONSTRATION MODE` notice confirming that displayed sensor telemetry, yields, and financial projections are simulated engineering models—not independently certified physical plant measurements.
- **No Uncertified Claims in Code/UI:** Never label simulated oxygen output as "medical-grade" or claim "100% zero emissions" in UI labels without third-party NABL/PESO/CPCB certification flags.

## 2. Equipment-Specific Thermodynamic & Sensor Envelopes
When generating or updating telemetry simulation logic, enforce these exact engineering thresholds from the A.R.C.S. Master Blueprint:
- **Quartz Pyrolysis Core (`R201`):** Nominal cracking zone `500 °C` (simulated stress test ceiling up to `750 °C`; fused-silica material limit `1,200 °C`).
- **System Operating Pressure:** `1.01 bar – 1.25 bar` in pyrolysis/condensation loop (`1.08 bar` nominal); `350 bar` isolated strictly to **Vessel B** (`Type IV` carbon-fibre `H₂` cylinders).
- **Mid-IR QCL & LIBS Chlorine Interlock (`I301`):**
  - Baseline `Gas Index` (`3.46 µm` HCl proxy): `0.05 – 0.22` → `AI STATUS: NORMAL`.
  - Spike condition (`>0.05%` HCl rise within `2 ms` window / `Gas Index >= 0.25`) → Trigger immediate local Edge-FPGA reflux pump override on Scrubber `I301` and divert excess `CO₂` (`4.26 µm`) to **Vessel C** (`Hastelloy C-276` mineralisation chamber).
- **Bio-Oil Buffer (`Vessel A`):** Maintain `65 °C` heating blanket threshold; trigger pneumatic discharge valve at `85%` Guided-Wave Radar (`1–2 GHz`) level.
- **Algae PBR (`PBR401`):** Monitor `680 nm / 720 nm` optical density ratio; throttle `CO₂` sparger (`D401`) flow if cell density drops below active uptake threshold.

## 3. Software Architecture & Hardware-Transition Standards
- **Edge-First Decoupling:** Keep the telemetry simulation engine modular so simulated JSON payloads can be replaced seamlessly in Phase 2 by live `ESP32` / `Modbus TCP` / `MQTT` streams from physical thermocouples, pH probes, and gas sensors without altering UI components.
- **Zero-Build-Fragility Frontend:** Maintain clean, high-contrast industrial SCADA/HMI styling with zero heavy framework bloat so the Digital Twin loads instantaneously on low-bandwidth coastal field connections.
