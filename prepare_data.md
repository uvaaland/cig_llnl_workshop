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
3. Set the relevant simulation parameters in the `Par_file`.


* **Step 1:** Provide the source characteristics for the event we want to simulate.

  The format for the source should follow that of the [Global CMT Catalog](http://www.globalcmt.org/).
  For the Napa earthquake, the source CMTSOLUTION is given as follows:

      CMT 2014 08 24 10 20 49.36 38.3100 -122.3800 12.0000 6.1 6.1 C201408241020A
      event name:     C201408241020A
      time shift:      0.0000
      half duration:   0.0000
      latitude:        38.3100
      longitude:       -122.3800
      depth:           12.0000
      Mrr:      -4.760000E+23
      Mtt:      -1.090000E+25
      Mpp:       1.140000E+25
      Mrt:      -1.360000E+24
      Mrp:      -2.500000E+24
      Mtp:       1.120000E+25


* **Step 2:** Check that the compilers have been loaded

```shell
      mpicc --version
      # icc (ICC) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
      
      mpif90 --version
      # ifort (IFORT) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
```

* **Step 3:** Configure SPECFEM3D_GLOBE by running the following command in the root folder (`./specfem3d_globe`):

```shell
      ./configure CC=icc CXX=icpc FC=ifort MPIFC=mpif90
```

