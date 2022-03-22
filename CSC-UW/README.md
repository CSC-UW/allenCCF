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

## Best practices [Work in progress]

### When registering slices
- Prefer registration points local to the probe track.
- Place more points in areas of higher certainty/utility.
- Only place registration points on undamged/warped areas, usually deeper inside the brain, unless strictly necessary. 
- If you need to place registration points on the cortical surface, but don't have a high quality landmark, try to use a chain of equidistant points starting at the midline

### When marking probe tracks
- If the probe track on a single slice is clearly linear, use 2 probe points to mark its extremes. Otherwise, use a single probe point to mark its center of mass, even if its oblong. 
- Start by marking probe points that clearly belong together. It can be helpful to scroll through all slices first to get an overview of visible tracks, and you may end up deciding to work back-to-front. 
- Mark unambiguous probe tracks -> Visualize using `Display_Probe_Tracks` -> Assign ambiguous probe points/tracks to unused probes -> Visualize -> Reassign ambiguous points -> Repeat until done.
- It is not always best to mark every probe point. If the local transoformation is suspect, e.g. because of a badly warped slice, it might be better to omit some points and project the line of best fit instead. 
- Don't forget to check the camviewer3d photos of probe locations to help sanity check / orient yourself.

## TODO
- Add ability to project along a best-fit line to a NEW/expected slice. 
- Add ability to use >11 "probes", or "probe points" that are not actually assigned to a probe.
- 'd' should only delete probe points from active slices. 
- Add ability to weight probe points.
