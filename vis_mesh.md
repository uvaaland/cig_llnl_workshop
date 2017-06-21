### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
    1. [Visualize Seismograms](/vis_seismo.md)
    2. [Visualize Model Mesh](/vis_mesh.md)
    3. [Visualize Movie](/vis_movie.md)
6. [Resources](resources.md)


## Part III: Visualization

In this third part of the tutorial, we will look at methods for visualizing the
output simulation data. We will look at the following categories:

* Visualize Seismograms
* <mark>Visualize Model Mesh</mark>
* Visualize Movie

### Visualize Model Mesh

In order to visualize the model mesh, we need to modify the `Par_file` such
that the mesh data are being saved. Therefore, open up the `Par_file` and set
the following parameter to `true`:

      ...

      # save mesh files to check the mesh
      SAVE_MESH_FILES                 = .true.

      ...

Once we have updated this parameter, we need to go through the following three
steps in order to visualize the model mesh:

1. Rerun the mesh routine
2. Combine the output mesh data
3. Open up Paraview

* **Step 1: Rerun the mesh routine**
  
  This step is identical to what we did in Part II. We run the `xmeshfem3D`
  executable on the cluster by submitting the `submit_mesher` script:

```shell
      sbatch submit_mesher
```
  We can then use `squeue` to monitor the job.

* **Step 2: Combine the output mesh data**

  Once we have rerun the mesh routine with the `SAVE_MESH_FILES` parameter set
  to true, the mesh files will be output to the `DATABASES_MPI/` folder. The
  data is partitioned among the processees, and we will want to combine these
  data into single files.

  We can achieve this by running the `xcombine_vol_data_vtk` executable that is
  located in the `bin/` folder.


