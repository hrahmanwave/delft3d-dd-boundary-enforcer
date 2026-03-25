# Delft3D DD Boundary Enforcer

A browser-based tool for enforcing identical bathymetry depths at **domain decomposition (DD) interface cells** in Delft3D models. Eliminates depth mismatches at DD boundaries that cause numerical instabilities, Courant exceedances, and UZD non-convergence.

## The Problem

In Delft3D domain decomposition setups, the inner and outer domain depth files (`.dep`) are often generated independently (e.g., from different DEM sources or QUICKIN sessions). This results in **depth discontinuities at DD interface cells**, which can cause:

- Velocity blow-up at the interface
- Courant number exceedances
- UZD solver non-convergence
- Segmentation faults during simulation

## The Solution

This tool reads a **master XYZ bathymetry file** (the authoritative depth source) and two Delft3D `.dep` files, then:

1. Identifies interface cells along the specified domain edges
2. Interpolates depths from the master XYZ to each interface cell using **IDW** or **nearest-neighbor** interpolation
3. Applies a configurable **blend zone** (Schwarz overlap transition) to smoothly transition from enforced depths back to original grid depths
4. Exports corrected `.dep` files ready for Delft3D

## Features

- **Two interpolation methods**: Inverse Distance Weighting (IDW) with configurable power, and Nearest Neighbor
- **Blend zone**: Configurable transition width matching Delft3D's Schwarz overlap, with linear blending from enforced to original depths
- **Edge selection**: Interface on any edge (east/west/north/south) for each domain
- **Live log**: Step-by-step processing log with statistics
- **Preview table**: Sortable view of all modified cells with original vs. enforced depths and Δ values
- **Direct download**: Corrected `.dep` files in Delft3D-compatible format
- **Zero installation**: Runs entirely in the browser — no Python, no server, no dependencies

## How to Use

1. Open `dd_boundary_enforcer.html` in any modern browser
2. Upload your **master XYZ bathymetry file** (space/tab-delimited X Y Z)
3. Upload **Domain 1** and **Domain 2** `.dep` files
4. Configure parameters:
   - Interpolation method (IDW or nearest neighbor)
   - IDW power (default: 2)
   - Search radius in grid cells
   - Blend zone width (Schwarz overlap cells)
   - Interface edge for each domain
5. Click **Enforce Boundary Depths**
6. Review the log and preview table
7. Download corrected `.dep` files

## Parameters

| Parameter | Default | Description |
|---|---|---|
| Method | IDW | Interpolation algorithm |
| IDW Power | 2 | Distance weighting exponent (higher = sharper falloff) |
| Search Radius | 10 cells | Maximum search distance for master XYZ points |
| Blend Width | 3 cells | Schwarz overlap transition zone (0 = hard edge) |
| Domain Edge | East / West | Which edge of each domain is the DD interface |

## Input File Formats

### Master XYZ
Plain text, space/tab/comma-delimited, one point per line:
```
588000.0  2420000.0  -3.450
588010.0  2420000.0  -3.512
588020.0  2420000.0  -3.601
```

### Delft3D .dep
Standard Delft3D depth file — space-separated depth values, row by row. As produced by QUICKIN or Delft3D-RGFGRID.

## Context

Developed for coastal hydrodynamic modeling of the **Gabura/Rangabali region, Bangladesh**, as part of storm surge simulation research at the **Institute of Water and Flood Management (IWFM), BUET**. Tested with domain decomposition setups including GBU_INT_6 (705×705 inner domain) and GBU_EXT outer domain configurations.

## License

MIT License — see [LICENSE](LICENSE).

## Author

[Hasan Rahman](https://github.com/hrahmanwave) — IWFM, BUET, Bangladesh
