This is a brief introduction on how to setup and run the SPECFEM3D_GLOBE
software package. More information can be found in the SPECFEM3D_GLOBE manual:

* [PDF version](https://geodynamics.org/cig/software/specfem3d_globe/specfem3d_globe-manual.pdf)
* [HTML version](http://specfem3d-globe.readthedocs.io/en/latest/)



## Table of Contents
1. [Getting Started with SPECFEM3D_GLOBE](#getting_started)
    1. [Obtain the Source Code](#source_code)
    2. [Configure](#configuration)
    3. [Compile](#compilation)
2. [Prepare the Input Files](#input)



## Getting Started with SPECFEM3D_GLOBE <a name="getting_started"></a>


### Obtain the Source Code <a name="source_code"></a>
* **For this workshop:**
  * Clone the following GitHub repository by running:

        git clone https://github.com/uvaaland/specfem3d_globe.git


* **In general:**
  * The current, stable release can be downloaded as a **tar.gz** file at:
  https://geodynamics.org/cig/software/specfem3d_globe/ 

  * To get the development code, clone the GitHub repository:

        git clone --recursive --branch devel https://github.com/geodynamics/specfem3d_globe.git


### Configure <a name="configuration"></a>
In order to generate the `Makefile`, we need to configure SPECFEM3D_GLOBE.
Here, we will configure using the `Intel compilers`:

**Step 1:** Load the `Intel compilers` by typing the following in the command
line

      module load intel/16.0/64/16.0.4.258 intel-mpi/intel/5.1.3/64

**Step 2:** Check that the compilers have been loaded

      mpicc --version
      # icc (ICC) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
      
      mpif90 --version
      # ifort (IFORT) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.

**Step 3:** Configure SPECFEM3D_GLOBE by running the following command in the
repository's root folder (`./specfem3d_globe`)

      ./configure CC=mpicc CXX=icpc FC=ifort MPIFC=mpif90


### Compile <a name="compilation"></a>
After configuration, we can compile the source code my typing `make all` in the
repository's root folder. The resulting binary files can be found in the
`./specfem3d_globe/bin` folder.



## Prepare the Input Files <a name="input"></a>
**CMTSOLUTION**
**STATIONS**
**Par_file**
