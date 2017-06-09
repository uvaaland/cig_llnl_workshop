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
* Generate a Mesh for the Continental Model
* <mark>Run the Solver</mark>

### Run the Solver

After editing the parameter files and generating the mesh, we are ready to run
the solver itself. Before we do this, we will run through the following
checklist to make sure that we have gone through all the preceeding steps
correctly:

* Edited the parameter files.
* Recompiled the source code if any parameter in the `Par_file` was changed.
* Generated the model mesh and checked the output for success.

If all of these steps have been covered, we can go on to run the solver. The
solver is run with the executable `xspecfem3D` on the cluster. Similar to the
meshing routine, we need to send our job to the cluster's job scheduler. The
script we use for this task is the `submit_solver` script:

```shell
      #!/bin/bash
      
      #SBATCH -N 4
      #SBATCH --ntasks-per-node=16
      #SBATCH -t 01:00:00
      
      # load appropriate compilers/libraries
      module load intel/16.0/64/16.0.4.258
      module load intel-mpi/intel/5.1.3/64
      
      # change directory to build
      cd /tigress/uvaaland/SPECFEM3D_GLOBE/specfem3d_globe
      
      srun -n 64 ./bin/xspecfem3D
```

We submit the job by typing in the command line

```shell
      sbatch submit_solver
```

and we can monitor the job by typing `squeue`.





---

[Previous section](/generate_mesh.md) -- [Next section](/run_solver.md)
