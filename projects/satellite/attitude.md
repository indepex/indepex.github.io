---
layout: default
title: Spacecraft Attitude Modeling
permalink: /projects/satellite/attitude/
---

<style>
.attitude-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 16px;
    margin: 24px 0;
}

.attitude-grid figure {
    margin: 0;
    min-width: 0;
}

.attitude-grid img {
    display: block;
    width: 100%;
    height: auto;
    border: 1px solid #ddd;
}

.attitude-grid figcaption {
    text-align: center;
    font-size: 0.85em;
    margin-top: 6px;
}

@media (max-width: 800px) {
    .attitude-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
    }
}

@media (max-width: 500px) {
    .attitude-grid {
        grid-template-columns: 1fr;
    }
}
</style>


# Spacecraft Attitude Modeling

## Overview

The spacecraft attitude is calculated over one orbital revolution to investigate the orientation 
of the satellite relative to the Sun, Earth, and observation target.

The attitude model consists of two operating modes:

1. **Observation mode:** The spacecraft points its observation axis toward a fixed celestial 
target while maintaining a prescribed orientation relative to the Sun.
2. **Non-observation mode:** The spacecraft performs a rotation approximately about the Sun 
direction, returning to the required observation attitude before the next observation period.

The model is intended for preliminary spacecraft design, including the evaluation of viewing 
geometry and the angular relationships between spacecraft surfaces and the surrounding environment.

The attitude is represented by three orthogonal spacecraft-fixed unit vectors, 
expressed in an approximately common inertial coordinate system.

The calculation and visualization processes are separated. 
The attitude calculation first produces a compressed NumPy NPZ file containing the orbital 
and attitude data. 
All plots and three-dimensional visualizations are subsequently generated from this file, 
without repeating the attitude calculation.

The NPZ file also serves as a common source of numerical data for further analysis. 
When alternative representations are required, such as Euler angles, quaternions, 
rotation matrices, or attitude relative to the local orbital frame, 
they can be derived from the stored data using separate conversion programs. 
This approach allows additional data products to be generated without modifying or 
rerunning the original attitude calculation.

## Attitude Model

### Spacecraft Coordinate System

The spacecraft attitude is defined by three body-fixed axes:

- **X-axis:** The spacecraft axis used as the reference direction for Sun-oriented rotation 
during the non-observation period.
- **Y-axis:** The axis constrained to be perpendicular to the Sun direction before applying 
the observation roll correction.
- **Z-axis:** The observation axis, directed toward the celestial target during 
the observation period.

The axes form a right-handed orthonormal coordinate system.

### Observation Mode

During the observation period, the spacecraft Z-axis is directed toward the observation target.

The initial attitude is constructed so that the Y-axis is perpendicular to both 
the target and Sun directions. A roll correction about the Z-axis is then applied to 
obtain the specified position angle relative to celestial north.

The roll correction is calculated from the Sun-target geometry and the prescribed 
target position angle.

In the present example, the observation target is the Galactic Center.

### Non-Observation Mode

During the non-observation period, the spacecraft follows a Sun-oriented attitude profile.

At the center of this period:

- The spacecraft X-axis is aligned with the Sun direction.
- The spacecraft Z-axis lies in the plane defined by the satellite position, 
Earth center, and Sun direction, with its component perpendicular to the Sun 
direction pointing away from Earth.
- The spacecraft rotates approximately one full revolution about the Sun-oriented X-axis 
over the non-observation interval.

Short transition intervals connect this rotating attitude profile to the observation 
attitudes at the beginning and end of the observation period.

The transition attitudes are calculated using quaternion interpolation. 
In the present implementation, each transition interval spans 10° of orbital phase.

This is a prescribed kinematic attitude model rather than a simulation of spacecraft 
attitude-control dynamics.

## Simulation Conditions

The example considers a low Earth, Sun-synchronous dawn-dusk orbit with the following parameters.

| Parameter | Value |
|---|---|
| Orbital altitude | 570 km |
| Local time of ascending node (LTAN) | 06:00 |
| Observation target | Galactic Center |
| Target position-angle parameter | −2° |
| Orbital revolutions | One per case |
| Orbital phase interval | 0°–360° |
| Sampling interval | 5° |
| Solar ecliptic longitudes | 312°, 0°, 42°, 132°, 180°, 222° |

Six solar-longitude conditions are selected to examine the seasonal dependence of 
the spacecraft attitude.

The calculated roll correction differs between cases because the relative geometry of 
the Sun and observation target changes.

| Case | Solar longitude | Calculated roll correction |
|---|---:|---:|
| 00 | 312° | −6.04° |
| 01 | 0° | −0.25° |
| 02 | 42° | +4.99° |
| 03 | 132° | −6.04° |
| 04 | 180° | −0.26° |
| 05 | 222° | +4.99° |

## Results

### Three-Dimensional Attitude Visualization

The spacecraft attitude is visualized along one orbital revolution using a simplified arrow model.

The arrows represent the spacecraft body axes:

- **Red:** Spacecraft Z-axis
- **Green:** Spacecraft X-axis
- **Blue:** Spacecraft Y-axis

The spacecraft attitude is drawn at 5° orbital-phase intervals. Phase labels are displayed every 30° to improve readability.

The Earth and orbital path provide a spatial reference for examining the changing spacecraft orientation.

<div class="attitude-grid">
  {% assign solar_longitudes = "312,0,42,132,180,222" | split: "," %}
  {% for longitude in solar_longitudes %}
  {% assign index = forloop.index0 | prepend: "0" | slice: -2, 2 %}
  <figure>
    <a href="{{ '/assets/images/satellite/attitude/attitude_view' | append: index | append: '.png' | relative_url }}">
      <img src="{{ '/assets/images/satellite/attitude/attitude_view' | append: index | append: '.png' | relative_url }}"
           alt="Spacecraft attitude at solar longitude {{ longitude }} degrees">
    </a>
    <figcaption>Solar longitude {{ longitude }}°</figcaption>
  </figure>
  {% endfor %}
</div>

*Figure 1. Three-dimensional spacecraft attitude for six solar-longitude conditions. Click an image to enlarge it.*

The figures illustrate the seasonal variation of the spacecraft attitude while preserving the same basic observation and non-observation strategy.

### Angular Relationships

The angular relationships between the spacecraft and its environment are evaluated throughout each orbit.

The upper panel of each plot shows:

- Elevation of the observation target
- Elevation of the Sun in spacecraft coordinates
- Azimuth of the Sun in spacecraft coordinates

The lower panel shows the elevation of the Earth direction relative to the spacecraft X-, Y-, and Z-axes.

These quantities provide a convenient description of the changing observation and illumination geometry.

<div class="attitude-grid">
  {% assign solar_longitudes = "312,0,42,132,180,222" | split: "," %}
  {% for longitude in solar_longitudes %}
  {% assign index = forloop.index0 | prepend: "0" | slice: -2, 2 %}
  <figure>
    <a href="{{ '/assets/images/satellite/attitude/attitude_plot' | append: index | append: '.pdf' | relative_url }}">
      <img src="{{ '/assets/images/satellite/attitude/attitude_plot' | append: index | append: '.png' | relative_url }}"
           alt="Angular relationships at solar longitude {{ longitude }} degrees">
    </a>
    <figcaption>Solar longitude {{ longitude }}° — PDF</figcaption>
  </figure>
  {% endfor %}
</div>

*Figure 2. Angular relationships for six solar-longitude conditions. Click a plot to open the full-resolution PDF.*

## Implementation and Reproduction

The calculations are implemented in Python.

The principal programs are:

- `orb_att.py` — Calculates the spacecraft attitude and saves the results.
- `orb_view.py` — Generates angular plots and three-dimensional attitude visualizations.
- `lib_sat.py` — Provides orbital and attitude calculation functions.
- `lib_plot.py` — Provides plotting functions.
- `lib_view.py` — Provides three-dimensional visualization functions.

### Attitude Calculation

The six example cases can be calculated using:

```bash
python orb_att.py \
    -s examples/attitude/output/attitude.npz \
    --orb examples/orbit/input/orbit.json5 \
    --obj examples/orbit/input/GC_pos.json5 \
    --sln 312,0,42,132.0,180,222.0 \
    --ltan 6 --alt 570 --tpa -2
```

The input files define the reference orbital conditions and the observation target.

### Angular Plots

```bash
python orb_view.py \
    examples/attitude/output/attitude.npz \
    -f \
    -d examples/attitude/output \
    -n attitude
```

### Three-Dimensional Visualization

```bash
python orb_view.py \
    examples/attitude/output/attitude.npz \
    -v -m arrow \
    -d examples/attitude/output \
    -n attitude
```

The visualization program generates PNG images and interactive HTML files.

### Numerical Output

The calculated results are stored in a compressed NumPy NPZ file.

Each case contains:

- Orbital and observation parameters
- Orbital phase
- Sample times
- Spacecraft position and velocity
- Spacecraft X-, Y-, and Z-axis unit vectors
- Sun and Earth direction vectors
- Observation target direction
- Calculated roll correction

The spacecraft position and velocity are stored in kilometers and kilometers per second, respectively.

The attitude axes are stored as unit vectors rather than Euler angles. This representation avoids dependence on a particular Euler-angle convention and allows subsequent conversion to rotation matrices, quaternions, or alternative reference frames.

The NPZ file is intended to serve as the numerical interface between attitude calculation and subsequent analysis.

## Assumptions and Limitations

The following approximations and limitations apply to the present implementation.

**Orbital model.** The spacecraft orbit is propagated using SGP4 from a synthetic TLE representing the specified Sun-synchronous orbit.

**Coordinate systems.** The SGP4 position and velocity are expressed in TEME coordinates. The solar direction is obtained from Astropy, while the target direction is defined in ICRS. These directions are treated as belonging to an approximately common inertial coordinate system. The small differences between these frames are neglected for the present preliminary analysis.

**Attitude-control dynamics.** The prescribed attitude profile is kinematic. Spacecraft inertia, actuator limitations, angular-rate constraints, and control errors are not modeled.

**Attitude transitions.** Quaternion interpolation is used to connect the observation and non-observation attitude profiles over specified orbital-phase intervals. The resulting maneuver durations and angular rates are not independently validated against attitude-control hardware capabilities.

**Observation geometry.** The model assumes a fixed celestial target and an idealized pointing strategy. Detailed operational constraints, including acquisition and settling times, are not included.

Despite these simplifications, the model provides a consistent geometric description of spacecraft attitude over an orbit and a reusable numerical basis for further analysis.
