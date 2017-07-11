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
7. [Resources](resources.md)


## Part IV: Adjoint Simulations (Bonus)

In this final part of the tutorial, we will look at how to run adjoint
simulations. SPECFEM3D_GLOBE supports two types of adjoint simulations: for
source inversions and for finite-frequency kernels. In this tutorial, we will
focus on the application to finite-frequency kernels, but the steps required
are similar for both applications. The steps we need to take are the following: 

* <mark>Run Forward Simulation and Save State Variables</mark>
* Prepare the Adjoint Source(s)
* Run Kernel Simulation

### Run Forward Simulation and Save State Variables
The first step is similar to what we have done in the previous parts of the
tutorial. We need to run a forward simulation and save the save the state
variables at the end of the simulation, such that we can back-propagate the
wavefield in the kernel simulation.

In order to save the state variables, we need to select this option in the
`Par_file` by setting the following option to `.true.`

      SAVE_FORWARD                    = .true.   # save last frame of forward simulation or not

We need the output seismograms to be in `ASCII` format, so we change the
`Par_file` accordingly:

      # output format for the seismograms (one can use either or all of the three formats)
      OUTPUT_SEISMOS_ASCII_TEXT       = .true.
      OUTPUT_SEISMOS_SAC_BINARY       = .false.

Furthermore, to save memory, we will also set the visualization parameters in the `Par_file`
to `.false.` as follows:

      ...

      # save mesh files to check the mesh
      SAVE_MESH_FILES                 = .false.

      ...

      # save AVS or OpenDX movies
      # MOVIE_COARSE saves movie only at corners of elements (SURFACE OR VOLUME)
      # MOVIE_COARSE does not work with create_movie_AVS_DX
      MOVIE_SURFACE                   = .false.

      ...

After we have made these changes to the `Par_file`, we can go ahead and run the
forward simulation by submitting the `submit_solver` script to the job queue by
typing

```shell
      sbatch submit_solver
```

We can then monitor the job with `squeue`, and check the
`OUTPUT_FILES/output_solver.txt` file to make sure that the solver ran
successfully.

---
In this section, we have looked at how to run the solver and save the state
variables that will be used in the kernel simulation.

In the next section we will look at how to prepare the adjoint sources that
will be used in the kernel simulation to back-propagate the wavefield.

[Previous section](/vis_movie.md) -- [Next section](/prepare_adj_source.md)
