---
layout: default
---

### Table of Contents
1. [Motivation](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Getting Started](/getting_started.md)
    1. [Obtain the Source Code](#source_code)
    2. [Configure](#configuration)
    3. [Compile](#compilation)
    4. [Prepare the Input](#prepare_input)
4. [Meshing](/mesh.md)
5. [Solving](/solve.md)
6. [Example](/example.md)

# Getting Started

### Obtain the Source Code <a name="source_code"></a>

* **In general:**
  * The current stable release can be downloaded as a **tar.gz** file at:
  https://geodynamics.org/cig/software/specfem3d_globe/

  * To get the development code, clone the github repository:

        git clone --recursive --branch devel https://github.com/geodynamics/specfem3d_globe.git
    


* **For this workshop:**
  * Clone the following github repository:
  
        git clone https://github.com/uvaaland/specfem3d_globe.git



### Configure <a name="configuration"></a>
In order to generate the `Makefile`s, we need to configure SPECFEM3D_GLOBE. Here, we will configure it using the `Intel compilers`:

* **Step 1:** Load the `Intel compilers` by typing the following in the command line

      module load intel/16.0/64/16.0.4.258 intel-mpi/intel/5.1.3/64 
  
* **Step 2:** Check that the compilers have been loaded

      mpicc --version
      # icc (ICC) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
      
      mpif90 --version
      # ifort (IFORT) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.


* **Step 3:** Configure SPECFEM3D_GLOBE by running the following command in the repository's root folder (`./specfem3d_globe`)

      ./configure CC=mpicc FC=mpif90

### Compile <a name="compilation"></a>
After configuration, we can compile the source code by typing `make` in the repository's root folder. The resulting binary files can be found in the `./specfem3d_globe/bin` folder.


## Prepare the Input Files <a name="prepare_input"></a>
* **CMTSOLUTION**
* **STATIONS**
* **Par_file**
