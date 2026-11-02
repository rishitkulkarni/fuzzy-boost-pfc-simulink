# Fuzzy Logic Controlled Boost PFC Converter

MATLAB/Simulink simulation of a single-phase boost power factor correction (PFC) converter. A fuzzy logic controller regulates the DC-link voltage, while an inner current-control loop shapes the AC input current to follow the supply voltage.

## Overview

A diode bridge rectifies the AC supply. The boost stage uses an inductor, MOSFET, diode, and output capacitor to supply the DC load. The outer voltage loop compares the DC-link voltage with a 150 V reference and feeds the error into a single-input fuzzy logic controller. Its output sets the amplitude of an inductor-current reference proportional to the rectified input voltage. The current-control stage uses inductor-current feedback to generate the MOSFET PWM signal.

```text
AC source → Bridge rectifier → Boost converter → DC-link capacitor + load
                  │                  ↑
                  └→ Rectified voltage × fuzzy voltage-loop output
                                       → Current reference → Current controller + PWM
                                                               ↑
                                                    Inductor-current feedback
DC-link voltage → Compare with 150 V → Fuzzy voltage controller ────────┘
```

## Simulink model

![Simulink model of the bridge rectifier, boost converter, and fuzzy control loop](images/simulink-model.png)

*Figure extracted from the project report.* The voltage reference block in this screenshot reads **160 V**, while the report specifications state **150 V**. Check the actual `.slx` model and update the reference and documentation to match before publishing results.

## Model parameters

| Parameter | Value |
| --- | ---: |
| Input voltage | 113.14 V RMS, single phase |
| Input frequency | 50 Hz |
| DC-link voltage reference | 150 V |
| Boost inductance | 22.5 mH |
| Output capacitance | 940 µF |
| Load resistance | 212 Ω |
| Switching frequency | 20 kHz |
| Simulation environment | MATLAB/Simulink |

## Reported results

The project report gives an input-current THD of **70.22% without PFC** and **2.7% with PFC**. It describes the controlled input current as approximately sinusoidal and in phase with the input voltage. The report does not give a numerical measured power factor, so none is claimed here.

## Running the simulation

1. Open the project's Simulink model in a MATLAB installation with its required Simulink components and Fuzzy Logic Toolbox.
2. Check the model parameters against the table above and load any accompanying fuzzy inference system (FIS) file if the model references one.
3. Run the simulation and inspect the DC-link voltage, current reference and inductor current, AC input voltage and current, and steady-state input-current FFT.
4. For a meaningful with/without PFC comparison, use the same source and load conditions and calculate THD over a steady-state interval.

> The attached report documents the simulation, but does not identify a particular `.slx` filename or MATLAB release. Update these steps with the actual model path and version when adding the simulation files to this repository.

## Documentation

See the project report for the circuit diagram, fuzzy controller description, waveforms, and discussion. Add the report under `docs/` and link its actual filename here when publishing the repository.
