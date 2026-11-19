# hardware — bill of materials and CAD

<p align="center"><img src="../.github/media/mabel_lab.jpg" width="560" alt="MABEL"></p>

```text
bom/    Bill of materials + build guide (MABEL_Build_Guide.pdf, mabel_bom.pdf, data/*.csv)
cad/    Full-robot assembly, STEP (zipped)
```

## Build in four steps

1. **Order parts** from [`bom/MABEL_Build_Guide.pdf`](bom/MABEL_Build_Guide.pdf) — vendor links and
   the three reference builds (Essential / Recommended / Maximum). `bom/data/core.csv` is the
   source of truth; regenerate the PDFs and figures with `cd bom && python3 tools/build_bom.py`.
2. **Open the CAD**: `unzip cad/MABEL_full_assembly.step.zip` and import the STEP into any CAD tool
   (Fusion, SolidWorks, Onshape, FreeCAD). Print or machine the custom parts from it; the sheet-metal parts and their quotes are in
   [Sheet-metal fabrication](#sheet-metal-fabrication) below.
3. **Build the upstream sub-assemblies** as published:

   | Sub-assembly | Source |
   |---|---|
   | 7-DOF arms | [OpenArm](https://github.com/enactic/openarm_hardware) |
   | 17-DOF hands | [ORCA Hand](https://github.com/orcahand/orcahand_hardware) |
   | Swerve modules | REV MAXSwerve (commercial) |
   | Lift | commercial linear column |

4. **Wire it up**: base carrier PCB in [`../electrical/`](../electrical/), firmware in
   [`../firmware/`](../firmware/).

## Sheet-metal fabrication

Seven custom sheet-metal parts (eight pieces) make up the base and torso structure. Upload each part's
flat pattern from the STEP assembly to a laser-cut sheet-metal service (the quotes below are online
instant quotes; 1.02 is quoted in 5052-H32 aluminium, 0.080 in / 2.0 mm) and select the operations
listed. Prices are USD per piece at each order quantity; the last column is the cost for one robot.

| Ref | Part | Operations | Qty | @1 | @2 | @10 | @50 | @100 | @1000 | Per robot (qty 1) |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 1.02 | Base sheet metal, lower | Laser cutting only - no secondary operations | 1 | $51.75 | $38.05 | $27.59 | $26.39 | $25.98 | $24.54 | $51.75 |
| 1.03 | Base sheet metal, upper | 4 bends + dimple forming + hardware insertion + tapping | 1 | $195.36 | $156.42 | $112.94 | $97.49 | $88.30 | $85.82 | $195.36 |
| 2.02 | Lift-to-torso adapter | 2 bends + dimple forming + hardware insertion + tapping | 1 | $59.26 | $40.69 | $28.93 | $25.15 | $22.42 | $17.99 | $59.26 |
| 2.03 | Torso output plate | 1 bend + hardware insertion + tapping | 1 | $55.16 | $36.62 | $25.70 | $22.77 | $21.87 | $19.29 | $55.16 |
| 2.04 | Body bottom plate | 2 bends + hardware insertion + tapping | 1 | $33.55 | $22.29 | $15.73 | $12.81 | $11.44 | $8.97 | $33.55 |
| 2.06 | Neck mounting plate | 2 bends only | 1 | $29.05 | $19.21 | $13.86 | $10.93 | $9.74 | $7.60 | $29.05 |
| 2.05 | Arm mounting plate | Hardware insertion + tapping | 2 | $13.17 | $13.17 | $9.42 | $7.56 | $6.64 | $5.26 | $26.34 |
| | **Set per robot** | | | **$450.47** | **$339.62** | **$243.59** | **$210.66** | **$193.03** | **$174.73** | **$450.47** |

Source: [`bom/data/machined.csv`](bom/data/machined.csv) — the same numbers feed the volume-pricing
figure and the machined-parts table in [`bom/MABEL_Build_Guide.pdf`](bom/MABEL_Build_Guide.pdf).
Ordering for ten robots instead of one cuts the set from $450.47 to $243.59 per robot.

Per-link meshes of the whole robot are also in
[`../simulation/mabel_mujoco/assets/meshes/`](../simulation/mabel_mujoco/assets/meshes/).
