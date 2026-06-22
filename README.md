# pervoskite_irradiation
 Pb Block 662 keV Gamma Energy-Deposition Simulation

This repository contains a Geant4/SEE-style macro that simulates monoenergetic 662 keV gamma rays incident on a lead (`Pb`) block and records energy deposition (`Edep`) in a sensitive volume.

## File

- `.mac` — simulation macro file.

## What the Macro Does

The macro defines and runs a simplified lead absorber simulation:

- Uses **22 threads** for the run.
- Defines a material named `Pb_block` with density `11.34 g/cm3` and elemental composition `Pb 1`.
- Builds a bulk lead geometry of `50 mm x 50 mm x 50 mm`.
- Defines a sensitive volume (`SV`) centered inside the absorber with dimensions approximately `49 mm x 49 mm x 49 mm`.
- Uses `G4EmStandardPhysics_option4` for electromagnetic physics.
- Applies production cuts of `1 um` for gammas, electrons, and positrons in both `Bulk` and `SV` regions.
- Shoots a rectangular beam of monoenergetic `662 keV` gamma rays toward the block.
- Scores total deposited energy using standard `Edep` scoring.
- Records the scoring output with a linear histogram from `0` to `0.7 MeV` using `2000` bins.
- Runs `1,000,000` primary events.

## Simulation Setup Summary

| Parameter | Value |
|---|---:|
| Primary particle | gamma |
| Gamma energy | 662 keV |
| Direction | `0 0 -1` |
| Beam center | `0 0 30 mm` |
| Beam shape | Rectangle |
| Beam half-width | 25 mm |
| Beam half-height | 25 mm |
| Absorber material | Lead (`Pb`) |
| Bulk size | `50 mm x 50 mm x 50 mm` |
| Sensitive volume size | `49 mm x 49 mm x 49 mm` |
| Physics list | `G4EmStandardPhysics_option4` |
| Events | 1,000,000 |
| Histogram | Linear, 2000 bins, 0–0.7 MeV |

## How to Run

Run the macro with the simulation executable that supports the `/SEE/...` command set. For example:

```bash
./your_simulation_executable 882cfda0-ef96-405e-aba5-c21614295df7.mac
```

Replace `./your_simulation_executable` with the actual executable for your Geant4/SEE application.

## Expected Output

The macro enables standard energy-deposition scoring:

```text
/SEE/scoring/standard/Edep 1
```

The output should include an energy-deposition histogram configured as:

```text
/SEE/scoring/setHistogram lin 2000 0 0.7 MeV
```

The exact output file name and format depend on the simulation application that implements the `/SEE/scoring/...` commands.

## Notes

- The lead block is made thick enough that the sensitive volume covers nearly the whole absorber while leaving a small margin inside the bulk geometry.
- The incident gamma energy, `662 keV`, is commonly associated with Cs-137 gamma emission.
- The macro is marked as a simplified comparison case based on the style of `TLP.mac`.
- Thread count can be changed by editing:

```text
/run/numberOfThreads 22
```

- The number of simulated events can be changed by editing:

```text
/run/beamOn 1000000
```

## Macro Structure

The macro is organized into these sections:

1. Run settings
2. Material definition
3. Geometry definition
4. Physics list
5. Production cuts
6. Initialization
7. Primary particle source
8. Scoring setup
9. Run command
