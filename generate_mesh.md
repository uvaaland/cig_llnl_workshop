### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
    1. [Prepare the Data and Paramaters](/prepare_data.md)
    2. [Generate a Mesh for the Continental Model](/generate_mesh.md)
    3. [Run the Solver](/run_solver.md)
5. [Part III: Visualization](/vis_seismo.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
7. [Further Work](/further_work.md)
8. [Resources](/resources.md)


## Part II: Continental-scale Simulations

This second part of the tutorial will take you through the steps that are
needed to run a continental-scale simulation with SPECFEM3D_GLOBE. The steps we
need to take are the following:
* Prepare the Data and Parameters
* <mark>Generate a Mesh for the Continental Model</mark>
* Run the Solver

### Generate a Mesh for the Continental Model

Before we run the solver, we need to generate the mesh for the continental
model.

We do this by running the executable `xmeshfem3D` on the cluster. In order to
do this, we need to send our job to the cluster's job scheduler. The script for
doing this is the `submit_mesher` script, which is written for a SLURM job
scheduler:

```shell
      #!/bin/bash
      
      #SBATCH -N 4
      #SBATCH --ntasks-per-node=36
      #SBATCH -t 00:30:00
      
      # load appropriate compilers/libraries
      module load intel/16.0.4
      
      # change directory to build (e.g. /p/lscratchh/vaaland1/specfem3d_globe/)
      cd path/to/specfem3d_globe
      
      srun -n 144 ./bin/xmeshfem3D
```

**NOTE:** We need to modify this file such that `path/to/specfem3d_globe` is the path to
the current working directory (e.g. `/p/lscratchh/vaaland1/specfem3d_globe/`).

The number of processors is determined by the parameters that we set in the
`Par_file`

      #processors = NPROC_XI * NPROC_ETA * NCHUNKS

which for the `Par_file` on the previous page becomes `8 * 8 * 1 = 64`
processors. In order to submit our job, we type the following in the command line

```shell
      sbatch submit_mesher
```

we can then monitor the job by typing `squeue`.

<p align="center">
  <img src="Fig/chunk_mesh.png" alt="Regional mesh">
</p>


Once the job has finished, the output can be found in the `OUTPUT_FILES/`
folder. We can check to see if the mesher ran successfully by inspecting the
`OUTPUT_FILES/output_mesher.txt` file.

This file contains information about the mesh, including the number of spectral 
elements in the mesh, and the size of the time step that will be used when 
running the solver.

#### Model Resolution

The shortest period that is resolved in the seismograms can be determined by

      shortest period ~ (256 / NEX_XI) * (ANGULAR_WIDTH_XI_IN_DEGREES / 90) * 17

Which for our setup gives us a shortest period of about `(256 / 192) * (45 / 90) * 17 = 11`. That is, the seismograms in this simulation will be accurate down to approximately 11 s periods.

---
In this section, we have looked at how to generate a mesh for the
continental-scale model.

In the next section, we will look at how to run the solver for our
continental-scale simulation.

[Previous section](/prepare_data.md) -- [Next section](/run_solver.md)
