````{admonition} Scripts for **Imaging - Lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/major_image_lines.py" target="_blank">major_image_lines.py</a> # main script (adopted approach described on the present page)
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/image_lines.py" target="_blank">image_lines.py</a> # experimental main script (initial experiments described on a [previous page](imaging-lines-initial-approaches.md))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_mask.py" target="_blank">dictionary_mask.py</a> # loads mask_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a> # loads disk_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_lines.py" target="_blank">dictionary_lines.py</a> # loads line_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/JvM_correction_casa6.py" target="_blank">JvM_correction_casa6.py</a> # MAPS JvM correction script ([Czekala et al. 2021](https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/keplerian_mask.py" target="_blank">keplerian_mask.py</a> # modified version of [keplerian_mask](https://github.com/richteague/keplerian_mask) by [Rich Teague](https://richteague.github.io/)
````

````{admonition} Visibility Data for **Imaging - Lines** (obtained after [step 4](../step4/step4-line-mses-achieved.md)):
:class: tip
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_12CO.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_13CO.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_C18O.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_SO.bin30s.ms.contsub</a>
````


# Adopted Line Imaging Strategy

*The following text is a synthesis of the Methods section of <a href="https://www.nature.com/articles/s41586-024-07877-0" target="_blank">Speedie et al. 2024</a> and Section 2.2 of  <a href="https://doi.org/10.3847/2041-8213/adb7d5" target="_blank">Speedie et al. 2025</a>. The line imaging script in the companion github repository is <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/major_image_lines.py" target="_blank">major_image_lines.py</a>.*


**SOFTWARE:** All imaging was performed with the CASA ``tclean`` task. 

**STRATEGY:** The <sup>12</sup>CO data immediately presented two challenges: 

1. Non-Keplerian large-scale diffuse emission with morphologies difficult to mask. 

2. Negative bowling (<a href="https://ui.adsabs.harvard.edu/abs/1985A&A...143..307B" target="_blank">Braun & Walterbos 1985</a>), particularly in central channels. 

The latter issue is symptomatic of emission on spatial scales larger than the maximum recoverable scale of our short-baseline configuration C-3 (MRS ~ 7" at 230 GHz; <a href="https://ui.adsabs.harvard.edu/abs/2019athb.rept.....R" target="_blank">ALMA Technical Handbook</a>), and can only be solved by obtaining additional observations sampling the visibility function at smaller *uv*-spacings. 

In the absence of more data --and after experimentation with CASA's auto-multithresh masking algorithm (<a href="https://ui.adsabs.harvard.edu/abs/2020PASP..132b4505K" target="_blank">Kepley et al. 2020</a>; see [experiments](imaging-lines-initial-approaches.md))-- we adopted the following strategies to mitigate both those two challenges (listed above): 

**First, we cleaned with a broad mask** encompassing all emission within the field of view (FOV).

To achieve this broad mask we used the ``tclean`` arguments ``usemask=`pb'`` and ``pbmask=0.2``, which sets a cleaning mask extending to where the 12m antenna primary beam gain reaches the 20% level, which is usually considered the edge of the FOV. The fact that we did not image with a Keplerian mask also meant we did not restrict our ability to observe non-Keplerian emission (critical for the science). 

In accordance with cleaning with this broad mask, **we cleaned conservatively** (i.e., relatively shallowly). 
The CLEAN ``threshold`` was set to 5x the rms noise measured in 20 line-free channels of the dirty image cube. 

**Second, we forced frequent major cycles** to repeatedly re-populate the *uv*-plane and interpolate into the missing short *uv*-spacings. 

To achieve frequent major cycles we set the maximum number of minor cycle iterations per channel to ``cycleniter=80``, the minor cycle threshold to ``max_psf_sidelobe_level=3.0`` and ``minpsffraction=0.5``, and the maximum assigned clean component to ``gain=0.02`` times the peak residual. Here is an excerpt of the ``tclean`` function arguments:

````
# Cautious/conservative clean:
cycleniter             = 80    # Jess: Maximum number of minor-cycle iterations (per plane) before triggering a major cycle
cyclefactor            = 3.0   # Ryan: 3x max_psf_sidelobe_level as minor cycle threshold (default is 1.0)
gain                   = 0.02  # Ryan: assign clean component peaks to 2% of pixel value (default is 0.1)
minpsffraction         = 0.5   # PHANGS: cycle threshold is never lower than 0.5 times the peak residual (default: 0.05)
````

To ensure we were successful in forcing frequency major cycles, we kept track of the number of major cycles that occurred in the imaging of each cube. For example, the <sup>12</sup>CO cube imaged with ``robust=0.5`` underwent 282 major cycles and took 5 days to run. The <sup>13</sup>CO cube imaged with ``robust=0.5`` underwent 198 major cycles; and the C<sup>18</sup>O cube imaged with ``robust=0.5`` underwent 76 major cycles.

To summarize: We clean conservatively, with a broad mask (``usemask='pb'`` and ``pbmask=0.2``), forcing frequent major cycles. This approached borrowed from the philosophy of the PHANGS-ALMA Large Program (<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..255...19L" target="_blank">Leroy et al. 2021</a>).



**DECONVOLUTION BASIS FUNCTIONS:** We used the multiscale deconvolution algorithm (<a href="https://ui.adsabs.harvard.edu/abs/2008ISTSP...2..793C" target="_blank">Cornwell 2008</a>) with 
Gaussian deconvolution scales ``[0.02", 0.1", 0.3", 0.6", 1.0"]``, with an additional largest scale of ``2.0"`` appended for <sup>12</sup>CO. 

**WEIGHTING:** 
We adopted a Briggs robust weighting scheme, and generated two sets of image cubes; one with a robust value of ``0.5`` and a second with robust ``1.5``. 

**FOV AND PIXEL SIZE:** 
We imaged with a FOV out to the primary beam FWHM (38") with 0.02" pixels (9 or 12 pixels per synthesized beam minor or major axis, respectively). 

**SPECTRAL GRIDDING:** 
We imaged in LSRK velocity channels at 42 m/s for <sup>12</sup>CO & <sup>13</sup>CO, and at 84 m/s for C<sup>18</sup>O and SO (nearly the native channel spacing of the data).

**POST-DECONVOLUTION CORRECTIONS:** 
We applied JvM correction (<a href="https://ui.adsabs.harvard.edu/abs/1995AJ....110.2037J" target="_blank">Jorsater & van Moorsel 1995</a>, <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C" target="_blank">Czekala et al. 2021</a>) and primary beam correction. 




## Resulting Line Image Cubes

Properties of the resulting line image cubes are provided in the table below. Note that this table scrolls horizontally. All the parameter details you'd need to reproduce these images can be found in the CASA log files linked in the second-to-last column of the table.


````{card}
<div class="table_wrapper">
<table>

| <div style="width:125px">Transition</div>         | <div style="width:150px">Rest Frequency</div> | <div style="width:125px">Channel Width</div> | <div style="width:80px">``robust``</div> | <div style="width:175px">Beam        </div>  | <div style="width:100px">rms Noise </div> | <div style="width:100px">JvM epsilon</div> | <div style="width:200px">Number of major cycles</div> | <div style="width:350px">CASA log file</div>   | <div style="width:200px">Version name in <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_lines.py" target="_blank">dictionary_lines.py</a></div> |
|--------------------|----------------------|------------------------|--------|------------------------------------|------------------------|--------------------------|--------------------------|--------------------------------------------|---------|
|                                                   | **(GHz)**                                     | **(km/s)**        |            | **(" x ", deg)**  | **(mJy/beam)** |             |                        |                 |                                     |
| <sup>12</sup>CO *J*=2-1         | 230.538000           | 0.042                  | 0.5    | 0.235" × 0.172", 0.2°    | 1.63                   | 0.496                      | 282                      | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230411-171634-12CO.log" target="_blank">casa-20230411-171634-12CO.log</a> (77 MB)      | v11_    |
| <sup>12</sup>CO *J*=2-1         | 230.538000           | 0.042                  | 1.5    | 0.398" × 0.270", -5.0°   | 0.76                   | 0.325                      | 261                      | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230405-174838-12CO.log" target="_blank">casa-20230405-174838-12CO.log</a> (93 MB)      | v11_    |
| <sup>13</sup>CO *J*=2-1         | 220.398684           | 0.042                  | 0.5    | 0.237" × 0.175", 1.2°     | 1.84                   | 0.497                      | 198                      | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230324-185500-13CO.log" target="_blank">casa-20230324-185500-13CO.log</a> (39 MB)      | v11_    |
| <sup>13</sup>CO *J*=2-1         | 220.398684           | 0.042                  | 1.5    | 0.390" × 0.274", -1.4°   | 1.10                   | 0.339                      | 346                      | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230331-174529-13CO.log" target="_blank">casa-20230331-174529-13CO.log</a> (70 MB)      | v11_    |
| C<sup>18</sup>O *J*=2-1         | 219.560358           | 0.084                  | 0.5    | 0.240" × 0.180", -2.2°    | 0.93                   | 0.510                      | 76                       | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230324-185500-C18O.log" target="_blank">casa-20230324-185500-C18O.log</a> (8.7 MB)     | v11_    |
| C<sup>18</sup>O *J*=2-1         | 219.560358           | 0.084                  | 1.5    | 0.400" × 0.276", -7.7°   | 0.53                   | 0.330                      | 120                      | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230331-174529-C18O.log" target="_blank">casa-20230331-174529-C18O.log</a> (13 MB)      | v11_    |
| SO *J*<sub>N</sub> = 5<sub>6</sub>-4<sub>5</sub>      | 219.949442           | 0.084                  | 0.5    | 0.237" × 0.179", -2.7°    | 0.95                   | 0.511                      | 6                        | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230324-185500-SO.log" target="_blank">casa-20230324-185500-SO.log</a> (400 KB)       | v11_    |
| SO *J*<sub>N</sub> = 5<sub>6</sub>-4<sub>5</sub>      | 219.949442           | 0.084                  | 1.5    | 0.390" × 0.276", -8.8°   | 0.55                   | 0.340                      | 15                       | <a href="https://github.com/jjspeedie/guide.2021.1.00690.S/blob/main/imaging-cont/casalogs/casa-20230331-174529-SO.log" target="_blank">casa-20230331-174529-SO.log</a> (1 MB)         | v11_    |

 </table>
 </div>
+++
&rarr;&rarr;&rarr; *This table scrolls horizontally* &rarr;&rarr;&rarr;

**Properties of the published line image cubes.** The metrics shown here correspond to the primary beam corrected, JvM corrected image cubes, though all ``tclean`` image output types are available in the public data repositories (see links below). All data has been continuum-subtracted, though SO images without continuum subtraction are available.
The rms noise is measured in a line-free channel of the cubes within a circlular aperture of 10" radius centered on the star.
````




````{admonition} Links to download the resulting **Line Images**:
:class: tip
Moment maps and VADPs are also available.
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/images_lines/12CO/v11_robust0.5/full_cube" target="_blank"><sup>12</sup>CO line images fits files (``robust=0.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/images_lines/12CO/v11_robust1.5" target="_blank"><sup>12</sup>CO line images fits files (``robust=1.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/images_lines/13CO/v11_robust0.5" target="_blank"><sup>13</sup>CO line images fits files (``robust=0.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/images_lines/13CO/v11_robust1.5" target="_blank"><sup>13</sup>CO line images fits files (``robust=1.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/images_lines/C18O/v11_robust0.5" target="_blank">C<sup>18</sup>O line images fits files (``robust=0.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/images_lines/C18O/v11_robust1.5" target="_blank">C<sup>18</sup>O line images fits files (``robust=1.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/images_lines/SO/v11_robust0.5" target="_blank">SO line images fits files (``robust=0.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/images_lines/SO/v11_robust1.5" target="_blank">SO line images fits files (``robust=1.5``)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/images_lines/SO/v11_withcont_robust0.5" target="_blank">SO line images fits files (``robust=0.5``, not continuum-subtracted)</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/images_lines/SO/v11_withcont_robust1.5" target="_blank">SO line images fits files (``robust=1.5``, not continuum-subtracted)</a>
````

