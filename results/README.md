# Key Engineering Results

This section summarizes the principal engineering results obtained during the
development and numerical investigation of the CHARON Blended Wing Body UAV.

The project combined aerodynamic optimization, low- and higher-fidelity
aerodynamic modelling, full-aircraft CFD and propulsion–airframe integration
to investigate the behaviour of the BWB configuration and the subsequent
integration of Electric Ducted Fan propulsion.

Detailed methodology is documented separately in:

- [`optimization/`](../optimization/) — aerodynamic optimization framework
- [`cfd/`](../cfd/) — CFD methodology, validation and configuration studies
- [`propulsion/`](../propulsion/) — EDF architecture and integration concept

---

## 1. Aerodynamic Design and Optimization

The CHARON geometry was developed as a multi-segment Blended Wing Body and
optimized using a CMA-ES-based computational framework.

The optimization process coupled:

- CMA-ES optimization in MATLAB
- custom FORTRAN90 aerodynamic and geometry-processing routines
- NACA 2412 and reflexed NACA 2412 airfoil families
- XFOIL/XFLR5 aerodynamic data
- spanwise aerodynamic calculations
- force and pitching-moment integration

The design objective combined aircraft lift capability, aerodynamic
efficiency and longitudinal pitching-moment behaviour into a single
optimization problem.

The resulting configuration provided the aerodynamic baseline for the
subsequent CFD and propulsion-integration studies.

For the complete optimization methodology and computational architecture,
see [`optimization/`](../optimization/).

---

## 2. 2D Aerodynamic Validation

Before proceeding to full-aircraft CFD, two-dimensional CFD predictions were
compared with XFOIL/XFLR5 results for four airfoil configurations:

- NACA 2412 Standard
- NACA 2412 Reflex05
- NACA 2412 Reflex010
- NACA 2412 Reflex015

The comparison included:

- lift coefficient, CL
- drag coefficient, CD
- aerodynamic efficiency, CL/CD

Reasonable agreement was observed in the approximately linear pre-stall lift
regime.

The principal discrepancies appeared at higher angles of attack, where CFD
predicted an earlier onset of stall and higher drag than the lower-fidelity
aerodynamic model.

These differences motivated the extension of the investigation to
three-dimensional CFD of the complete aircraft.

---

## 3. Clean-Aircraft CFD Baseline

The complete CHARON geometry was analysed in OpenFOAM at a reference velocity
of:

**V = 40 m/s (77.75 kt)**

The three-dimensional computational model used approximately:

- **10 million cells**
- **30 inflation layers**
- near-wall resolution targeting **y⁺ < 10**

The clean-aircraft angle-of-attack sweep identified a near-zero
pitching-moment condition around:

**AoA ≈ 3.9°**

Representative results at this condition were:

| Quantity | Value |
|---|---:|
| Angle of attack | 3.9° |
| Lift | 2001 N |
| Drag | 196 N |
| Pitching moment | -34 N·m |
| CL | 0.1556 |
| CD | 0.0152 |
| Cm | -0.00096 |

This condition provided the reference point for the subsequent
propulsion-integration studies.

---

## 4. External Propulsion Integration

The first propulsion-integration study retained the EDF nacelles externally
mounted on the upper surface of the BWB.

Three configurations were compared:

| Configuration | Description | Reported L/D |
|---|---|---:|
| C1 | Clean aircraft | 10.33 |
| C2 | External nacelles, rotor off | 9.64 |
| C3 | External nacelles, operating EDF | 12.92 |

The C2 configuration demonstrated the aerodynamic penalty introduced by the
external nacelles when considered without rotor operation.

The C3 configuration subsequently introduced the operating EDF and therefore
propulsion–airframe aerodynamic interaction.

For the C3 study, the EDF was operated at a nominal rotational speed of:

**N = 5500 rpm**

Because the rotor produces thrust, the resulting total axial force cannot be
interpreted directly as passive aerodynamic drag. The configuration-level
results must therefore be considered together with the component force
breakdown documented in the CFD study.

---

## 5. Embedded Nacelle / BLI Investigation

The propulsion architecture was subsequently modified by recessing the
nacelles into the upper BWB geometry.

This embedded configuration allowed the EDF inlet to interact more directly
with the near-wall flow and formed the basis of the Boundary Layer Ingestion
investigation.

Two principal configurations were considered:

- **C2\*** — embedded nacelles, rotor off
- **C3\*** — embedded nacelles with operating EDF

For the embedded rotor-off configuration at AoA = 4°, the reported
aerodynamic efficiency was:

**C2\*: L/D = 10.36**

The operating-EDF configuration was then evaluated over three rotor speeds.

| Configuration | Rotor speed [rpm] | Fx [N] | Fy [N] | Fz [N] | Reported L/D |
|---|---:|---:|---:|---:|---:|
| C3*-A | 4770 | 119.25 | -286.48 | 1118.73 | 9.39 |
| C3*-B | 5732 | 131.74 | -294.95 | 1160.67 | 8.85 |
| C3*-C | 6687 | 147.70 | -346.79 | 1203.90 | 8.18 |

The rotor-speed sweep revealed an important propulsion–airframe integration
trade-off.

Increasing EDF rotational speed increased the vertical aerodynamic force
component and altered the flow around the embedded installation.

However, the increased aerodynamic loading was accompanied by increased
pressure drag.

Consequently, the reported aerodynamic efficiency decreased across the
investigated rotor-speed range:

**L/D: 9.39 → 8.85 → 8.18**

for:

**4770 → 5732 → 6687 rpm**

The highest investigated rotor speed therefore did not correspond to the
highest aerodynamic efficiency.

---

## 6. Principal Engineering Findings

The CHARON investigation produced several principal observations:

1. **Model fidelity matters.**  
   XFOIL/XFLR5 and CFD produced comparable trends in the approximately linear
   pre-stall regime, while increasingly different behaviour appeared in drag
   prediction and near stall.

2. **Propulsion installation cannot be evaluated independently of the
   airframe.**  
   Adding external nacelles introduced a measurable aerodynamic penalty
   relative to the clean aircraft.

3. **Rotor operation fundamentally changes the axial-force balance.**  
   Once the EDF is operating, thrust and passive aerodynamic drag contribute
   simultaneously to the measured axial force and must be interpreted
   separately.

4. **Geometric integration changes the propulsion–airframe interaction.**  
   Recessing the nacelles introduced direct interaction between the EDF inlet
   and the near-wall flow over the BWB.

5. **Higher EDF rotational speed did not automatically produce higher
   aerodynamic efficiency.**  
   The embedded-nacelle sweep showed increasing aerodynamic loading together
   with decreasing L/D over the investigated rotational-speed range.

6. **The final configuration is therefore governed by a coupled design
   trade-off.**  
   Airframe aerodynamics, nacelle geometry, rotor operating condition and
   propulsion integration cannot be optimized independently when evaluating
   the complete aircraft.

---

## 7. Scope and Limitations

The reported results should be interpreted within the scope of the numerical
methodology used in the project.

Important limitations include:

- sensitivity of CFD predictions to mesh resolution and near-wall treatment,
- differences between XFOIL/XFLR5 and CFD near nonlinear and post-stall flow,
- simplified numerical representation of the propulsion system,
- limited experimental validation,
- configuration comparisons performed at selected operating conditions
  rather than across a complete propulsion–airframe operating envelope.

The project should therefore be interpreted as a comparative numerical
investigation of aerodynamic design and propulsion–airframe integration,
rather than as a fully validated aircraft performance model.

---

## Detailed Documentation

Further technical details are available in:

- **[Optimization](../optimization/)** — CMA-ES framework, design variables,
  aerodynamic model and objective function
- **[CFD](../cfd/)** — 2D validation, OpenFOAM methodology, C1/C2/C3 analysis
  and embedded-nacelle rotor-speed study
- **[Propulsion](../propulsion/)** — EDF architecture, external installation
  and embedded/BLI integration concept
