---
layout: default
---

### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
7. [Resources](resources.md)


## Part I: Setting up SPECFEM3D_GLOBE

In the first part of the tutorial, we will go through the three steps that are
needed to set up SPECFEM3D_GLOBE:
* Obtain the Source Code
* Configuration
* Compilation

### Obtain the Source Code <a name="source_code"></a>

For this workshop we will get the source code by cloning this [GitHub repository](https://github.com/uvaaland/specfem3d_globe):

```shell
      git clone https://github.com/uvaaland/specfem3d_globe.git
```

In general, the current, stable release of SPECFEM3D_GLOBE can be downloaded at
the CIG website, while the development code is available on GitHub:
* [Stable release](https://geodynamics.org/cig/software/specfem3d_globe/)
* [Development code](https://github.com/geodynamics/specfem3d_globe)


#### File Structure
Now that we have downloaded the source code, we will take a look at what's
inside. The repository includes a whole range of files that serve different
purposes, but the key files and folders that are relevant to this tutorial are
highlighted in the following tree-structure:


```
      ./specfem3d_globe
      +-- DATA/
      |   +-- STATIONS
      |   +-- STATIONS_ADJOINT
      |   +-- CMTSOLUTION
      |   +-- Par_file
      +-- OUTPUT_FILES/
      +-- DATABASES_MPI/
      +-- SEM/
      +-- combine_data.py
      +-- gen_adj_source.py
      +-- seisplot.py
```

#### Explanation
* **DATA/:**  Folder that holds all the parameter files that are used for running the simulation

  * STATIONS: Contains the names and locations of all the stations
  * STATIONS_ADJOINT: Contains the names and locations of all the stations used as adjoint sources
  * CMTSOLUTION: Contains the source characteristics
  * Par_file: Contains the simulation parameters

* **OUTPUT_FILES/:** Folder where the output seismograms are stored
* **DATABASES_MPI/:** Folder where the mesh partitions are stored
* **SEM/:** Folder where the adjoint sources are generated
* combine_data.py: script for combining volumetric data files
* gen_adj_source.py: script for generating adjoint sources
* seisplot.py: script for plotting seismograms using ObsPy

### Configuration
In order to generate the `Makefile`, we need to configure SPECFEM3D_GLOBE. We
will configure it using `Intel compilers`. Refer to the manual for
configuration with other compilers.

* **Step 1:** Load the `Intel compilers` by typing the following in the command line

```shell
      module load intel/16.0/64/16.0.4.258 intel-mpi/intel/5.1.3/64 
```

* **Step 2:** Check that the compilers have been loaded

```shell
      mpicc --version
      # icc (ICC) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
      
      mpif90 --version
      # ifort (IFORT) 16.0.4 20160811
      # Copyright (C) 1985-2016 Intel Corporation.  All rights reserved.
```

* **Step 3:** Configure SPECFEM3D_GLOBE by running the following command in the root folder (`specfem3d_globe/`):

```shell
      ./configure CC=icc CXX=icpc FC=ifort MPIFC=mpif90
```

### Compilation
Once we have configured SPECFEM3D_GLOBE, we can compile the source code by
typing `make all` in the root directory. This will produce all the binary files
that we will use in the remaining parts of this tutorial. The resulting binary
files can be found in the `bin/` folder.

**NOTE:** The solver executable `xspecfem3D` uses static allocations which will
depend upon the parameters set in the `Par_file`. This means that if you change any
parameter in the `Par_file` after compiling SPECFEM3D_GLOBE, you should
recompile the code. Recompile the code by running `make clean` and
`make` in the root folder.

---
In this section we have looked at how to set up, configure, and compile
SPECFEM3D_GLOBE.

In the next section we move on to **Part II** of the tutorial, and
look at how to prepare the input data for the continental-scale simulation.

[Previous section](/intro_specfem.md) -- [Next section](/prepare_data.md)
