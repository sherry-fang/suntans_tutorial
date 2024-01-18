# 2d version of the constant buoyancy flux base case simulation

2D model domain with a constant sloping bottom shelf/ridge topography, linear vertical temperature (density) stratification without tidal forcing (barotropic tide) at one open offshore and one closed coast boundary. The instability is eliminated in this 2d model. This model is the 2d version of the NWS representative case. 

## Notes on periodic grid generation

The grid generation code is in `mfiles/quadgrid.m`. You will need either MATLAB or Octave to run this code. On linux Octave is install via `sudo apt install octave` 

Modify the script to change the grid resolution.

Also note that this example has its own `grid.c` file that calculates geometry variables appropriately for a periodic domain.

Noted that this 2D model is quasi-2d which has 3 grid point in the y- axis (along-shelf direction).

## Set up for the constant net heat loss

set the `metmodel==3` to ensure the model has a uniformly constant net heat flux applied throughout the entire simulation. (here we set

```
        met->Hl[i] = -100.; // contant
	met->Hlw[i] = 0.;
	met->Hs[i] = 0.;
	met->Hsw[i] = 0.;'
```

---
Sherry

UWA, Jan 2024
