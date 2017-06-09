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
  For the Napa earthquake, the source `CMTSOLUTION` is given as follows:

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

  For the Napa earthquake, the `STATIONS` file has XXX number of stations:

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


