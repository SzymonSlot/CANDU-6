# CANDU-6 – 3D full-core model in Serpent 2

*[Wersja polska](README.pl.md)*

Course project for *Numerical Methods* (AGH University of Krakow): a Monte Carlo
model of the full CANDU-6 core (380 fuel channels, 37-element natural-uranium
bundles, heavy-water moderator and reflector) built in the Serpent 2 code.

## Input files

The model is built from nested universes, from the smallest to the largest:

| file | contents | universe |
|---|---|---|
| `materials` | UO2 fuel, Zircaloy-4, Zr-2.5%Nb, Zircaloy-2, annulus gas, D2O coolant / moderator / reflector, S(α,β) data | – |
| `fuelrod` | fuel element over the full channel length (12 bundles × 49.53 cm) | `F` |
| `channel` | 37-element bundle (circular lattice) and fuel channel: pressure tube, gas gap, calandria tube, moderator | `BUN`, `CH` |
| `core` | square lattice of 380 channels (pitch 28.575 cm) inside the calandria (R = 379.7 cm) | `CORE`, `0` |
| `CANDU` | main input: `include`s, run parameters, plots, detectors | – |

## Running

```
serpent -plot CANDU       # geometry plots only
serpent CANDU             # full calculation
serpent -omp 8 CANDU      # parallel, 8 threads
```

Main results: `CANDU_res.m` (k-eff: `ANA_KEFF`, `IMP_KEFF`),
detectors in `CANDU_det0.m` – channel power map (`ChPower`), axial power per bundle
(`AxPower`), two-group flux across the core (`FluxX`).

Input files must have LF line endings (enforced by `.gitattributes`).

## Model assumptions

- fresh natural UO2 fuel at a single temperature (1200 K),
- no reactivity devices (adjusters, absorbers) yet,
- bundle end plates and end shields not modelled; vacuum boundary outside the calandria,
- nuclear data: JEFF-3.2 (cross sections), JEFF-3.1 (thermal scattering).

## Sources

Geometry and material data based on:

- *Burnup Calculation of a CANDU6 Reactor Using the Serpent and MCNP6 Codes*
- *Feasibility Study for Minor Actinides Transmutation in Conventional Power Reactors*
- Serpent Wiki – *2D CANDU fuel bundle geometry*
