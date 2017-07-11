### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
    1. [Visualize Seismograms](/vis_seismo.md)
    2. [Visualize Model Mesh](/vis_mesh.md)
    3. [Visualize Surface Movie](/vis_movie.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
7. [Resources](resources.md)


## Part III: Visualization

In this third part of the tutorial, we will look at methods for visualizing the
output simulation data. We will look at the following categories:

* Visualize Seismograms
* Visualize Model Mesh
* <mark>Visualize Surface Movie</mark>

### Visualize Surface Movie

In order to create a surface movie for the simulation, we need to go through a
couple of steps that are similar to what we did for visualizing the model mesh.

First, we need to modify the `Par_file` such that the movie data are being
saved. Therefore, open up `DATA/Par_file` and set the following parameter to
`.true.`:

      ...

      # save AVS or OpenDX movies
      # MOVIE_COARSE saves movie only at corners of elements (SURFACE OR VOLUME)
      # MOVIE_COARSE does not work with create_movie_AVS_DX
      MOVIE_SURFACE                   = .true.

      ...

Once this is done, we need to go through the following three steps in order to
visualize the surface movie:

1. Rerun the solver routine
2. Generate the movie data
3. Visualize using Paraview

* **Step 1: Rerun the solver routine**

  This step is the same as what we did in Part II. We run the `xspecfem3D`
  executable on the cluster by submitting the `submit_solver` script:

```shell
      sbatch submit_solver
```
  And use `squeue` to monitor the job. Once the job finishes, we can check the
  `OUTPUT_FILES/output_solver.txt` file to make sure that the solver ran
  successfully, and then we can move on to the next step.

* **Step 2: Generate the movie data**

  The surface movie data files are stored in the
  `OUTPUT_FILES/` folder as `moviedata*`. In order to visualize the surface 
  movie in `Paraview`, we need to convert these datafiles to a format that 
  `Paraview` can work with.

  In order to do this, we run the `xcreate_movie_AVS_DX` that is located in the
  `bin/` folder. From the root folder, run the following
  command:

```shell
      ./bin/xcreate_movie_AVS_DX
```

  This script will then give you several options for how you want to format the
  movie data:

  * 1st prompt: Choose option `2 = create files in AVS UCD format with 
    individual files`.

  * 2nd prompt: Choose the timestep you want the movie to `start` (e.g. 1).

  * 3rd prompt: Choose the timested you want the movie to `end` (e.g. -1).

  * 4th prompt: Choose the `component` you want to visualize (e.g. 1)

  The movie data will now be converted to `AVS` format and stored in the
  `OUTPUT_FILES/` folder.

* **Step 3: Visualize using Paraview**

  Start `Paraview`, click the `Open` button in the top left corner, and
  navigate to the `OUTPUT_FILES/` folder. In this folder you should see 
  a file-bundle called `AVS_movie_*.inp`, which is the formatted movie 
  data that we generated in the previous step.

  In order to visualize the surface movie, select the `AVS_movie_*.inp` bundle
  (not the individual files contained in the bundle) and click `OK`.
  
  An `Open Data With...` menu should now appear. Select the `AVS UCD
  Binary/ASCII Files` option and click `OK`.

  The movie data is now loaded, and you can click `Apply` in the `Properties`
  menu on the left-hand side in order to display it. To run the movie, click
  the leftmost green arrow in the top menu, called `First Frame`, and then
  click the center green arrow, called `Play`.

  You might want to adjust the color scale to your own liking.

---
In this section, we have looked at how to create a surface movie for our
simulation and how to visualize it using Paraview.

In the next section we move on to **Part IV** of the tutorial, and look at how
to run adjoint simulations using SPECFEM3D_GLOBE.

[Previous section](/vis_mesh.md) -- [Next section](/run_adj_solver.md)
