---
layout: default
title: Satellite Orbit, Attitude & Thermal Analysis
permalink: /systems/satellite-thermal/
---
# Satellite Orbit, Attitude & Thermal Analysis

## Overview

This study investigates the thermal design of a space telescope operating in 
a low Earth orbit, with the objective of cooling its detector system to approximately 170 K 
using passive radiative cooling alone.

The analysis focuses on minimizing radiative heat input from the Sun and Earth by combining 
orbital propagation, spacecraft attitude modeling, thermal shield design, 
and ray-tracing-based radiative coupling calculations.

## Spacecraft Configuration and Operations

The spacecraft is assumed to operate in a Sun-synchronous dawn-dusk orbit at 
an altitude of approximately 570 km.

During roughly half of each orbit, the telescope observes a fixed celestial target, 
with its optical axis (+Z axis) directed toward the target. 
During the remaining half, the spacecraft adopts a non-observation attitude designed 
to reduce thermal exposure to the Earth.

The spacecraft attitude is also constrained by solar illumination. 
A designated spacecraft side (+X) is oriented approximately toward the Sun during observations 
and aligned with the Sun during the non-observation phase. 
A sunshield is placed on the Sun-facing side to protect the telescope and 
its low-temperature components from direct solar radiation.

<figure>
  <img src="{{ '/assets/images/satellite-attitude.png' | relative_url }}"
       alt="Spacecraft attitude and observation strategy">
  <figcaption>
    Figure 1. Schematic illustration of the spacecraft attitude
    and observation strategy.
 The spacecraft operates in a Sun-synchronous dawn-dusk orbit. 
During approximately half of each orbit, the telescope (+Z axis) points toward 
a fixed celestial target. During the remaining half, the spacecraft adopts 
a different attitude to reduce radiative heat input from the Earth. 
The radiator is located on the +Z side of the telescope, 
while the sunshield protects the spacecraft from direct solar radiation. 
The diagram is schematic and not to scale
  </figcaption>
</figure>


The detector system is designed to operate at approximately 170 K, 
using passive radiative cooling without active cooling devices.

Achieving this temperature requires minimizing radiative heat input from both the Sun and Earth. 
In particular, terrestrial infrared radiation can significantly reduce the cooling capability 
of the radiator.

The thermal design must therefore consider solar shielding and the time-dependent radiative 
coupling between the Earth and the radiator.

## Thermal Design Challenges

The spacecraft configuration and operational constraints lead to several interconnected 
design questions.

- From which directions does terrestrial radiation reach the radiator during observation?
- How does this angular distribution change with orbital position and spacecraft attitude?
- What shield geometry is required to reduce the radiative coupling between 
the Earth and the radiator?
- How do reflections and absorption by surrounding spacecraft structures affect 
the radiator's effective cooling capability?
- How sensitive is the thermal performance to orbital parameters and observation duration?

These questions motivate the analysis workflow described below.


## Analysis Workflow

The analysis follows a step-by-step approach, from orbital and attitude calculations 
to thermal shield design and radiative performance evaluation.

1. **Orbit Propagation** — Calculate the spacecraft orbit and the relative positions of 
the Sun and Earth using orbital parameters and SGP4.

2. **Satellite Attitude** — Model spacecraft attitudes during observation and 
non-observation periods, including attitude transitions and solar avoidance constraints.

3. **Earth Radiation Geometry (Dice Satellite Model)** — Use a simplified cubic satellite 
model to investigate the angular distribution of Earth radiation in spacecraft coordinates. 
Identify critical incident directions and elevation angles for radiator shielding.

4. **Thermal Shield Design** — Determine shielding requirements from the dice-satellite 
analysis and investigate geometrical solutions, including single- and multi-stage conical shields.

5. **Ray-Tracing-Based Radiative Coupling** — Construct a three-dimensional spacecraft model 
and calculate directional radiative coupling, accounting for reflection, absorption, and 
the actual shielding geometry.

6. **Integrated Thermal Analysis** — Combine orbital, attitude, and radiative coupling 
calculations to estimate radiator performance and investigate its dependence on orbital parameters, spacecraft geometry, and operational conditions.

## Topics

### Orbit Propagation

Calculation of spacecraft orbits using TLE and SGP4, including the generation of orbital 
parameters for specified altitudes and local times of ascending node (LTAN). 
The resulting orbital positions provide the basis for evaluating the relative geometry of 
the spacecraft, Earth, and Sun.

[Read more]({{ '/projects/satellite/orbit/' | relative_url }})

### Satellite Attitude

Modeling spacecraft attitudes during observation and non-observation periods. 
The analysis includes target pointing, solar avoidance constraints, 
and attitude transitions using quaternion interpolation.

[Read more]({{ '/projects/satellite/attitude/' | relative_url }})

### Earth Radiation Geometry (Dice Satellite Model)

A simplified cubic satellite model is used to investigate the angular distribution of 
terrestrial radiation in spacecraft coordinates. 
The analysis identifies critical incident directions and elevation angles, 
providing the geometrical requirements for radiator shielding.

[Read more]({{ '/projects/satellite/earth-radiation/' | relative_url }})

### Thermal Shield Design

Geometrical investigation of thermal shields to reduce terrestrial radiation reaching the radiator.
Single- and multi-stage conical shield configurations are compared to determine suitable 
shielding geometries.

[Read more]({{ '/projects/satellite/shield-design/' | relative_url }})

### Radiative Coupling

Ray-tracing calculations of directional radiative coupling between the radiator and 
its surroundings, accounting for reflection and absorption by spacecraft structures. 
The results are used to evaluate the effective radiative coupling with the Earth.

[Read more]({{ '/projects/satellite/radiative-coupling/' | relative_url }})

### Integrated Thermal Analysis

Evaluation of passive radiator cooling performance by combining orbital propagation, 
spacecraft attitude, and three-dimensional radiative coupling calculations. 
The analysis investigates the effects of orbital altitude, LTAN, observation duration, 
and shield geometry on the radiator's thermal performance.

[Read more]({{ '/projects/satellite/thermal-analysis/' | relative_url }})

## Scope

The analyses presented here are intended to demonstrate numerical methods for preliminary spacecraft thermal design. The case study is based on selected design assumptions and simplified thermal models.

The results should not be interpreted as final spacecraft design specifications or as a substitute for detailed transient thermal analysis.
