### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
    1. [Prepare the Data and Paramaters](/prepare_data.md)
    2. [Generate a Mesh for the Continental Model](/generate_mesh.md)
    3. [Run the Solver](/run_solver.md)
5. [Part III: Additional Topics](/partIII.md)
6. [Resources](resources.md)


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

We do this by running the executable `xmeshfem3E` on the cluster. In order to
do this, we need to send our job to the cluster job scheduler. The script for
doing this is the `submit_mesher` script, which is written for a SLURM job
scheduler:

```shell
      #!/bin/bash
      
      #SBATCH -N 4
      #SBATCH --ntasks-per-node=16
      #SBATCH -t 00:30:00
      
      # load appropriate compilers/libraries
      module load intel/16.0/64/16.0.4.258
      module load intel-mpi/intel/5.1.3/64
      
      # change directory to build
      cd /tigress/uvaaland/SPECFEM3D_GLOBE/specfem3d_globe
      
      srun -n 64 ./bin/xmeshfem3D
```

In order to submit your job, type the following in the command line

```shell
      sbatch submit_mesher
```













---
In the next section, we will look at how to run the solver for our continental
simulation.

[Previous section](/prepare_data.md) -- [Next section](/generate_mesh.md)
