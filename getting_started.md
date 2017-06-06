---
layout: default
---

### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/getting_started.md)
4. [Part II: Regional Simulation](/prep_data.md)
5. [Part III: Additional Topics](/partIII.md)
6. [Resources](resources.md)


## Part I: Setting up SPECFEM3D_GLOBE

In the first part of the tutorial, we will go through the three steps that are
needed to set up SPECFEM3D_GLOBE:
* Obtain the Source Code
* Configuration
* Compilation

### Obtain the Source Code <a name="source_code"></a>

For this workshop we will get the source code by cloning this [GitHub repository](https://github.com/uvaaland/specfem3d):

      git clone https://github.com/uvaaland/specfem3d_globe.git

In general, the current, stable release of SPECFEM3D_GLOBE can be downloaded at
the CIG website, while the development code can be obtained by cloning the
GitHub repository:
* [Stable release](https://geodynamics.org/cig/software/specfem3d_globe/)
* [Development code](https://github.com/geodynamics/specfem3d_globe)


### Configuration
In order to generate the `Makefile`, we need to configure SPECFEM3D_GLOBE. We
will configure it using `Intel compilers`. Refer to the manual for
configuration with other compilers.

* **Step 1:** Load the `Intel compilers` by typing the following in the command line

      module load intel/16.0/64/16.0.4.258 intel-mpi/intel/5.1.3/64 
  
* **Step 2:** Check that the compilers have been loaded

      mpicc --version
      # icc (ICC) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
      
      mpif90 --version
      # ifort (IFORT) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.


* **Step 3:** Configure SPECFEM3D_GLOBE by running the following command in the root folder (`./specfem3d_globe`):

      ./configure CC=icc CXX=icpc FC=ifort MPIFC=mpif90


### Compilation
Once we have configured SPECFEM3D_GLOBE, we can compile the source code by
typing `make all` in the root directory. This will produce all the binary files
that we will use in the remaining parts of this tutorial. The resulting binary
files can be found in the `./specfem3d_globe/bin` folder.

---
In this section we have looked at how to set up, configure, and compile
SPECFEM3D_GLOBE. In the next section we move on to **Part II** of the tutorial, and
will look at how to prepare the input data for the regional simulation.

[Previous section](/intro_specfem.md) -- [Next section](/getting_started.md)
