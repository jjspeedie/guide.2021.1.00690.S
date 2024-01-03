`````{admonition} The tasks in this chapter use the following scripts:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/image_continuum.py" target="_blank">image_continuum.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_mask.py" target="_blank">dictionary_mask.py</a> # loads mask_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/JvM_correction_casa6.py" target="_blank">JvM_correction_casa6.py</a> # MAPS JvM correction script ([Czekala et al. 2021](https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract))

````{card} And data (obtained after [step 3](../step3/step3-continuum-ms-achieved.md)):
- <a href="https://www.canfar.net/storage/vault/list/jspeedie/2021.1.00690.S/private/measurement_sets" target="_blank">ABAur_continuum.bin30s.ms</a> **could also link to log file
`````

# Preliminary Images

WRONG: 2X RMS NOISE. The following images were cleaned non-interactively using a circular mask of radius 2 arcsec centered on 04:55:45.854900 +30.33.03.73320 (J2000), the hogbom deconvolver with a Briggs robust weighting and no uv-taper, a cell size of 0.04 arcsec and 2000 cells, and cleaned down to a threhold of 1x the rms noise measured in the dirty image within an annulus (inner radius 4 arcsec; outer radius 10 arcsec).
Things to improve: The cell size should be dependent on the `robust` parameter (cell size should sample the beam ~5-10 times and the beam depends on the `robust` parameter); the beam minor axis is borderline-sampled in the robust=0 image. We could also try uv-tapering. It is strange to clean down to 1x the rms noise measured in the dirty image, but I felt the residuals after cleaning to 4x or 3x were still quite large (i.e. I felt the residuals were still well above the noise and more signal could be extracted).


## Image made with Briggs robust = 0.5

````{card} Key values in imaging process
| Dirty Image RMS (uJy/beam)|CLEAN `threshold` (mJy/beam)|JvM Epsilon (unitless)      | Residual Image Peak (unitless)|
|---------------------|----------------|------------------|-------------------------------|
|50.20    |0.1004   |0.4566|0.0992                    |
````

````{card} Properties of the resulting images
|CLEAN Image          |Peak Intensity (mJy/beam)|Disk Flux (mJy)   |RMS noise (uJy/beam)|SNR               |
|-----------------|-------------------------|------------------|--------------------|------------------|
|`.image`           |2.13        |102.9|13.34  |159.5|
|`.JvMcorr.image`   |2.09       |89.9 |6.11   |342.6 |
|`.image.pbcor`     |2.14        |103.1|17.37   |123.1|
|`.JvMcorr.image.pbcor`|2.09        |90.0 |7.92   |264.1|
+++
Peak intensity, disk flux (total flux within cleaning mask), measured RMS noise (within an annulus with inner and outer radii 4'' and 11'', respectively) and signal to noise ratio (column 2 / column 4) for each of the 4 image types. `.image` is the "regular" CLEAN image. `.pbcor` indicates primary beam corrected, and `.JvMcorr` indicates JvM corrected.
````

````{card}
<img src="images/robust0.5.ABAUR_continuum.JvMcorr.image.pbcor_zoomout.jpg" alt="robust0.5.ABAUR_continuum.JvMcorr.image.pbcor" class="mb-1" width="48%">
<img src="images/robust0.5.ABAUR_continuum.JvMcorr.image.pbcor_zoom.jpg" alt="robust0.5.ABAUR_continuum.JvMcorr.image.pbcor" class="mb-1" width="48%">
+++
JvM-corrected and primary beam-corrected continuum image with `robust` parameter of 0.5. <i>Left:</i> Zoom-out with aggressive colorbar stretch to accentuate background noise. <i>Right:</i> Zoom-in with less aggressive colorbar stretch.
````


````{card}
<img src="images/robust0.5.ABAUR_continuum.image_zoomout.jpg" alt="robust0.5.ABAUR_continuum.image" class="mb-1" width="32%">
<img src="images/robust0.5.ABAUR_continuum.image.pbcor_zoomout.jpg" alt="robust0.5.ABAUR_continuum.image.pbcor" class="mb-1" width="32%">
<img src="images/robust0.5.ABAUR_continuum.JvMcorr.image_zoomout.jpg" alt="robust0.5.ABAUR_continuum.JvMcorr.image" class="mb-1" width="32%">
+++
<i>Left:</i> Regular CLEAN image. <i>Middle:</i> Regular CLEAN image, primary beam corrected. <i>Right:</i> JvM corrected image (not primary beam corrected).
````

## Image made with Briggs robust = 1.0

````{card} Key values in imaging process
| Dirty Image RMS (uJy/beam)|CLEAN `threshold` (mJy/beam)|JvM Epsilon (unitless)      | Residual Image Peak (unitless)|
|---------------------|----------------|------------------|-------------------------------|
|150.3    |0.3006   |0.3531 |0.2998                    |
````


````{card} Properties of the resulting images
|CLEAN Image          |Peak Intensity (mJy/beam)|Disk Flux (mJy)   |RMS noise (uJy/beam)|SNR               |
|-----------------|-------------------------|------------------|--------------------|------------------|
|`.image`           |4.47       |111.65|24.24  |184.2|
|`.JvMcorr.image`   |4.30        |89.86 |8.45   |509.1 |
|`.image.pbcor`     |4.45        |111.84|31.33   |142.0|
|`.JvMcorr.image.pbcor`|4.34        |89.96 |11.04  |393.5|
+++
Peak intensity, disk flux (total flux within cleaning mask), measured RMS noise (within an annulus with inner and outer radii 4'' and 11'', respectively) and signal to noise ratio (column 2 / column 4) for each of the 4 image types. `.image` is the "regular" CLEAN image. `.pbcor` indicates primary beam corrected, and `.JvMcorr` indicates JvM corrected.
````

````{card}
<img src="images/robust1.0.ABAUR_continuum.JvMcorr.image.pbcor_zoomout.jpg" alt="robust1.0.ABAUR_continuum.JvMcorr.image.pbcor" class="mb-1" width="48%">
<img src="images/robust1.0.ABAUR_continuum.JvMcorr.image.pbcor_zoom.jpg" alt="robust1.0.ABAUR_continuum.JvMcorr.image.pbcor" class="mb-1" width="48%">
+++
JvM-corrected and primary beam-corrected continuum image with `robust` parameter of 1.0. <i>Left:</i> Zoom-out with aggressive colorbar stretch to accentuate background noise. <i>Right:</i> Zoom-in with less aggressive colorbar stretch.
````


````{card}
<img src="images/robust1.0.ABAUR_continuum.image_zoomout.jpg" alt="robust1.0.ABAUR_continuum.image" class="mb-1" width="32%">
<img src="images/robust1.0.ABAUR_continuum.image.pbcor_zoomout.jpg" alt="robust1.0.ABAUR_continuum.image.pbcor" class="mb-1" width="32%">
<img src="images/robust1.0.ABAUR_continuum.JvMcorr.image_zoomout.jpg" alt="robust1.0.ABAUR_continuum.JvMcorr.image" class="mb-1" width="32%">
+++
<i>Left:</i> Regular CLEAN image. <i>Middle:</i> Regular CLEAN image, primary beam corrected. <i>Right:</i> JvM corrected image (not primary beam corrected).
````

## Image made with Briggs robust = 1.5

````{card} Key values in imaging process
| Dirty Image RMS (uJy/beam)|CLEAN `threshold` (mJy/beam)|JvM Epsilon (unitless)      | Residual Image Peak (unitless)|
|---------------------|----------------|------------------|-------------------------------|
|253.2    |0.5064   |0.3383|0.5064                    |
````


````{card} Properties of the resulting images
|CLEAN Image          |Peak Intensity (mJy/beam)|Disk Flux (mJy)   |RMS noise (uJy/beam)|SNR               |
|-----------------|-----------------------|------------------|--------------------|------------------|
|`.image`           |5.94       |117.38|41.83   |142.1|
|`.JvMcorr.image`   |5.73        |90.13 |14.13  |405.6       |
|`.image.pbcor`     |5.95        |117.60|54.10   |110.0|
|`.JvMcorr.image.pbcor`|5.76        |90.25 |18.34  |314.2|
+++
Peak intensity, disk flux (total flux within cleaning mask), measured RMS noise (within an annulus with inner and outer radii 4'' and 11'', respectively) and signal to noise ratio (column 2 / column 4) for each of the 4 image types. `.image` is the "regular" CLEAN image. `.pbcor` indicates primary beam corrected, and `.JvMcorr` indicates JvM corrected.
````

````{card}
<img src="images/robust1.5.ABAUR_continuum.JvMcorr.image.pbcor_zoomout.jpg" alt="robust1.5.ABAUR_continuum.JvMcorr.image.pbcor" class="mb-1" width="48%">
<img src="images/robust1.5.ABAUR_continuum.JvMcorr.image.pbcor_zoom.jpg" alt="robust1.5.ABAUR_continuum.JvMcorr.image.pbcor" class="mb-1" width="48%">
+++
JvM-corrected and primary beam-corrected continuum image with `robust` parameter of 1.5. <i>Left:</i> Zoom-out with aggressive colorbar stretch to accentuate background noise. <i>Right:</i> Zoom-in with less aggressive colorbar stretch.
````


````{card}
<img src="images/robust1.5.ABAUR_continuum.image_zoomout.jpg" alt="robust1.5.ABAUR_continuum.image" class="mb-1" width="32%">
<img src="images/robust1.5.ABAUR_continuum.image.pbcor_zoomout.jpg" alt="robust1.5.ABAUR_continuum.image.pbcor" class="mb-1" width="32%">
<img src="images/robust1.5.ABAUR_continuum.JvMcorr.image_zoomout.jpg" alt="robust1.5.ABAUR_continuum.JvMcorr.image" class="mb-1" width="32%">
+++
<i>Left:</i> Regular CLEAN image. <i>Middle:</i> Regular CLEAN image, primary beam corrected. <i>Right:</i> JvM corrected image (not primary beam corrected).
````










#
