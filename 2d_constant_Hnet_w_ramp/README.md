# 2d version of the constant buoyancy flux base case simulation with ramp factor considered

Based on the example model run of `2d_constant_Hnet`, this example considered applying the ramp factor in the quasi-2d simulation.

## Notes on periodic grid generation

The grid generation code is in `mfiles/quadgrid.m`. You will need either MATLAB or Octave to run this code. On linux Octave is install via `sudo apt install octave` 

Modify the script to change the grid resolution.

Also note that this example has its own `grid.c` file that calculates geometry variables appropriately for a periodic domain.

Noted that this 2D model is quasi-2d which has 3 grid point in the y- axis (along-shelf direction).

## Set up for the constant net heat loss

set the `metmodel==3` in the `met.c` to ensure the model has a uniformly constant net heat flux applied throughout the entire simulation. 

```
met->Hl[i] = -100.0*rampfac; // contant
met->Hlw[i] = 0.;
met->Hs[i] = 0.;
met->Hsw[i] = 0.;'
```

where the `rampfac` was set in the `boundaries.c`. need to point the location of rampfac carefully to make SUNTANS running.
## State equation

In this example, the change of density is primarily based on the temperature. Though the salinity is still in the state equation (check `state.c`), but we set salinity as a constant (check `scripts
/make_scenario_tidalfront.py`)
```
 # Velocity boundary
bnd.boundary_S[:,k,ii] = S0
```

---
Sherry

UWA, Jan 2024
