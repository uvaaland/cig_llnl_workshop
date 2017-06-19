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
* <mark>Prepare the Data and Parameters</mark>
* Generate a Mesh for the Continental Model
* Run the Solver

### Prepare the Data and Parameters

As we talked about in the previous part of the tutorial, the parameter files
for the SPECFEM3D_GLOBE package are found in the `DATA/` folder. In order to
set up the simulation, we need to:

1. Provide the source characteristics for the event we want to simulate.
2. Provide names and locations for the recording stations that we want to use.
3. Set the relevant simulation parameters in the `Par_file`.


* **Step 1:** Provide the source characteristics for the event we want to simulate.

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


* **Step 2:** Provide the names and locations for the recording stations that
  we want to use.

  The recording stations are given in the `STATIONS` file, using the following
  format:

      Station    Network    Latitude(degrees)    Longitude(degrees)    Elevation(m)    Burial(m)

  For the South Napa earthquake, the `STATIONS` file has X number of stations:

      034A       TA       27.0647    -98.6833     155.0     0.0
      035A       TA       26.9379    -98.1023      29.0     0.0
      035Z       TA       26.4630    -98.0683      19.0     0.0
      058A       TA       27.0569    -81.8049      15.0     0.0
      059A       TA       26.9671    -81.1440      11.0     0.0
      059Z       TA       26.3373    -81.4432       8.0     0.0
      060A       TA       27.0361    -80.3618       9.0     0.0
      060Z       TA       26.4062    -80.5560       9.0     0.0
      061Z       TA       25.8657    -80.9070       9.0     0.0
      062Z       TA       24.7266    -81.0523       5.0     0.0
      109C       TA       32.8889   -117.1051     150.0     0.0
      112A       TA       32.5356   -114.5804      87.0     0.0
      113A       AR       32.7683   -113.7667     118.0     0.0
      113A       TA       32.7683   -113.7667     118.0     0.0
      ...
      Z53A       TA       33.2801    -83.5713     144.0     0.0
      Z54A       TA       33.2362    -82.8417     134.0     0.0
      Z55A       TA       33.2211    -82.1359     100.0     0.0
      Z56A       TA       33.3253    -81.3687      81.0     0.0
      Z57A       TA       33.2970    -80.7039      81.0     0.0
      Z58A       TA       33.3349    -79.8129      18.0     0.0
      Z59A       TA       33.2414    -79.2780       8.0     0.0
      ZAIG       MX       22.7692   -102.5670    2408.0     0.0
      ZAR        CM        7.4923    -74.8580     205.0     0.0
      ZKR        GE       35.1147     26.2170     270.0     0.0
      ZOMB       AF      -15.3833     35.3500     885.0     0.0
      ZRNK       KZ       52.9510     69.0043     380.0     0.0
      ZRN        KZ       52.9510     69.0043     420.0     0.0

* **Step 3:** Set the relevant simulation parameters in the `Par_file`.

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
      ANGULAR_WIDTH_XI_IN_DEGREES     = 90.d0   # angular size of a chunk
      ANGULAR_WIDTH_ETA_IN_DEGREES    = 90.d0
      CENTER_LATITUDE_IN_DEGREES      = 40.d0
      CENTER_LONGITUDE_IN_DEGREES     = 10.d0
      GAMMA_ROTATION_AZIMUTH          = 20.d0
      
      # number of elements at the surface along the two sides of the first chunk
      # (must be multiple of 16 and 8 * multiple of NPROC below)
      NEX_XI                          = 128
      NEX_ETA                         = 128
      
      # number of MPI processors along the two sides of the first chunk
      NPROC_XI                        = 8
      NPROC_ETA                       = 8

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
      RECORD_LENGTH_IN_MINUTES        = 25.0d0

      ...

      # path to store the local database files on each node
      LOCAL_PATH                      = ./DATABASES_MPI
     
      ...

      # output format for the seismograms (one can use either or all of the three formats)
      OUTPUT_SEISMOS_SAC_BINARY       = .true.

      ...

  We will leave the `Par_file` as it is for now, and use this setup to generate
  the model mesh and run a simulation of the South Napa earthquake.

**NOTE:** As mentioned in the previous section, if you make any changes to the
`Par_file` after compiling SPECFEM3D_GLOBE, you need to recompile the package by
running `make clean` and `make` in the root folder.

---
In this section, we have looked at how to provide the input data that is
necessary to run a continental-scale simulation with SPECFEM3D_GLOBE.

In the next section, we will look at how to generate a mesh for the
continental-scale model.

[Previous section](/setup_specfem3d.md) -- [Next section](/generate_mesh.md)
