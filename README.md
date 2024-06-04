# earlyLongitudinalBrainDevelopmentLanguage

This repository houses code (or links to code) used for the following study:

    Turesky et al. Longitudinal trajectories of brain development from infancy to school-age and their relationship to language skill

Broadly, the study involved structural and diffusion processing pipelines followed by statistical analyses. An inventory of the code used for each pipeline is provided below:

### Structure:

    .
    ├── reFS.sh                                 <-- runs infant brain morphometry pipeline
        ├── iFS_wrap.sh                         <-- sets environmental variables for iFS and runs it *this file will need adjustments based on the user's compute setup
        ├── ibeat2aseg.m                        <-- merges iFS and iBEATv2.0 tissue segmentations
            ├── aseg_labels2coords.m            <-- converts aseg labels to coordinates
        ├── aseg2wm.m                           <-- generates FS white matter file using iBEATv2.0 segmentation
        ├── fs_autorecon2_end.sh                <-- runs FS autorecon2 with adjustments
        ├── fs_autorecon3_wrap.sh               <-- runs FS autorecon3 with adjustments (uses expert.opts file included)
    ├── consol_stats.sh                         <-- tabulates brain estimates in preparation for statistical analysis


Requires iBEATv2.0 (https://github.com/iBEAT-V2/iBEAT-V2.0-Docker) segmentations be generated beforehand. 

Dependencies: iBEATv2.0 Docker, Infant FreeSurfer, FreeSurfer 7.3, Matlab.
The folder containing the above scripts also need to be added to your shell PATH. 


### Diffusion:

    .
    ├── dwi_proc_tck_gen_v2.sh                     <-- preprocesses diffusion data and runs fiber tracking
    ├── mrtrix2bids_sep.sh                         <-- reorganizing directory structure to prepare for py(Baby)AFQ
    ├── baby-pyafq-gen.py                          <-- bids_path needs to be entered 
    ├── pyafq-gen.py                               <-- bids_path needs to be entered 
    ├── plot_viz_inf_cam_(l/r)trk_core.py                             <-- visualizes tracts 
    ├── plot_viz_inf_cam_ltrk_core_r2.py                             <-- visualizes tract cores 


Requires FreeSurfer-style T1 segmentation be generated beforehand.

Dependences: MRtrix3, FSL, ANTs, FreeSurfer, GCC libraries for LD_LIBRARY_PATH, pyAFQ
The folder containing the above scripts also need to be added to your shell PATH. Additionally, our first script (indirectly) calls the cuda implementation of eddy, which also requires access to a GPU (we used Nvidia A100). 


### Statistical analyses:

    .
    ├── bb_struct_reorg.R                             <-- reformats structural estimates from FreeSurfer 
    ├── bb_dwi_reorg_r4.R                             <-- reformats diffusion estimates from py(Baby)AFQ
    ├── longitudinal_model_control.R                  <-- set paramaters for statistical analyses visualizations
        ├── model_funs.R                              <-- runs longitudinal models - linear, logarithmic, quadratic, or asymptotic - including data cleaning, curve fitting and visualizations, and associations with outcomes
        ├── graph_labels_colors.R                     <-- specifies colors used in graphs
        ├── gen_heatmap.R                             <-- runs heatmaps depicting covariate contributions to models
        ├── compare_models_fun.R                      <-- compares fits among longitudinal models (does not include asymptotic functions)
        ├── MSU_longitudinal_models_functions.R       <-- leverages a subset of functions provided here: https://github.com/knickmeyer-lab/ORIGINs_ICV-and-Subcortical-volume-development-in-early-childhood (asymptotic models only)
        ├── long_model_report_stats_fun               <-- generates and reports statistics corrected for multiple comparisons (for structural and average- or quarter-based diffusion analyses)  
        ├── diff_node_clust_r5.R                      <-- generates and reports statistics corrected for multiple comparisons (for node-based diffusion analyses)
        ├── brain_region_ggseg_fun_r3.R               <-- depicts significant brain regions (for structure only)
        ├── long_graph_r2.R                           <-- generates graph showing longitudinal sample
        ├── long_descriptive_stats_r6.R               <-- reports descriptive stats for study


required packages: dplyr, reshape, stringr, ggplot2, ggseg, lme4, lmerTest, nlme, permuco





