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

* Run Forward Simulation and Save State Variables
* Prepare the Adjoint Source(s)
* <mark>Run Kernel Simulation</mark>

### Run Kernel Simulation
Once we have run the forward simulation and generated the adjoint sources,
running the kernel simulation is straight forward. In the `Par_file` we need to
change two parameters. First, we don't want to save the state variables, so we
set the `SAVE_FORWARD` parameter to `.false.` again.

      SAVE_FORWARD                    = .false.   # save last frame of forward simulation or not

Secondly, we need to change the simulation type. We want to run a kernel
simulation, and therefore we need to set the `SIMULATION_TYPE` parameter
accordingly

      SIMULATION_TYPE                 = 3   # set to 1 for forward simulations, 2 for adjoint simulations for sources, and 3 for kernel simulations

Once we have made these modifications to the `Par_file`, we can submit the
`submit_solver` script to the job queue with the following command

```shell
      sbatch submit_solver
```

and monitor the progress with the `squeue` command. Once the simulation ends,
we check the `OUTPUT_FILES/output_solver.txt` file to make sure that the solver
ran successfully.

For details on how to visualize the output from the kernel simulations, and
instructions on how to run adjoint simulations for sources, please consult the
SPECFEM3D_GLOBE [manual](https://specfem3d-globe.readthedocs.io/en/latest/06_adjoint_simulations/).
