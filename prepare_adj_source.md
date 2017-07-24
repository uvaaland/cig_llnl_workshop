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

      A22        GY       37.9293     58.1125     662.9    21.8
      AAE        IU        9.0292     38.7656    2442.0     0.0
      AAUS       AF        9.0349     38.7665    2437.8     0.0
      ABKAR      KZ       49.2558     59.9431     362.0     0.0
      ABKT       II       37.9304     58.1189     678.0     7.0
      ...
      WLF        GE       49.6646      6.1526     295.0     0.0
      YNDE       AF        3.8700     11.4560     717.0     0.0
      ZKR        GE       35.1147     26.2170     270.0     0.0
      ZRNK       KZ       52.9510     69.0043     380.0     0.0
      ZRN        KZ       52.9510     69.0043     420.0     0.0

Say we want to use the `AZ.BZN`, `BK.CVS`, and `CI.VOG` stations as adjoint sources
in the kernel simulation. Then, we copy these lines from the `DATA/STATIONS` file and
paste them into the `DATA/STATIONS_ADJOINT` file:

      CVS        BK       38.3453   -122.4584     295.1    23.2
      VOG        CI       36.3210   -119.3823      90.0     0.0
      BZN        AZ       33.4915   -116.6670    1301.0     0.0

Then we need to generate these two adjoint sources by running the
`gen_adj_source.py` script from the root folder. The usage for this script is
as follows

```shell
      python3 gen_adj_source.py [station_file_names]
```

In order to generate the `AZ.BZN`, `BK.CVS`, and `CI.VOG` sources, we need to provide the path
to the associated output seismograms

```shell
      python3 gen_adj_source.py ./OUTPUT_FILES/AZ.BZN.BX*.ascii ./OUTPUT_FILES/BK.CVS.BX*.ascii ./OUTPUT_FILES/CI.VOG.BX*.ascii
```

**NOTE:** The asterix `*` in the above command is used to include all the
components associated with the station of interest. It is necessary to include
all the component files for the kernel simulation to work.

This script then copies the relevant seismograms, renames them, and stores them
in the `SEM/` folder. To check that the adjoint sources were successfully
generated, inspect this folder to check that there are three component
files associated with each adjoint source. In the example case with the `AZ.BZN`,
`BK.CVS`, and `CI.VOG` sources, we expect to see the following files in the `SEM/` folder:

      AZ.BZN.BXE.adj
      AZ.BZN.BXN.adj
      AZ.BZN.BXZ.adj
      BK.CVS.BXE.adj
      BK.CVS.BXN.adj
      BK.CVS.BXZ.adj
      CI.VOG.BXE.adj
      CI.VOG.BXN.adj
      CI.VOG.BXZ.adj

---
In this section, we have looked at how to prepare the adjoint sources that will
be used in the kernel simulation to back-propagate the wavefiled.

In the next section we will complete the final step and run the kernel
simulation.

[Previous section](/run_adj_solver.md) -- [Next section](/run_adj_kernel.md)
