### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
    1. [Prepare the Data and Paramaters](/prepare_data.md)
    2. [Generate a Mesh for the Continental Model](/generate_mesh.md)
    3. [Run the Solver](/run_solver.md)
5. [Part III: Visualization](/vis_seismo.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
7. [Further Work](/further_work.md)
8. [Resources](/resources.md)


## Part II: Continental-scale Simulations

This second part of the tutorial will take you through the steps that are
needed to run a continental-scale simulation with SPECFEM3D_GLOBE. The steps we
need to take are the following:
* <mark>Prepare the Data and Parameters</mark>
* Generate a Mesh for the Continental Model
* Run the Solver

### Prepare the Data and Parameters

As we talked about in the previous part of the tutorial, the parameter files
for the SPECFEM3D_GLOBE package are found in the `DATA/` folder. In order to
set up the simulation, we need to:

1. Provide the source characteristics for the event we want to simulate
2. Provide names and locations for the stations we want to use
3. Set the relevant simulation parameters in the `Par_file`


* **Step 1: Provide the source characteristics for the event we want to simulate**

  The format for the source should follow that of the [Global CMT Catalog](http://www.globalcmt.org/).
  For the South Napa earthquake, the source `CMTSOLUTION` is given as follows:

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


* **Step 2: Provide the names and locations for the stations we want to use**

  The recording stations are given in the `STATIONS` file, using the following
  format:

      Station    Network    Latitude(degrees)    Longitude(degrees)    Elevation(m)    Burial(m)

  For the South Napa earthquake, the `STATIONS` file has 167 stations from the
  Global Seismographic Network (GSN):

      AAE        IU        9.0292     38.7656    2442.0     0.0
      AAK        II       42.6390     74.4940    1645.0    30.0
      ABKT       II       37.9304     58.1189     678.0     7.0
      ABPO       II      -19.0180     47.2290    1528.0     5.3
      ADK        IU       51.8823   -176.6842     130.0     0.0
      ...
      XMAS       IU        2.0448   -157.4457      19.0     1.0
      XPF        II       33.6092   -116.4533    1280.0   100.0
      XPFO       II       33.6107   -116.4555    1280.0     0.0
      YAK        IU       62.0310    129.6805     110.0    14.0
      YSS        IU       46.9587    142.7604     148.0     2.0

  More station information can be found on the [FDSN webpage](http://www.fdsn.org/).

* **Step 3: Set the relevant simulation parameters in the `Par_file`**

  The `Par_file` is the file where most of the simulation parameters are set.
  In this tutorial, we will only work with the subset of parameters that is
  shown below. For a full description of all the parameters in the `Par_file`,
  please consult the [SPECFEM3D_GLOBE manual](http://specfem3d-globe.readthedocs.io/en/latest/).

      # forward or adjoint simulation
      SIMULATION_TYPE                 = 1   # set to 1 for forward simulations, 2 for adjoint simulations for sources, and 3 for kernel simulations
      NOISE_TOMOGRAPHY                = 0   # flag of noise tomography, three steps (1,2,3). If earthquake simulation, set it to 0.
      SAVE_FORWARD                    = .false.   # save last frame of forward simulation or not
      
      # number of chunks (1,2,3 or 6)
      NCHUNKS                         = 1
      
      # angular width of the first chunk (not used if full sphere with six chunks)
      ANGULAR_WIDTH_XI_IN_DEGREES     = 45.d0   # angular size of a chunk
      ANGULAR_WIDTH_ETA_IN_DEGREES    = 45.d0
      CENTER_LATITUDE_IN_DEGREES      = 40.d0
      CENTER_LONGITUDE_IN_DEGREES     = -120.d0
      GAMMA_ROTATION_AZIMUTH          = 0.d0
      
      # number of elements at the surface along the two sides of the first chunk
      # (must be multiple of 16 and 8 * multiple of NPROC below)
      NEX_XI                          = 192
      NEX_ETA                         = 192
      
      # number of MPI processors along the two sides of the first chunk
      NPROC_XI                        = 12
      NPROC_ETA                       = 12

      ...

      # 3D model
      MODEL                           = s362ani

      # parameters describing the Earth model
      OCEANS                          = .true.
      ELLIPTICITY                     = .true.
      TOPOGRAPHY                      = .true.
      GRAVITY                         = .true.
      ROTATION                        = .true.
      ATTENUATION                     = .true.

      # absorbing boundary conditions for a regional simulation
      ABSORBING_CONDITIONS            = .true.

      # record length in minutes
      RECORD_LENGTH_IN_MINUTES        = 10.0d0

      ...

      # path to store the local database files on each node
      LOCAL_PATH                      = ./DATABASES_MPI
     
      ...

      # output format for the seismograms (one can use either or all of the three formats)
      OUTPUT_SEISMOS_ASCII_TEXT       = .false.
      OUTPUT_SEISMOS_SAC_BINARY       = .true.

      ...

  We will leave the `Par_file` as it is for now, and use this setup to generate
  the model mesh and run a simulation of the South Napa earthquake.

**NOTE:** As mentioned in the previous section, if you make any changes to the
`Par_file` after compiling SPECFEM3D_GLOBE, you need to recompile the package by
running `make clean` and `make all` in the root folder.

---
In this section, we have looked at how to provide the input data that is
necessary to run a continental-scale simulation with SPECFEM3D_GLOBE.

In the next section, we will look at how to generate a mesh for the
continental-scale model.

[Previous section](/setup_specfem3d.md) -- [Next section](/generate_mesh.md)
