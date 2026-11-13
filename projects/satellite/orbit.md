---
layout: default
title: Orbit Propagation
permalink: /projects/satellite/orbit/
---

# Orbit Propagation

## Overview

The spacecraft orbit is calculated to determine the time-dependent position of the 
satellite relative to the Earth and Sun. This information is subsequently used for 
spacecraft attitude modeling and thermal analysis.

The calculation consists of two steps:

1. **TLE Generation:** Generate a synthetic Two-Line Element set (TLE) from specified 
mission parameters, assuming a circular Sun-synchronous orbit.
2. **Orbit Propagation:** Use the SGP4 model to calculate the spacecraft position and 
velocity at specified times.

This approach allows the effects of orbital altitude and local time of ascending node (LTAN) 
to be investigated during preliminary spacecraft design.

## Orbit Parameters

The orbital conditions are specified in
`examples/orbit/input/orbit.json5`.
A representative configuration is:

```json
{
  "epoch": "2033-03-01 12:00:00",
  "ltan": 6.0,
  "altitude": 570.0,
  "InternationalDesignator": "33001A"
}
```

Here, `epoch` is the reference time in UTC, `ltan` is given in hours, and `altitude` is 
given in kilometers. The international designator serves as an identifier in the generated TLE.

The nominal configuration is a low Earth, Sun-synchronous dawn-dusk orbit. 
Different values of altitude and LTAN can be used to investigate alternative orbital conditions.

## TLE Generation

The function `set_TLE()` in `lib_sat.py` generates a synthetic TLE from the specified 
orbital parameters.

### Orbital inclination

For a Sun-synchronous orbit, the secular precession of the right ascension of 
the ascending node (RAAN), caused primarily by the Earth's oblateness, 
must approximately match the apparent annual motion of the Sun.

Using the first-order J2 perturbation model,

\[
\dot{\Omega} =
-\frac{3}{2}J_2 n
\left(\frac{R_E}{a}\right)^2
\frac{\cos i}{(1-e^2)^2}
\]

where \(a\) is the semi-major axis, \(e\) the eccentricity, \(i\) the inclination, \(n\) 
the mean motion, \(R_E\) the Earth's reference radius, and \(J_2\) 
the second zonal harmonic coefficient.

For the assumed circular orbit, \(e=0\) and \(a\) is approximated by the Earth's radius 
plus the specified altitude. The inclination is determined by imposing 
the Sun-synchronous precession rate.

### Local time of ascending node

The LTAN determines the orientation of the orbital plane relative to the Sun.

Let \(\alpha_\odot\) be the right ascension of the Sun at the reference epoch 
and \(L\) the LTAN in hours. The approximate relation is

\[
\Omega = \alpha_\odot + 15^\circ(L-12)
\pmod{360^\circ}
\]

where \(\Omega\) is the RAAN.

This relation is used to determine the orbital plane orientation for the specified epoch and LTAN.

### Mean motion and TLE construction

The mean motion is estimated from the assumed orbital altitude and the Earth's 
gravitational parameter. The resulting orbital elements are formatted into a TLE, 
which is subsequently interpreted by the SGP4 model.

### Generated TLE

For the orbital parameters specified above, the following synthetic TLE is generated:

```text
1 00000U 33001A   33060.50000000  .00000000  00000-0  00000-0 0  9994
2 00000  97.6704 252.2343 0000001 000.0000 090.0000 14.98995172000001
```

The resulting orbital inclination is 97.6704 degrees, and the mean motion is 
14.98995172 revolutions per day, corresponding to an orbital period of approximately 96.06 minutes.

The TLE is generated using `get_tle.py` and the orbital parameters in 
`examples/orbit/input/orbit.json5`. It is intended for preliminary orbit analysis, not as an operational satellite ephemeris.

## Orbit Propagation Using SGP4

The generated TLE is used to initialize the SGP4 propagator with `Satrec.twoline2rv()`.

The spacecraft position and velocity are calculated at successive time steps. 
The resulting position vectors are expressed in the TEME coordinate system.

For ground-track visualization, the positions are transformed from TEME to the Earth-fixed ITRS 
coordinate system using Astropy. The geodetic latitude and longitude are then plotted using Cartopy.

### Ground Track

![Ground track of a Sun-synchronous orbit]({{ '/assets/images/satellite/orbit/orbit-map.png' | relative_url }})

*Ground track over 24 hours starting at 2033-03-01 12:00 UTC. The first orbital revolution is highlighted in red, while the full 24-hour trajectory is shown in blue. The specified orbit has an altitude of 570 km and an LTAN of 6:00.*

The spacecraft completes approximately 15 revolutions per day. The displacement of successive ground tracks is caused by the Earth's rotation.

## Implementation

The orbit calculation is implemented in Python using Astropy and the `sgp4` package. Cartopy and Matplotlib are used for visualization.

The principal files in the `on-orbit-radiator-analysis` repository are:

| File | Purpose |
|---|---|
| `get_tle.py` | Generate a synthetic TLE from the specified orbital parameters |
| `lib_sat.py` | Calculate orbital elements and construct the TLE |
| `lib_utils.py` | Common utility functions |
| `orbit_map.py` | Propagate the orbit using SGP4 and plot the ground track |
| `examples/orbit/input/orbit.json5` | Input orbital parameters |
| `examples/orbit/output/orbit.tle` | Generated TLE |
| `examples/orbit/output/orbit-map.png` | Ground-track figure |

### Reproducing the Results

From the root directory of the `on-orbit-radiator-analysis` repository, generate the TLE:

```bash
python get_tle.py --orb examples/orbit/input/orbit.json5 \
    > examples/orbit/output/orbit.tle
```

Then generate the ground-track figure:

```bash
python orbit_map.py \
    --tle examples/orbit/output/orbit.tle \
    --days 1 \
    --step 60 \
    -o examples/orbit/output/orbit-map.png
```

The input data, source code, and generated outputs are included in the repository.

## Limitations

The TLE is generated from simplified orbital assumptions, including a circular orbit and 
a first-order Sun-synchronous condition. 
It does not represent a measured or operationally maintained spacecraft orbit.

The conversion from LTAN to RAAN is approximate, and the generated orbital elements are 
not fitted to a high-precision numerical orbit solution.

The method is intended for comparative studies of spacecraft geometry and thermal 
performance during preliminary design.

