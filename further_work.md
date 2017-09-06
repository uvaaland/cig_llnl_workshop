### Table of Contents
1. [Overview](/index.md)
2. [Introduction](/intro_specfem.md)
3. [Part I: Setting up SPECFEM3D_GLOBE](/setup_specfem3d.md)
4. [Part II: Continental-scale Simulations](/prepare_data.md)
5. [Part III: Visualization](/vis_seismo.md)
6. [Part IV: Adjoint Simulations (Bonus)](/run_adj_solver.md)
7. [Further Work](/further_work.md)
8. [Resources](/resources.md)


## Further Work
If you have finished the tutorial up until this point, you could attempt one of
the following tasks:

#### Run a forward simulation with a different model resolution

  **Hint:** Change the following parameters in the `Par_file` and the submission
  scripts `submit_mesher` and `submit_solver` accordingly

      # number of elements at the surface along the two sides of the first chunk
      # (must be multiple of 16 and 8 * multiple of NPROC below)
      NEX_XI                          = 192
      NEX_ETA                         = 192
  
      # number of MPI processors along the two sides of the first chunk
      NPROC_XI                        = 12
      NPROC_ETA                       = 12

  **Recall:** `#processors = NPROC_XI * NPROC_ETA * NCHUNKS`

#### Setup and run a simulation with an event of your choice

  **Hint:** Replace the `CMTSOLUTION` file with the CMT solution for your
  event. You can find this information at the [Global CMT web page](http://www.globalcmt.org/).

  It might also be necessary to change the following parameters in the
  `Par_file`, depending on the location of the event

      # angular width of the first chunk (not used if full sphere with six chunks)
      CENTER_LATITUDE_IN_DEGREES      = 40.d0
      CENTER_LONGITUDE_IN_DEGREES     = -120.d0

#### Run a forward simulation with a different background model and compare the seismograms for the two simulations

  **Hint:** Change the following parameter in the `Par_file` to one of the
  other models that is listed.

      # 1D models with real structure:
      # 1D_isotropic_prem, 1D_transversely_isotropic_prem, 1D_iasp91, 1D_1066a, 1D_ak135f_no_mud, 1D_ref, 1D_ref_iso, 1D_jp3d,1D_sea99
      #
      # 1D models with only one fictitious averaged crustal layer:
      # 1D_isotropic_prem_onecrust, 1D_transversely_isotropic_prem_onecrust, 1D_iasp91_onecrust, 1D_1066a_onecrust, 1D_ak135f_no_mud_onecrust
      #
      # fully 3D models:
      # transversely_isotropic_prem_plus_3D_crust_2.0, 3D_anisotropic, 3D_attenuation,
      # s20rts, s40rts, s362ani, s362iso, s362wmani, s362ani_prem, s362ani_3DQ, s362iso_3DQ,
      # s29ea, s29ea,sea99_jp3d1994,sea99,jp3d1994,heterogen,full_sh
      #
      # 3D models with 1D crust: append "_1Dcrust" the the 3D model name
      #                          to take the 1D crustal model from the
      #                          associated reference model rather than the default 3D crustal model
      # e.g. s20rts_1Dcrust, s362ani_1Dcrust, etc.
      MODEL                           = s362ani

  Remember to save the seismograms from the first simulation before you run the
  simulation with a different background model.

---

[Previous section](/run_adj_kernel.md) -- [Next section](/resources.md)
