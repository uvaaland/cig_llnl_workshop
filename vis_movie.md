### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
    1. [Visualize Seismograms](/vis_seismo.md)
    2. [Visualize Model Mesh](/vis_mesh.md)
    3. [Visualize Surface Movie](/vis_movie.md)
6. [Resources](resources.md)


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
saved. Therefore, open up the `Par_file` and set the following parameter to
`true`:

      ...

      # save AVS or OpenDX movies
      #MOVIE_COARSE saves movie only at corners of elements (SURFACE OR VOLUME)
      #MOVIE_COARSE does not work with create_movie_AVS_DX
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
  And use `squeue` to monitor the job.


* **Step 2: Generate the movie data**

  The surface movie data files are stored in the
  `./specfem3d_globe/OUTPUT_FILES/` folder as `moviedata*`. In order to
  visualize the surface movie in `Paraview`, we need to convert these datafiles
  to a format that `Paraview` can work with.

  In order to do this, we run the `xcreate_movie_AVS_DX` that is located in the
  `./specfem3d_globe/bin/` folder. From the root folder, run the following
  command:

```shell
      ./bin/xcreate_movie_AVS_DX
```

  This script will then give you several options for how you want to format the
  movie data:

  * 1st prompt: Choose option `2 = create files in AVS UCD format with 
    individual files`.

  * 2nd prompt: Choose the timestep you want the movie to `start`.

  * 3rd prompt: Choose the timested you want the movie to `end`.

  * 4th prompt: Choose the `component` you want to visualize.

  For the first prompt, choose option `2 = create files in AVS UCD
  format with individual files`.

  For the following two prompts, choose the timesteps you want the movie to
  `start` and `end`. Then, for the final prompt, choose which component you want to
  visualize `(Z/N/E)`.

  The movie data will now be converted to `AVS` format and stored in the
  `./specfem3d_globe/OUTPUT_FILES/` folder.

* **Step 3: Visualize using Paraview**

---
In this section, we have looked at how to provide the input data that is
necessary to run a continental-scale simulation with SPECFEM3D_GLOBE.

In the next section, we will look at how to generate a mesh for the
continental-scale model.



[Previous section](/vis_mesh.md) -- [Next section](/vis_movie.md)
