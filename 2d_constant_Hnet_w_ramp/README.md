# 2d version of the constant buoyancy flux base case simulation with ramp factor considered

Based on the example model run of `2d_constant_Hnet`, this example considered applying the ramp factor in the quasi-2d simulation.

## Set up for the constant net heat loss

set the `metmodel==3` in the `met.c` to ensure the model has a uniformly constant net heat flux applied throughout the entire simulation. 

```
met->Hl[i] = -100.0*rampfac; // contant
met->Hlw[i] = 0.;
met->Hs[i] = 0.;
met->Hsw[i] = 0.;'
```

where the `rampfac` was set in the `boundaries.c`. need to point the location of rampfac carefully to make SUNTANS running.

