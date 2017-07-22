### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
7. [Resources](resources.md)


## Further Work
If you have finished the tutorial up until this point, you could attempt one of
the following tasks:
* Run a forward simulation with a different model resolution

  **Hint:** Change the following parameters in the `Par_file` and the submission
  scripts `submit_mesher` and `submit_solver` accordingly

      # number of elements at the surface along the two sides of the first chunk
      # (must be multiple of 16 and 8 * multiple of NPROC below)
      NEX_XI                          = 256
      NEX_ETA                         = 256
  
      # number of MPI processors along the two sides of the first chunk
      NPROC_XI                        = 16
      NPROC_ETA                       = 16


* Setup and run a simulation with an event of your choice
* Run a forward simulation with a different background model and compare the
  seismograms for the two simulations


---

[Previous section](/run_adj_kernel.md) -- [Next section](/resources.md)
