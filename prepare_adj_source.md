### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
    1. [Run Forward Simulation and Save State Variables](/run_adj_solver.md)
    2. [Prepare the Adjoint Source(s)](/prepare_adj_source.md)
    3. [Run Kernel Simulation](/run_adj_kernel.md)
7. [Further Work](/further_work.md)
8. [Resources](/resources.md)


## Part IV: Adjoint Simulations (Bonus)

In this final part of the tutorial, we will look at how to run adjoint
simulations. SPECFEM3D_GLOBE supports two types of adjoint simulations: for
source inversions and for finite-frequency kernels. In this tutorial, we will
focus on the application to finite-frequency kernels, but the steps required
are similar for both applications. The steps we need to take are the following: 

* Run Forward Simulation and Save State Variables
* <mark>Prepare the Adjoint Source(s)</mark>
* Run Kernel Simulation

### Prepare the Adjoint Source(s)
After running the forward simulation and saving the state variables in the
first step, we now need to select the stations for which we want to compute the
time-reversed adjoint sources, and prepare them for use in the kernel
simulation.

Choose the stations you want to use from the `DATA/STATIONS` file and copy them
into the `DATA/STATIONS_ADJOINT` file, which uses the same format as the former
file.

For example, in the `DATA/STATIONS` file we have the following list of
available stations:

      AAE        IU        9.0292     38.7656    2442.0     0.0
      AAK        II       42.6390     74.4940    1645.0    30.0
      ABKT       II       37.9304     58.1189     678.0     7.0
      ABPO       II      -19.0180     47.2290    1528.0     5.3
      ADK        IU       51.8823   -176.6842     130.0     0.0
      ...
      XMAS       IU        2.0448   -157.4457      19.0     1.0
      XPF        II       33.6092   -116.4533    1280.0   100.0
      XPFO       II       33.6107   -116.4555    1280.0     0.0
      YAK        IU       62.0310    129.6805     110.0    14.0
      YSS        IU       46.9587    142.7604     148.0     2.0

Say we want to use the `IU.ANMO`, `II.PFO`, and `IU.TUC` stations as adjoint sources
in the kernel simulation. Then, we copy these lines from the `DATA/STATIONS` file and
paste them into the `DATA/STATIONS_ADJOINT` file:

      ANMO       IU       34.9459   -106.4572    1750.0   100.0
      PFO        II       33.6092   -116.4553    1280.0     0.0
      TUC        IU       32.3098   -110.7847     909.0     1.0

Then we need to generate these two adjoint sources by running the
`gen_adj_source.py` script from the root folder. The usage for this script is
as follows

```shell
      python3 gen_adj_source.py [station_file_names]
```

In order to generate the `IU.ANMO`, `II.PFO`, and `IU.TUC` sources, we need to provide the path
to the associated output seismograms

```shell
      python3 gen_adj_source.py ./OUTPUT_FILES/IU.ANMO.BX*.ascii ./OUTPUT_FILES/II.PFO.BX*.ascii ./OUTPUT_FILES/IU.TUC.BX*.ascii
```

**NOTE:** The asterix `*` in the above command is used to include all the
components associated with the station of interest. It is necessary to include
all the component files for the kernel simulation to work.

This script then copies the relevant seismograms, renames them, and stores them
in the `SEM/` folder. To check that the adjoint sources were successfully
generated, inspect this folder to check that there are three component
files associated with each adjoint source. In the example case with the `IU.ANMO`,
`II.PFO`, and `IU.TUC` sources, we expect to see the following files in the `SEM/` folder:

      IU.ANMO.BXE.adj
      IU.ANMO.BXN.adj
      IU.ANMO.BXZ.adj
      II.PFO.BXE.adj
      II.PFO.BXN.adj
      II.PFO.BXZ.adj
      IU.TUC.BXE.adj
      IU.TUC.BXN.adj
      IU.TUC.BXZ.adj

---
In this section, we have looked at how to prepare the adjoint sources that will
be used in the kernel simulation to back-propagate the wavefiled.

In the next section we will complete the final step and run the kernel
simulation.

[Previous section](/run_adj_solver.md) -- [Next section](/run_adj_kernel.md)
