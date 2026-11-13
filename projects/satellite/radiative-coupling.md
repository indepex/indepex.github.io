---
layout: page
title: Three-Dimensional Radiative Coupling
permalink: /projects/satellite/radiative-coupling/
---

# Three-Dimensional Radiative Coupling

This study evaluates the directional radiative coupling of a spacecraft radiator using a three-dimensional geometric model and ray tracing. It follows the [two-dimensional thermal shield design]({{ '/projects/satellite/shield-design/' | relative_url }}) and provides the coupling factors used in the subsequent thermal balance analysis.

The model includes the spacecraft body, telescope and baffle, solar panels, Earth-radiation shield, and Sun shield. Surface interactions are represented through reflection and absorption. The Earth shield follows the approximately 45° rejection concept examined in the preceding study.

## Spacecraft model

![Three-dimensional spacecraft model]({{ '/assets/images/satellite/radiative-coupling/model.png' | relative_url }})

*Figure 1. Three-dimensional model used in the ray-tracing analysis.*

## Sunlight incidence check

Parallel incident rays are traced from a representative Sun direction, with zenith angle 40° and azimuth 11°. In this test, none of the 1,681 traced rays reached the radiator. This is a check for the specified direction, not a verification over all operational Sun directions.

![Incident-ray tracing]({{ '/assets/images/satellite/radiative-coupling/from_far_grid.png' | relative_url }})

*Figure 2. Incident rays for the tested Sun direction.*

## Directional emission from the radiator

Rays are launched from 1,480 radiator starting points in 100,000 directions, totaling approximately 148 million traced rays. Their interactions with spacecraft surfaces are followed until absorption or escape. Escaping rays are accumulated by direction with cosine weighting, yielding an effective far-field directional distribution.

The calculated fraction of emitted weight absorbed by spacecraft surfaces is approximately **1.35%**. These weights are dimensionless; they are not powers in watts.

![Directional emission distribution]({{ '/assets/images/satellite/radiative-coupling/outward.png' | relative_url }})

*Figure 3. Relative directional emission, normalized to the displayed maximum.*

## Earth coupling along the orbit

At each orbital phase, the Earth's apparent disk is determined in spacecraft coordinates. The directional weights falling within that disk are summed to obtain the geometric coupling fraction:

\[
F_{\mathrm{Earth}}(\phi) = \frac{W_{\mathrm{Earth}}(\phi)}{W_{\mathrm{total}}}.
\]

Here, \(\phi\) is orbital phase, \(W_{\mathrm{Earth}}\) is the accumulated weight in Earth-facing directions, and \(W_{\mathrm{total}}\) is the total emitted weight. This fraction is not itself a heat load.

![Earth coupling versus orbital phase]({{ '/assets/images/satellite/radiative-coupling/earth_coupling.png' | relative_url }})

*Figure 4. Earth coupling as a function of orbital phase for six seasonal and attitude conditions, at 570 km altitude and LTAN 06:00.*

| Solar longitude | Roll angle | Orbit-averaged Earth coupling |
| ---: | ---: | ---: |
| 312° | −6.0° | 0.025 |
| 0° | −0.3° | 0.019 |
| 42° | +5.0° | 0.026 |
| 132° | −6.0° | 0.025 |
| 180° | −0.3° | 0.018 |
| 222° | +5.0° | 0.023 |

The largest **orbit-averaged** coupling factor among these cases is **0.026**. It must not be confused with the maximum instantaneous coupling shown in Figure 4.

## Interpretation and limitations

The three-dimensional analysis accounts for shielding by spacecraft structures and reflections that cannot be evaluated with the preceding two-dimensional cross section alone. Nevertheless, the results depend on the modeled geometry, surface interaction assumptions, orbit, and attitude. Sun avoidance must be checked over the full range of operational incidence directions.

The coupling factors provide inputs for estimating radiative heat loads; the conversion to watts requires separate assumptions about environmental radiation and surface properties. That calculation is treated in the next step, **Thermal Analysis**.

## Code and reproducibility

The geometry, scripts, sample input data, and original figures are available in the [Three-Dimensional Spacecraft Thermal Radiation Analysis example](https://github.com/indepex/on-orbit-radiator-analysis/tree/main/examples/thermal/3d-model). The main programs include `model_view.py`, `from_far.py`, `outward_emission.py`, `outward_view.py`, and `earth_sat.py`.
