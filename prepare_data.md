### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
    1. [Prepare the Data and Paramaters](/prepare_data.md)
    2. [Meshing the Model](/generate_mesh.md)
    3. [Running the Solver](/run_solver.md)
5. [Part III: Additional Topics](/partIII.md)
6. [Resources](resources.md)


## Part II: Continental-scale Simulations

This second part of the tutorial will take you through the steps that are
needed to run a continental-scale simulation with SPECFEM3D_GLOBE. The steps we
need to take are the following:
* Prepare the Data and Parameters
* Generate a Mesh for the Continental Model
* Run the Solver

### Prepare the Data and Parameters

As we talked about in the previous part of the tutorial, the parameter files
for the SPECFEM3D_GLOBE package are found in the `DATA/` folder. In order to
set up the simulation to our liking, we need to:

    1. Provide the source characteristics for the event we want to simulate.
    2. Provide names and locations for the recording stations that we want to use.
    3. Set the relevant simulation parameters in the `Par_file`


