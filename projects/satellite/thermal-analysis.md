---
layout: page
title: Thermal Balance and Radiator Cooling Capacity
permalink: /projects/satellite/thermal-analysis/
---

# Thermal Balance and Radiator Cooling Capacity

## Overview

This study estimates the net radiative cooling capacity of a spacecraft radiator using the geometric coupling factors obtained from the [three-dimensional radiative-coupling analysis]({{ '/projects/satellite/radiative-coupling/' | relative_url }}).

The calculation combines the radiator's thermal emission with estimated incoming infrared radiation from the Earth and nearby spacecraft surfaces. It is a **preliminary steady-state radiative heat budget**, not a transient thermal model or a prediction of detector temperature.

## Radiative coupling inputs

The three-dimensional ray-tracing and orbital analysis gives an Earth coupling factor that varies with orbital phase and spacecraft attitude. Among six representative seasonal/attitude cases, the largest **orbit-averaged** Earth coupling factor is **0.026**. This is not the maximum instantaneous coupling factor.

An internal spacecraft coupling factor of **0.014** is adopted from the absorption fraction in the modeled ray-tracing distribution.

For the calculation methods and directional results, see [Radiative Coupling]({{ '/projects/satellite/radiative-coupling/' | relative_url }}).

## Thermal assumptions

| Parameter | Assumed value | Notes |
| --- | ---: | --- |
| Radiator area, \(S\) | 0.148 m² | Geometric radiator area |
| Radiator emissivity, \(\varepsilon\) | 0.8 | Also used as effective infrared absorptivity |
| Radiator temperatures | 190 K and 172 K | Two operating cases |
| Effective Earth temperature | 270 K | Approximate blackbody equivalent of 300 W/m² |
| Earth coupling, \(F_{\mathrm{Earth}}\) | 0.026 | Largest orbit-averaged value among six cases |
| Internal coupling, \(F_{\mathrm{internal}}\) | 0.014 | Based on modeled absorption |
| Effective internal surface temperature | 270 K | Assumed temperature of the back of the Sun shield |

The JAXA *Spacecraft Thermal Control System Design Standard* (JERG-2-310, Section 5.1.4.1) gives an approximate Earth infrared radiation range of **150–300 W/m²**, depending on latitude, season, and weather. The upper value of **300 W/m²** is used here as a conservative assumption, equivalent to a blackbody temperature of approximately **270 K**.

The **270 K internal spacecraft surface temperature is a separate assumption**; it is not specified by the JAXA standard.

Reference: [JAXA JERG-2-310, Spacecraft Thermal Control System Design Standard (PDF)](https://sma.jaxa.jp/TechDoc/Docs/JAXA-JERG-2-310_N3.pdf).

## Radiator emission

The total thermal radiation emitted by the radiator is estimated using the Stefan–Boltzmann law:

\[
P_{\mathrm{emit}} = \varepsilon \sigma S T^4,
\]

where \(\sigma = 5.67 \times 10^{-8}\ \mathrm{W\,m^{-2}\,K^{-4}}\).

For the assumed radiator area and emissivity:

| Radiator temperature | Emitted thermal power |
| --- | ---: |
| 190 K | 8.75 W |
| 172 K | 5.88 W |

## Incoming radiation and net cooling

With an assumed effective environmental temperature of \(T_{\mathrm{env}}=270\ \mathrm{K}\), the incoming Earth and internal heat loads are approximated by

\[
P_{\mathrm{Earth}} = \varepsilon \sigma S T_{\mathrm{env}}^4 F_{\mathrm{Earth}},
\]

\[
P_{\mathrm{internal}} = \varepsilon \sigma S T_{\mathrm{env}}^4 F_{\mathrm{internal}}.
\]

Using the coupling factors above gives

\[
P_{\mathrm{Earth}} \simeq 0.93\ \mathrm{W}, \qquad
P_{\mathrm{internal}} \simeq 0.50\ \mathrm{W},
\]

and therefore

\[
P_{\mathrm{in}} = P_{\mathrm{Earth}} + P_{\mathrm{internal}} \simeq 1.43\ \mathrm{W}.
\]

The net radiative cooling capacity is

\[
P_{\mathrm{net}} = P_{\mathrm{emit}} - P_{\mathrm{in}}.
\]

| Radiator temperature | Emitted power | Estimated incoming power | Net cooling capacity |
| --- | ---: | ---: | ---: |
| 190 K | 8.75 W | 1.43 W | approximately **7.3 W** |
| 172 K | 5.88 W | 1.43 W | approximately **4.4 W** |

In the original design estimate, the **4.4 W** net cooling capacity at 172 K was compared with an assumed detector-side thermal load of approximately **2.9 W**. Under the stated assumptions, the estimated cooling capacity exceeds that load. This comparison does **not** establish the detector's operating temperature.

## Effect of shortening the observation interval

A supplementary case shortens the observation interval by **5° of orbital phase at each end**. The largest orbit-averaged Earth coupling decreases from approximately **0.026 to 0.020**.

| Quantity | Original interval | Shortened interval |
| --- | ---: | ---: |
| Largest orbit-averaged Earth coupling | 0.026 | 0.020 |
| Estimated Earth heat load | 0.93 W | 0.71 W |
| Total estimated incoming heat | 1.43 W | 1.21 W |
| Net cooling capacity at 172 K | about 4.4 W | about 4.7 W |

The improvement is modest because radiation from internal spacecraft surfaces remains a significant part of the estimated heat load. Shortening the observation interval also reduces available observing time, so the thermal benefit must be considered alongside mission operations.

## Scope and limitations

This calculation is intended for preliminary comparison of radiator and shield concepts. In particular:

- Earth coupling is represented by **orbit-averaged** factors rather than time-resolved thermal forcing.
- The Earth's infrared environment and the internal Sun-shield surface are represented by assumed effective temperatures.
- The 270 K internal surface temperature is not a calculated equilibrium temperature.
- Detailed spectral properties, conductive heat paths, and transient spacecraft/detector temperatures are not included.
- Sunlight avoidance has been demonstrated for an example incidence direction, not verified for every operational Sun direction.
- Different orbital conditions, observing schedules, and shield geometries may change the results.

The estimated cooling capacities should therefore be interpreted as **early-stage radiative thermal-budget results**, not final thermal verification.

## Related analyses and source code

- [Earth Radiation Geometry (Dice Satellite Model)]({{ '/projects/satellite/earth-radiation/' | relative_url }}) — incident-direction screening.
- [Thermal Shield Design]({{ '/projects/satellite/shield-design/' | relative_url }}) — two-dimensional shield trade-offs.
- [Radiative Coupling]({{ '/projects/satellite/radiative-coupling/' | relative_url }}) — three-dimensional ray tracing and coupling factors.
- [Three-Dimensional Spacecraft Thermal Radiation Analysis (source README)](https://github.com/indepex/on-orbit-radiator-analysis/blob/main/examples/thermal/3d-model/README.md) — detailed procedures, assumptions, and reproducible calculations.

