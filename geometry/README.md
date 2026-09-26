# Aircraft Geometry

This section documents the geometric definition and three-dimensional
development of the CHARON Blended Wing Body UAV.

The aircraft geometry was not treated as an independent CAD exercise.
Instead, it was linked directly to the aerodynamic design and optimization
process, with spanwise airfoil selection, incidence and twist defining the
resulting BWB configuration.

The resulting geometry was subsequently converted into a watertight
three-dimensional model suitable for full-aircraft CFD and propulsion
integration.

---

## Parametric BWB Definition

The CHARON lifting body was represented through multiple spanwise segments.

Each segment was defined through geometric and aerodynamic parameters
including:

- spanwise position
- root and tip chord
- airfoil section
- local incidence
- twist
- taper
- sweep
- dihedral

For the aerodynamic calculations, each segment was further divided into
10 spanwise sections.

This discretization allowed local airfoil properties and geometric parameters
to be associated with the corresponding spanwise location.

---

## Baseline Geometry

Representative baseline design parameters included:

| Parameter | Value |
|---|---:|
| Design mass | 205 kg |
| Reference velocity | 40 m/s |
| Reference area | 13.37 m² |
| Mean aerodynamic chord | 3.2 m |
| Root chord | 4.6 m |

The geometric definition was progressively refined through the aerodynamic
optimization process rather than being fixed entirely at the beginning of
the project.

---

## Spanwise Airfoil Distribution

The aerodynamic design used members of the NACA 2412 family with different
degrees of trailing-edge reflex:

- NACA 2412 Standard
- NACA 2412 Reflex05
- NACA 2412 Reflex010
- NACA 2412 Reflex015

The optimization framework selected the airfoil distribution together with
the local incidence and twist parameters.

A NACA 0012 symmetric section was additionally used in the outer
wing-tip region during the final geometric development.

This combination allowed the spanwise aerodynamic characteristics of the BWB
to be modified while accounting for both aerodynamic efficiency and
longitudinal pitching-moment behaviour.

---

## Optimized Spanwise Definition

The optimization produced the local incidence and airfoil assignments used
to generate the aircraft geometry.

Representative optimized incidence values were:

| Spanwise station | Incidence |
|---|---:|
| 1 | 1.309° |
| 2 | 1.149° |
| 3 | 0.509° |
| 4 | 0.109° |
| 5 | -0.291° |
| 6 | -0.691° |

The corresponding optimized airfoil-family assignments were then used by the
geometry-generation routines to construct the local sections of the aircraft.

The gradual reduction in local incidence toward the outer wing contributed
to the spanwise twist distribution used by the final BWB geometry.

---

## Geometry Generation

A custom FORTRAN90 routine was used to convert the optimized aerodynamic
parameters into airfoil-section coordinates.

The geometry-generation process combined:

1. the selected airfoil definition,
2. the optimized local incidence,
3. spanwise scaling according to local chord,
4. geometric positioning of each section,
5. sweep and dihedral transformations.

This provided a direct connection between the optimization output and the
three-dimensional aircraft definition.

The generated sections were subsequently imported into the geometric
modelling workflow used to construct the complete BWB surface.

---

## Three-Dimensional Surface Development

The initial aerodynamic geometry was developed using XFLR5 and subsequently
exported for further three-dimensional processing.

The geometry workflow included:

**XFLR5 aerodynamic definition**  
↓  
**airfoil-section / spanwise geometry generation**  
↓  
**3D surface construction**  
↓  
**STL export**  
↓  
**Blender / Meshmixer processing**  
↓  
**watertight CFD-ready geometry**

Additional surface processing was required because the aerodynamic model
alone was not sufficient for robust three-dimensional meshing.

Blender and Meshmixer were therefore used to refine the surface geometry,
remove geometric inconsistencies and prepare a closed model suitable for
OpenFOAM meshing.

---

## CFD Geometry Preparation

The final surface model had to satisfy requirements beyond the original
aerodynamic representation.

In particular, the geometry was prepared to support:

- watertight STL export,
- surface triangulation,
- `snappyHexMesh` processing,
- symmetry-plane treatment,
- local mesh refinement,
- subsequent nacelle integration.

This CFD-ready geometry became the baseline **C1 clean-aircraft
configuration** used in the three-dimensional OpenFOAM study.

Further modifications of this baseline geometry produced the external and
embedded propulsion configurations documented in:

- [`propulsion/`](../propulsion/)
- [`cfd/`](../cfd/)

---

## Geometry Evolution

The geometric development of CHARON can therefore be summarized as:

**Conceptual BWB**
→ **parametric spanwise definition**
→ **CMA-ES aerodynamic optimization**
→ **optimized airfoil / incidence / twist distribution**
→ **3D BWB surface**
→ **watertight CFD geometry**
→ **external EDF installation**
→ **embedded nacelle / BLI configuration**

This progression allowed the same underlying aircraft concept to be carried
from aerodynamic design through full-aircraft CFD and propulsion–airframe
integration.
