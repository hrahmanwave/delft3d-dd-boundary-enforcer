## DD Boundary Enforcer v1.0.0

Browser-based tool for enforcing identical bathymetry depths at Delft3D domain decomposition (DD) interface cells.

### Features
- IDW and nearest-neighbor interpolation from master XYZ bathymetry
- Configurable Schwarz overlap blend zone for smooth depth transitions
- Interface edge selection (N/S/E/W) for each domain
- Live processing log with modification statistics
- Preview table showing all modified cells with Δ values
- Direct download of corrected `.dep` files in Delft3D format
- Zero installation — runs entirely in the browser

### Usage
Open `dd_boundary_enforcer.html` in any browser → upload master XYZ + two `.dep` files → configure parameters → enforce → download corrected files.

### Context
Developed for coastal storm surge modeling (Gabura/Rangabali, Bangladesh) at IWFM, BUET.
