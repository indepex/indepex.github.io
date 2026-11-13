---
layout: default
title: On-Orbit Radiator Analysis
permalink: /systems/on-orbit-radiator-analysis/
---

# On-Orbit Radiator Analysis

## Overview

This project explores passive radiative cooling for a space telescope in low Earth orbit. The design study aims to cool its detector system to approximately 170 K by reducing heat input from the Sun, Earth, and surrounding spacecraft structures.

The analysis integrates orbit propagation, attitude modeling, Earth-radiation geometry, reflective shield design, three-dimensional ray tracing, and a preliminary thermal balance. The source code, example inputs, and reproducible results are available in the [on-orbit-radiator-analysis GitHub repository](https://github.com/indepex/on-orbit-radiator-analysis) (repository access depends on its visibility settings).

## Spacecraft Configuration and Operations

The example spacecraft operates in a Sun-synchronous dawn–dusk orbit at approximately 570 km altitude. During roughly half of each revolution, its telescope (+Z axis) points toward a fixed celestial target. During the remaining half, a non-observation attitude is used to reduce thermal exposure to Earth. The Sun-facing side (+X) is protected by a sunshield; the radiator is located on the +Z side.

<figure>
  <img src="{{ '/assets/images/satellite-attitude.png' | relative_url }}" alt="Schematic spacecraft attitude and observation strategy">
  <figcaption>Figure 1. Schematic spacecraft attitude and observation strategy. The illustration is not to scale.</figcaption>
</figure>

The key challenge is to preserve a sufficiently large radiator area while limiting radiation incident from Earth and the spacecraft itself.

## Analysis Workflow

The study proceeds through six linked topics:

1. **Orbit Propagation** — Determine spacecraft position and Sun–Earth geometry using orbital parameters and SGP4.
2. **Satellite Attitude** — Model target pointing, non-observation attitudes, and attitude transitions.
3. **Earth Radiation Geometry** — Identify incident Earth-radiation directions with a simplified dice-satellite model.
4. **Thermal Shield Design** — Compare reflective shield geometries and their radiator-area penalties.
5. **Radiative Coupling** — Use a three-dimensional spacecraft model and ray tracing to quantify directional emission and Earth coupling.
6. **Thermal Analysis** — Convert coupling factors into preliminary heat loads and net cooling capacity under stated assumptions.

## Topics

### Orbit Propagation

Satellite orbit calculations using TLE and SGP4, including example orbits at selected altitudes and local times of ascending node (LTAN). The resulting spacecraft position provides the geometry needed for subsequent attitude and thermal calculations.

[Read more]({{ '/projects/satellite/orbit/' | relative_url }})

### Satellite Attitude

Modeling observation and non-observation attitudes, target pointing, solar constraints, and quaternion-based transitions. These calculations determine how the Earth appears in spacecraft coordinates throughout an orbit.

[Read more]({{ '/projects/satellite/attitude/' | relative_url }})

### Earth Radiation Geometry (Dice Satellite Model)

A simplified cubic satellite model maps the directions from which Earth infrared radiation can reach the radiator. For the examined orbit and attitude cases, significant exposure occurs near the ±Y directions, with incident elevations extending toward 70° above the radiator plane. This is a directional screening study, not a calculation of thermal power.

[Read more]({{ '/projects/satellite/earth-radiation/' | relative_url }})

### Thermal Shield Design

Two-dimensional specular ray tracing compares single-stage and two-stage reflective shields. Rejecting radiation up to 70° strongly reduces available radiator area; a 45° design provides a less restrictive geometric compromise.

[Read more]({{ '/projects/satellite/shield-design/' | relative_url }})

### Radiative Coupling

Three-dimensional ray tracing includes the radiator, thermal shields, and surrounding spacecraft structures. The resulting directional emission distribution is combined with orbit and attitude data to estimate Earth coupling. Across six examined cases, the orbit-averaged coupling factors range from approximately 0.018 to 0.026.

[Read more]({{ '/projects/satellite/radiative-coupling/' | relative_url }})

### Integrated Thermal Analysis

A simplified steady-state radiation budget combines the geometric coupling results with assumptions about radiator area, emissivity, and environmental temperatures. Under the example assumptions, the net radiative cooling capacity is approximately 7.3 W at 190 K and 4.4 W at 172 K. These values are preliminary estimates, not transient temperature predictions.

[Read more]({{ '/projects/satellite/thermal-analysis/' | relative_url }})

## Scope and Limitations

This is an engineering case study intended to demonstrate numerical methods and design trade-offs. The examples use simplified geometry, prescribed spacecraft attitudes, idealized surface interactions in some stages, and an approximate thermal balance. They do not constitute a final spacecraft thermal verification or a full transient thermal model.

For implementation details, input files, and example results, see the [GitHub repository](https://github.com/indepex/on-orbit-radiator-analysis).
