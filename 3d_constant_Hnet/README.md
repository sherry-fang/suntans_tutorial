#  Constant buoyancy flux base case simulation (representing idealised NWS)

## bathymetry and resolution
- alongshore uniform and consisted of a constant sloping bottom at the coast, followed by a flat bottom extending offshore
- 300x250x40 grid size of domain with 1 km horizontal resolution and ~ 5.5 m vertical resolution


## boundary condition
- periodic boundary condition in the along-shelf direction
- open offshore
- close coast 

## constant net heat loss

set the `metmodel==3` in the `met.c` to ensure the model has a uniformly constant net heat flux applied throughout the entire simulation. 

```
met->Hl[i] = -100.; // contant
met->Hlw[i] = 0.;
met->Hs[i] = 0.;
met->Hsw[i] = 0.;'
```
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
