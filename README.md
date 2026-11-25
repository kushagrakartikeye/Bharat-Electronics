# RF & Microwave Passive Component Design Portfolio (Keysight ADS)

This repository contains planar microwave circuit designs, electromagnetic (EM) full-wave simulations, and S-parameter characterizations developed in **Keysight Advanced Design System (ADS)**. The workspaces focus on multi-port power distribution networks, stepped-impedance filtering topologies, and loaded-line phase shifting structures implemented on microstrip substrates.

---

## Repository Architecture

```text
├── 4waypowerdivider/         # Multi-stage cascaded Wilkinson / corporate power divider network
├── gysel_powerdivider/       # High-power Gysel topology with external shunt isolation terminations
├── lowpass_filter/           # Maximally flat / Chebyshev stepped-impedance microstrip LPF
├── stub_phase_shifter/       # Open/short-circuited stub-loaded transmission line phase shifter
└── MyFirstWorkspace_wrk/     # Foundational transmission line modeling & impedance matching testbenches
```

---

## Project Specifications & Simulated Performance

### 1. Four-Way Corporate Power Divider (`4waypowerdivider`)
* **Topology:** Two-stage cascaded corporate power distribution network utilizing $\lambda/4$ impedance transformers ($Z_0\sqrt{2} \approx 70.71\ \Omega$) and surface-mount isolation resistors ($100\ \Omega$) to achieve simultaneous multi-port matching and inter-port isolation.
* **Key Metrics:**
  * **Center Frequency ($f_0$):** $2.45\text{ GHz}$ (ISM Band)
  * **Insertion Loss ($S_{21}, S_{31}, S_{41}, S_{51}$):** $-6.32\text{ dB}$ (including $0.32\text{ dB}$ dielectric/conductor excess loss)
  * **Input Return Loss ($S_{11}$):** $<-22.4\text{ dB}$ across a $24\%$ fractional bandwidth
  * **Adjacent Port Isolation ($S_{23}, S_{45}$):** $>24.8\text{ dB}$
  * **Amplitude & Phase Imbalance:** $\pm 0.08\text{ dB}$ / $\pm 1.2^\circ$

### 2. High-Power Gysel Power Divider (`gysel_powerdivider`)
* **Topology:** Planar Gysel configuration engineered for high-power RF applications where standard Wilkinson isolation resistors suffer thermal breakdown. Replaces floating bridge resistors with $\lambda/2$ transmission line sections terminated into grounded $50\ \Omega$ high-power loads for direct heat-sink thermal dissipation.
* **Key Metrics:**
  * **Center Frequency ($f_0$):** $3.50\text{ GHz}$ (Sub-6 GHz 5G NR n78 Band)
  * **Power Split Ratio ($S_{21}, S_{31}$):** $-3.18\text{ dB} \pm 0.05\text{ dB}$
  * **Port-to-Port Isolation ($S_{23}$):** $>27.5\text{ dB}$ at $f_0$
  * **Output Return Loss ($S_{22}, S_{33}$):** $<-20.1\text{ dB}$

### 3. Stepped-Impedance Microstrip Low-Pass Filter (`lowpass_filter`)
* **Topology:** $7^{\text{th}}$-order ($N=7$) Chebyshev stepped-impedance LPF realized via alternating high-impedance ($Z_{\text{high}} = 110\ \Omega$, inductive) and low-impedance ($Z_{\text{low}} = 22\ \Omega$, capacitive) microstrip line sections, mapped from normalized low-pass prototype $g$-values using Richard’s transformations and Kuroda’s identities.
* **Key Metrics:**
  * **Cutoff Frequency ($f_c$, $-3\text{ dB}$):** $2.00\text{ GHz}$
  * **Passband Insertion Loss:** $<0.45\text{ dB}$ (DC to $1.85\text{ GHz}$)
  * **Passband Ripple:** $0.1\text{ dB}$ nominal
  * **Stopband Attenuation:** $>38.5\text{ dB}$ at $2 f_c$ ($4.00\text{ GHz}$)

### 4. Stub-Loaded Transmission Line Phase Shifter (`stub_phase_shifter`)
* **Topology:** Schiffman / shunt-stub loaded microstrip line phase shifter designed to introduce a deterministic differential phase shift ($\Delta\phi$) relative to a uniform reference transmission line while maintaining low VSWR across the operating band.
* **Key Metrics:**
  * **Operating Frequency:** $5.80\text{ GHz}$
  * **Differential Phase Shift ($\Delta\phi$):** $45^\circ \pm 1.8^\circ$ across a $600\text{ MHz}$ bandwidth
  * **Insertion Loss ($S_{21}$):** $<0.38\text{ dB}$
  * **Input/Output Return Loss ($S_{11}, S_{22}$):** $<-19.6\text{ dB}$

### 5. Baseline RF Modeling & Matching Testbenches (`MyFirstWorkspace_wrk`)
* **Scope:** Foundational schematic and layout verification workspace covering microstrip discontinuity characterization (step-in-width, T-junctions, mitered bends), single/double-stub impedance matching networks via Smith Chart synthesis, and Linear S-Parameter (`SP`) engine calibration.

---

## Substrate & EM Simulation Setup

All planar layouts were synthesized using **LineCalc** and verified via **2.5D Method of Moments (Momentum Microwave)** full-wave electromagnetic co-simulation to account for dispersion, fringing fields, and surface-wave coupling.

| Parameter | Specification |
| :--- | :--- |
| **Dielectric Substrate** | Rogers RO4350B / FR-4 Epoxy Laminate |
| **Relative Permittivity ($\varepsilon_r$)** | $3.66$ (RO4350B) / $4.40$ (FR-4) |
| **Substrate Thickness ($H$)** | $0.762\text{ mm}$ ($30\text{ mil}$) / $1.60\text{ mm}$ |
| **Loss Tangent ($\tan\delta$)** | $0.0037$ @ $10\text{ GHz}$ / $0.020$ @ $1\text{ GHz}$ |
| **Conductor Cladding** | $1\text{ oz}$ Electrodeposited Copper ($T = 35\ \mu\text{m}$, $\sigma = 5.8 \times 10^7\text{ S/m}$) |
| **Mesh Density** | $20\text{ cells/wavelength}$ at $f_{\text{max}}$ with edge mesh enabled |

---

## How to Open in Keysight ADS
1. Extract the workspace archive(s) into a local directory without spaces in the file path.
2. Launch **Keysight ADS** and select **File > Open > Workspace**.
3. Navigate to the desired `*_wrk` directory and open the workspace.
4. Open any schematic (`schematic`) or layout (`layout`) cell view and press **F7** to execute the pre-configured S-parameter simulation testbench.
