# Instructions for using CSC-UW version of allenCCF

## Installation
1. Install MATLAB and the Image Processing Toolbox (required by allenCCF).
2. Install `allenCCF` according to its instructions.
    - Save `annotation_volume_10um_by_index.npy` and `template_volume_10um.npy` to your `userpath` directory. You can find this directy by opening MATLAB and typing `userpath`. On Windows, its default location is `%USERPROFILE%/Documents/MATLAB`.
3. (Optional, but discouraged) Add `allenCCF` and `npy-matlab` to your MATLAB search path. Personally, I prefer to never to save changes to the path, and always modify my path each session, to avoid accidental namespace collisions and improve reproducibility across users.

## Usage
1. Place raw (1.25x objective, 2048x2048, 96dpi, 2.2612um/pixel) images on neuropixel_analysis, e.g. `/Volumes/neuropixel_analysis/Data/acute/recovery_sleep/ANPIX1-Sputnik/SHARP-Track_histology/`.
> WARNING: This code expects, but does not check, that you will give it images with 2.2612 um/pixel!!!
2. Make sure `allenCCF` and `npy-matlab` are on your MATLAB search path.
3. Copy template scripts `allenCCF/CSC-UW/ANPIX0-*.m`, rename with your subject's ID, and update the following variables in each of these scripts:
    - `A-Process_Histology.m`: `image_folder`
    - `B-Register_Slices.m`: `processed_images_folder`, `annotation_volume_location`, `template_volume_location`, `structure_stree_location`
    - `C-Mark_Probes.m`: `processed_images_folder`, `annotation_volume_location`, `template_volume_location`, `structure_stree_location`
    - `D-Display_Probe_Tracks.m`: `position_data_folder`, `processed_images_folder`, `annotation_volume_location`, `structure_stree_location`
4. Run steps in order, per the [SHARP-Track Wiki](https://github.com/cortex-lab/allenCCF/wiki).
