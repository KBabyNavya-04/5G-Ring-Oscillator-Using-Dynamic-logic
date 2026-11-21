# 5-Stage Ring Oscillator Using Dynamic Logic


![EDA](https://img.shields.io/badge/EDA-Cadence%20Virtuoso%20IC6.1-blue)
![PDK](https://img.shields.io/badge/PDK-GPDK%2045nm-green)
![VDD](https://img.shields.io/badge/VDD-1.0V-orange)
![DRC](https://img.shields.io/badge/Assura%20DRC-Clean-brightgreen)
![LVS](https://img.shields.io/badge/Assura%20LVS-Matched-brightgreen)
![Verification](https://img.shields.io/badge/Verification-In%20Progress-orange)


## 📌 Project Overview

This project focuses on the design and implementation of a **5-Stage Ring Oscillator Using Dynamic CMOS Logic**.

A ring oscillator is a circuit consisting of an odd number of inverter stages connected in a closed loop. It generates a continuous oscillating output without requiring an external periodic input signal.

This project explores dynamic CMOS logic for high-speed VLSI circuit design and its potential applications in next-generation 5G communication systems.

## 🎯 Objectives

- Design a 5-stage ring oscillator using CMOS logic.
- Understand dynamic CMOS logic operation.
- Design and implement the circuit schematic.
- Develop the physical layout of the circuit.
- Study oscillation behavior and frequency characteristics.
- Explore high-speed VLSI circuit design.

## ⚙️ Working Principle

1. Five inverter stages are connected in a closed-loop configuration.
2. Each stage introduces propagation delay.
3. The odd number of inverter stages creates the phase condition required for oscillation.
4. The output continuously switches between HIGH and LOW.
5. The oscillation frequency depends on the number of stages and propagation delay.

## 🧰 Tools and Technologies

- Cadence Virtuoso
- CMOS Technology
- Dynamic CMOS Logic
- VLSI Design
- Schematic Design
- Physical Layout Design

## 🔬 Circuit Design and Implementation

### 1. Five-Stage Ring Oscillator Schematic

The schematic shows five inverter stages connected in a ring configuration to generate an oscillating output signal.

![Five Stage Ring Oscillator Schematic](5stageringgcmosdy.png)

### 2. Five-Stage Ring Oscillator Layout

The physical layout represents the implementation of the five-stage ring oscillator with VDD, GND, input and output connections.

![Five Stage Ring Oscillator Layout](5str_lay.png)

### 3. Dynamic CMOS Circuit Schematic

The dynamic CMOS circuit schematic shows the transistor-level implementation using PMOS and NMOS transistors with clock and input connections.

![Dynamic CMOS Schematic](cmosDy_sche.png)

### 4. Dynamic CMOS Layout

The layout represents the physical implementation of the dynamic CMOS circuit, showing transistor regions, metal interconnections and supply connections.

![Dynamic CMOS Layout](cmosDy_lay.png)

### 5.Simulation Results
![Dynamic CMOS Layout](graph.png)

## Summary of Key Specifications

| Parameter | Value / Characteristic | Notes |
|---|---|---|
| Technology Node | 45nm CMOS (Cadence GPDK045) | Standard Cadence 45nm PDK |
| Nominal Supply Voltage (V<sub>DD</sub>) | **1.0 V** | GPDK045 nominal |
| Minimum Gate Length (L<sub>min</sub>) | 45 nm (0.045 µm) | GPDK045 baseline |
| Number of Stages (N) | **5** | Odd number required for oscillation |
| Oscillation Frequency (f<sub>osc</sub>) | **≈ 6.7 GHz** | Schematic only: ≈ 9–10 GHz |
| Oscillation Period (T) | ≈ 150 ps | T = 2·N·t<sub>pd</sub> |
| Propagation Delay per Stage (t<sub>pd</sub>) | ≈ 15 ps | Post-layout; ≈ 10–11 ps pre-layout |
| t<sub>pLH</sub> / t<sub>pHL</sub> | ≈ 17 ps / 13 ps | PMOS slower unless Wp/Wn is tuned |
| Total Average Power (P<sub>avg</sub>) | ≈ 133 µW | Dynamic + leakage |
| Power-Delay Product (PDP) | ≈ 2.0 fJ | P<sub>avg</sub> × t<sub>pd</sub> |
| Energy-Delay Product (EDP) | ≈ 30 fJ·ps | PDP × t<sub>pd</sub> |
| Duty Cycle | ≈ 48–52 % | Depends on Wp/Wn ratio |
| EDA Toolchain | Cadence Virtuoso / Spectre / Assura | Industry standard custom IC suite |

---

## Timing Performance Breakdown & RC Parameters

All propagation delays and lumped parasitic RC parameters were evaluated at the 50 % supply threshold (V<sub>mid</sub> = 0.5 V at V<sub>DD</sub> = 1.0 V):

| Hierarchy Block | t<sub>PLH</sub> | t<sub>PHL</sub> | t<sub>pd</sub> (Average) | R<sub>eff</sub> | C<sub>load</sub> | Elmore τ (0.69·RC) |
|---|---|---|---|---|---|---|
| CMOS Inverter (single stage, FO1 + wire) | 17 ps | 13 ps | 15 ps | ≈ 5.4 kΩ | ≈ 4 fF | ≈ 15 ps |
| 5-Stage Ring (total loop delay) | 85 ps | 65 ps | 75 ps (half period) | n/a | ≈ 20 fF total | n/a |

---

##  Power, PDP, and EDP Analysis (5-Stage Ring)

- **Total Average Power (P<sub>avg</sub>):** ≈ 133 µW
- **Dynamic Power (P<sub>dynamic</sub>):** ≈ 133 µW (> 99 % of total)

  `P_dynamic = N · C · V_DD² · f = 5 × 4 fF × (1.0 V)² × 6.67 GHz ≈ 133 µW`

  (α = 1, since every node toggles once per cycle in each direction. Short-circuit power is included.)
- **Static Leakage Power (P<sub>static</sub>):** ≈ 0.4 µW (< 1 % of total)

  `P_static = I_leak × V_DD ≈ 0.4 µA × 1.0 V = 0.4 µW`
- **Propagation Delay per Stage (t<sub>pd</sub>):** ≈ 15 ps

**1. Power-Delay Product (PDP)**

```
PDP = P_avg × t_pd = 133 µW × 15 ps ≈ 2.0 fJ
```

**2. Energy-Delay Product (EDP)**

```
EDP = PDP × t_pd = 2.0 fJ × 15 ps ≈ 30 fJ·ps
```

---

## Output Waveform Parameters

A ring oscillator is a free-running loop with no clock or registers, so setup, hold and skew do not apply. The following waveform metrics were extracted from the transient simulation instead:

| Parameter | Approx. Value | Notes |
|---|---|---|
| Rise Time (10–90 %) | ≈ 22 ps | 0.1 V to 0.9 V |
| Fall Time (90–10 %) | ≈ 16 ps | |
| Output Swing | ≈ 0 to 1.0 V | Rail-to-rail |
| Start-up Time | ≈ 0.3–1 ns | Needs initial condition or small kick |
| Period Jitter (RMS) | ≈ 0.3–1 ps | With transient noise enabled |
| Phase Noise @ 1 MHz offset | ≈ −85 to −95 dBc/Hz | PSS / Pnoise |
| Frequency Sensitivity to V<sub>DD</sub> | ≈ 3–5 GHz/V | V<sub>DD</sub> swept 0.8 V to 1.2 V |

---

## Design and Simulation Notes

- **Frequency formula:** `f_osc = 1 / (2 · N · t_pd)`
- **Initialization:** add an initial condition (`ic`) on one node, or a short pulse, so the simulation does not settle at the DC operating point (~0.5 V on every node).
- **Calculator expressions (ADE):** `freq()` or `period()` for frequency, `average(power)` for power, `delay()` with 50 % V<sub>DD</sub> thresholds for t<sub>pLH</sub> / t<sub>pHL</sub>.
- **Corner behavior:** frequency drops ≈ 25–30 % at SS / 125 °C and rises ≈ 25–30 % at FF / −40 °C.
- **Output buffer:** adding one lowers frequency by a few percent and slightly raises power.

## 📂 Project Structure
```text
5G-Ring-Oscillator-Using-Dynamic-logic/
│
├── 5stageringgcmosdy.png
├── 5stageringoscDYcmos.png
├── 5str_lay.png
├── 5str_sch_tb.png
├── 5stringosc.png
├── cmosDy_lay.png
├── cmosDy_sche.png
├── cmosDy_sym.png
├── cmosDynamic.zip
└── README.md
```

## 👩‍💻 Author

**K. Baby Navya**

Electronics and Communication Engineering (ECE)

## ⭐ Conclusion

This project demonstrates the design and implementation of a five-stage ring oscillator using dynamic CMOS logic. The schematic and physical layout provide practical understanding of transistor-level circuit design and VLSI implementation for high-speed applications.

---
If you find this project useful, don't forget to ⭐ the repository!


