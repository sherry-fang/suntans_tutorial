# 2d version of the constant buoyancy flux base case simulation

Based on the example model run of `2d_constant_Hnet`, this simulation try to run the model in a real 2d grid (instead of quasi 2d having 3 grid point in the along-shelf direction).

## Notes on periodic grid generation

The grid generation code is in `mfiles/quadgrid.m`. You will need either MATLAB or Octave to run this code. On linux Octave is install via `sudo apt install octave`

Modify the script to change the grid resolution.

Also note that this example has its own `grid.c` file that calculates geometry variables appropriately for a periodic domain.

This simulation will use grid size of `P300x1`

---

