---
layout: page
title: Thermal Shield Design
permalink: /projects/satellite/shield-design/
---

# Thermal Shield Design

## Objective

The preceding [Earth Radiation Geometry]({{ '/projects/satellite/earth-radiation/' | relative_url }}) study found that Earth infrared radiation reaches the spacecraft radiator mainly from directions near the ±Y axes. The incident directions extend to elevations of approximately 70° above the radiator plane, although the largest contribution occurs near 30°.

This study investigates reflective thermal-shield geometries and the trade-off between rejecting high-elevation radiation and preserving useful radiator area.

## Two-Dimensional Shield Models

A flat radiator is placed at the bottom of a reflective cup. Two cross-sectional geometries are considered:

- **Single-stage shield:** one straight wall segment between the radiator and the aperture.
- **Two-stage shield:** two straight wall segments with different inclinations, providing additional geometric freedom.

The wall surfaces are modeled as ideal specular reflectors. Rays may undergo multiple reflections before escaping or reaching the radiator. The *limiting elevation angle* is the maximum incident elevation rejected under the modeled geometric conditions.

For the single-stage geometry, physically meaningful solutions with nonnegative bottom radius exist only up to 60°. Two-stage geometries can reject rays at higher limiting elevations.

## Shielding Performance versus Radiator Area

For a shield height of 600 (in consistent length units), the calculated representative two-stage geometries are:

| Limiting elevation | Aperture radius | Bottom radius | Aperture / bottom radius | Radiator area / aperture area |
| --- | ---: | ---: | ---: | ---: |
| 60° | 293.4 | 132 | 2.2 | 20% |
| 65° | 293.5 | 108 | 2.7 | 14% |
| 70° | 304.0 | 88 | 3.5 | 8% |

For circular surfaces, the area ratio is the square of the bottom-to-aperture radius ratio. Rejection of higher-elevation rays therefore imposes a substantial penalty on the available radiator area.

[![Aperture-to-bottom radius ratio]({{ '/assets/images/satellite/shield/ratio2ss.png' | relative_url }})]({{ '/assets/images/satellite/shield/ratio2ss.pdf' | relative_url }})

*Figure 1. Aperture-to-bottom radius ratio for two-stage shields at limiting elevations of 60°, 65°, and 70° (height 600). Select the figure to open the PDF.*

## High-Elevation Shield: 70°

The two-stage design permits a 70° limiting elevation where the single-stage geometry cannot provide a physically meaningful solution under the same assumptions. However, the remaining radiator area is only approximately 8% of the aperture area.

[![Two-stage shield at 70 degrees]({{ '/assets/images/satellite/shield/s70.png' | relative_url }})]({{ '/assets/images/satellite/shield/s70.pdf' | relative_url }})

*Figure 2. Two-stage shield cross section and representative ray trajectories for a 70° limiting elevation.*

## A Less Restrictive Shield: 45°

A two-stage shield with the following geometry was also examined:

| Parameter | Value |
| --- | ---: |
| Aperture radius | 300 |
| Bottom (radiator) radius | 199 |
| Transition radius | 261 |
| Transition height | 196 |
| Total height | 600 |
| Limiting elevation | 45° |

The bottom-to-aperture area ratio is approximately **44%**, compared with **8%** for the 70° design. The model rejects rays at or below 45°, while some higher-elevation rays can reach the radiator.

[![Two-stage shield at 45 degrees]({{ '/assets/images/satellite/shield/s45.png' | relative_url }})]({{ '/assets/images/satellite/shield/s45.pdf' | relative_url }})

*Figure 3. Two-stage shield cross section and ray trajectories for a 45° limiting elevation.*

## Design Implications

Rejecting every geometrically possible Earth-radiation direction is not necessarily the best design objective. Since the strongest directional contribution in the preliminary analysis occurs near 30°, a less restrictive shield may preserve substantially more radiator area while accepting some residual radiation from higher elevations.

The preferred design must ultimately be evaluated using the actual three-dimensional spacecraft geometry and the orbital distribution of Earth radiation. In practice, shielding concentrated along the ±Y directions may be more appropriate than a fully axisymmetric conical shield.

## Scope and Limitations

This is a **two-dimensional geometric ray-tracing study**, not a prediction of thermal power. The analysis assumes ideal specular reflection and does not include finite reflectivity, absorption, roughness, shield thermal emission, or conduction. The results do not by themselves establish the performance of a complete three-dimensional spacecraft shield.

## Source Code and Detailed Example

The programs `shield2d/ratio2ss.py`, `shield2d/shield.py`, and `shield2d/modelshield.py` share the geometric and ray-tracing functions in `shield2d/lib_shield.py`.

- [Detailed example, numerical methods, and commands](https://github.com/indepex/on-orbit-radiator-analysis/tree/main/examples/thermal/shield-2d)
- [Shield-analysis source code](https://github.com/indepex/on-orbit-radiator-analysis/tree/main/shield2d)

[Back to Satellite Orbit, Attitude & Thermal Analysis]({{ '/systems/satellite-thermal/' | relative_url }})
