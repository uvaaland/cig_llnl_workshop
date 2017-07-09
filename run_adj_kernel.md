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

