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

In order to create a surface movie of teh simulation, we need to go through a
couple of steps that are similar to what we did for visualizing the model mesh.
First, we need to modify the `Par_file` surch that the movie data are being
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

* **Step 2: Generate the movie data**

* **Step 3: Visualize using Paraview**

---
In this section, we have looked at how to provide the input data that is
necessary to run a continental-scale simulation with SPECFEM3D_GLOBE.

In the next section, we will look at how to generate a mesh for the
continental-scale model.



[Previous section](/vis_mesh.md) -- [Next section](/vis_movie.md)
