# Program Overview

ALMA observed AB Aur in April, May and September 2022 under program ID 2021.1.00690.S (PI: R. Dong). Measurements were taken with the Band 6 receivers (<a href="https://ui.adsabs.harvard.edu/abs/2004stt..conf..181E/abstract" target="_blank">Ediss et al. 2004</a>) in array configurations C-3 (2 execution blocks) and C-6 (6 execution blocks), hereafter the "short-baseline" and "long-baseline" configurations, respectively.
In total, the 8 execution blocks (EBs) reached an on-source integration time of 5.75 hours.


## Observation Summary

````{card}
<center>

<img src="./images/observation-summary.png" alt="observation-summary" class="mb-1" width="98%">

</center>
+++
Details of the ALMA Band 6 observations. Footnote $^b$ refers to [step 2](../step2/step2-align-SBs.md).
````

### Long baseline data (C-6 configuration)

<style>
 .table_wrapper{
    display: block;
    overflow-x: auto;
    white-space: nowrap;
}
</style>

Below are further details on the TM1 scheduling block, compiled from a combination of the weblog and the QA reports. Note that you can scroll through this table horizontally.

````{card}
<div class="table_wrapper">
<table>

| <div style="width:250px">Execution Block</div>     | <div style="width:120px">Session</div> | <div style="width:250px">QA0 ExecBlock Status</div> | <div style="width:150px">QA0 Status</div> | <div style="width:250px">QA0 Comment</div>                   | <div style="width:700px">QA0 Warnings</div>                                                                                                                                       | <div style="width:150px">Exec Fraction</div> | <div style="width:80px">Band</div> | <div style="width:300px">Repr. Frequency (GHz, Sky)</div> | <div style="width:200px">Baselines (m)</div> | <div style="width:220px">Antennas (total)</div> | <div style="width:220px">Shadowing</div> | <div style="width:150px">PWV (mm)</div> | <div style="width:150px">PWV Octile</div> | <div style="width:150px">Tsys (OT, K)</div> | <div style="width:150px">Tsys (EB, K)</div> | <div style="width:250px">Start</div>           | <div style="width:250px">End</div>             | <div style="width:200px">Time on AB Aur (min)</div> | <div style="width:250px">Calibrators: Atmosphere</div> | <div style="width:250px">Calibrators: Bandpass</div> | <div style="width:200px">Calibrators: Flux</div> | <div style="width:200px">Calibrators: Phase</div> | <div style="width:200px">Calibrators: Pointing</div> | <div style="width:450px">Calibrators: WVR</div>                       | <div style="width:250px">Observe Check Source</div> |
|---------------------------|-------------|--------------------------|----------------|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------|--------------------------------|-------------------|----------------------|---------------|--------------|----------------|------------------|------------------|---------------------|---------------------|--------------------------|-----------------------------|---------------------------|-----------------------|------------------------|---------------------------|--------------------------------------------|--------------------------|
| uid___A002_Xfb8480_X6a5b  | 1           | SUCCESS                  | Pass           | Excellent conditions              | N/A                                                                                                                                                    | 1.5               | 6        | 220.392                        | 15-2617           | 41                   | 0.00%         | 0.24         | <1             | 116.5            | 65.4             | 2022-07-17 14:07:17 | 2022-07-17 15:25:26 | 47.37                    | J0510+1800, AB_Aur          | J0510+1800                | J0510+1800            | J0438+3004             | J0510+1800                | J0438+3004, J0510+1800, AB_Aur, J0435+2532 | J0435+2532               |
| uid___A002_Xfb8480_X178cb | 2           | SUCCESS                  | Pass           | The atmosphere was unstable       | Achieved angular resolution is outside the expected range. Observed:   0.13, requested: 0.14 - 0.22                                                    | 1.16              | 6        | 220.392                        | 15-2617           | 42                   | 1.11%         | 1.49         | 4-5            | 116.5            | 99.8             | 2022-07-19 12:02:10 | 2022-07-19 13:21:27 | 47.37                    | J0510+1800, AB_Aur          | J0510+1800                | J0510+1800            | J0438+3004             | J0510+1800                | J0438+3004, J0510+1800, AB_Aur, J0435+2532 | J0435+2532               |
| uid___A002_Xfbb255_X2286  | 3           | FAIL                     | Pass           | The atmosphere was. very unstable | Percentage of calibration data flagged: 0.010 %; Achieved angular   resolution is outside the expected range. Observed: 0.14, requested: 0.14 -   0.22 | 0.38              | 6        | 220.392                        | 15-2617           | 44                   | 0.00%         | 2.85         | 6-7            | 116.5            | 137              | 2022-07-20 14:03:55 | 2022-07-20 14:59:55 | 34.8                     | J0510+1800, AB_Aur          | J0510+1800                | J0510+1800            | J0438+3004             | J0510+1800                | J0438+3004, J0510+1800, AB_Aur, J0435+2532 | J0435+2532               |
| uid___A002_Xfbb9c7_X6731  | 4           | SUCCESS                  | Pass           | Very high atmosphere unstability  | Achieved angular resolution is outside the expected range. Observed:   0.13, requested: 0.14 - 0.22                                                    | 0.65              | 6        | 220.392                        | 15-2617           | 42                   | 0.00%         | 2.37         | 5-6            | 116.5            | 123.62           | 2022-07-21 14:01:35 | 2022-07-21 15:20:52 | 47.42                    | J0510+1800, AB_Aur          | J0510+1800                | J0510+1800            | J0438+3004             | J0510+1800                | J0438+3004, J0510+1800, AB_Aur, J0435+2532 | J0435+2532               |
| uid___A002_Xfbb9c7_Xd621  | 5           | SUCCESS                  | Pass           | The atmosphere was very unstable  | Percentage of calibration data flagged: 0.010 %; Achieved angular   resolution is outside the expected range. Observed: 0.14, requested: 0.14 -   0.22 | 1.5               | 6        | 220.392                        | 15-2617           | 44                   | 1.73%         | 0.84         | 2-3            | 116.5            | 81.444           | 2022-07-22 11:30:28 | 2022-07-22 12:49:58 | 47.33                    | J0510+1800, AB_Aur          | J0510+1800                | J0510+1800            | J0438+3004             | J0510+1800                | J0438+3004, J0510+1800, AB_Aur, J0435+2532 | J0435+2532               |
| uid___A002_Xfbb9c7_Xe05e  | 6           | SUCCESS                  | Pass           | The atmosphere. was unstable      | Achieved angular resolution is outside the expected range. Observed:   0.13, requested: 0.14 - 0.22                                                    | 1.5               | 6        | 220.392                        | 15-2617           | 41                   | 0.00%         | 0.63         | 1-2            | 116.5            | 73.95            | 2022-07-22 12:59:16 | 2022-07-22 14:18:16 | 47.42                    | J0510+1800, AB_Aur          | J0510+1800                | J0510+1800            | J0438+3004             | J0510+1800                | J0438+3004, J0510+1800, AB_Aur, J0435+2532 | J0435+2532               |

</table>
</div>

+++
&rarr;&rarr;&rarr; *This table scrolls horizontally* &rarr;&rarr;&rarr;

**AB_Aur_a_06_TM1: member.uid___A001_X15a2_Xb6b**.
````


### Short baseline data (C-3 configuration)

Below are further details on the TM2 scheduling block, compiled from a combination of the weblog and the QA reports. Note that you can scroll through this table horizontally.

````{card}
<div class="table_wrapper">
<table>

 | <div style="width:250px">Execution Block</div>     | <div style="width:120px">Session</div> | <div style="width:250px">QA0 ExecBlock Status</div> | <div style="width:150px">QA0 Status</div> | <div style="width:500px">QA0 Comment</div>                   | <div style="width:700px">QA0 Warnings</div>                                                                                                                                       | <div style="width:150px">Exec Fraction</div> | <div style="width:80px">Band</div> | <div style="width:300px">Repr. Frequency (GHz, Sky)</div> | <div style="width:200px">Baselines (m)</div> | <div style="width:220px">Antennas (total)</div> | <div style="width:220px">Shadowing</div> | <div style="width:150px">PWV (mm)</div> | <div style="width:150px">PWV Octile</div> | <div style="width:150px">Tsys (OT, K)</div> | <div style="width:150px">Tsys (EB, K)</div> | <div style="width:250px">Start</div>           | <div style="width:250px">End</div>             | <div style="width:200px">Time on AB Aur (min)</div> | <div style="width:250px">Calibrators: Atmosphere</div> | <div style="width:250px">Calibrators: Bandpass</div> | <div style="width:200px">Calibrators: Flux</div> | <div style="width:200px">Calibrators: Phase</div> | <div style="width:200px">Calibrators: Pointing</div> | <div style="width:450px">Calibrators: WVR</div>                       | <div style="width:250px">Observe Check Source</div> |
 |---------------------------|-------------|--------------------------|----------------|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------|--------------------------------|-------------------|----------------------|---------------|--------------|----------------|------------------|------------------|---------------------|---------------------|--------------------------|-----------------------------|---------------------------|-----------------------|------------------------|---------------------------|--------------------------------------------|--------------------------|
 | uid___A002_Xf7ad58_Xd406                                      | 1 | SUCCESS | Pass      | Some antennas shadowed due to high   declination (11.6%)                                                       | Percentage of calibration data flagged:   0.500 %                                                                                                      | 1.5 | 6 | 220.392 | 14-500 | 41  | 11.63% | 0.74 | 2-3 | 116.5 | 73   | 2022-04-19  7:25:22 | 2022-04-19  8:20:05 | 41   | J0510+1800, AB_Aur | J0510+1800 | J0510+1800 | J0438+3004 | J0510+1800 | J0438+3004, J0510+1800, AB_Aur | N/A |
 | uid___A002_Xf8d822_Xa976 (discarded by ALMA pipeline) | 2 | FAIL    | Semi-pass | APE2: 12m obs crash with 'Failed to handle an interface method   invocation'. no band set - problem in dataset | N/A                                                                                                                                                    | 0   | 6 | 220.392 | 15-500 | N/A | N/A    | 0.74 | 2-3 | N/A   | N/A  | N/A                 | N/A                 | 8.1  | J0510+1800, AB_Aur | J0510+1800 | J0510+1800 | J0438+3004 | J0510+1800 | J0438+3004, J0510+1800, AB_Aur | N/A |
 | uid___A002_Xf8f6a9_X15c79                                     | 3 | FAIL    | Pass      | DV 23 and DA54 presented issues. No other major issue.                                                         | Percentage of calibration data flagged: 0.020 %; Achieved angular   resolution is outside the expected range. Observed: 0.55, requested: 0.64 -   0.96 | 1.5 | 6 | 220.392 | 15-680 | 45  | 12.79% | 0.69 | 2-3 | 116.5 | 73.2 | 2022-05-15 18:05:13 | 2022-05-15 18:49:47 | 32.4 | J0510+1800, AB_Aur | J0510+1800 | J0510+1800 | J0438+3004 | J0510+1800 | J0438+3004, J0510+1800, AB_Aur | N/A |

 </table>
 </div>
+++
&rarr;&rarr;&rarr; *This table scrolls horizontally* &rarr;&rarr;&rarr;

**AB_Aur_a_06_TM2: member.uid___A001_X15a2_Xb6d**. The "second" execution block "uid___A002_Xf8d822_Xa976" was QA0 semi-pass, and was not included into the pipeline-delivered calibrated products. The QA0 comment (from the QA0 report) shows a fatal software error occurred and only 8 minutes of integration time on-source was achieved. We later looked at these data and considered re-running the pipeline calibration to include this EB, but in the end decided it was not worth it. The "third" execution block, "uid___A002_Xf8f6a9_X15c79", is thus what we move forward with as "SB EB2".
````

## Correlator Setup

Our correlator setup was designed for kinematic science.
We placed five spectral windows (SPWs) over the four available basebands to target four molecular emission lines and the continuum.  
````{card}
<center>

<img src="./images/correlator-setup.png" alt="correlator-setup" class="mb-1" width="98%">

</center>
+++
ALMA Band 6 correlator setup.
````

We centered one SPW at the $^{13}$CO $J=2-1$ molecular emission line transition rest frequency (220.405 GHz), covering a bandwidth of 58.594 MHz with 1920 channels, resulting in the highest achievable spectral resolution of 41.510 m/s after default spectral averaging with $N=2$ by Hanning smoothing within the correlator data processor. (This was our "representative" window in the OT.)

We placed a second SPW at the $^{12}$CO $J=2-1$ rest frequency (230.545 GHz) covering the same bandwidth with the same number of channels, achieving a slighty higher spectral resolution of 39.684 m/s (due to the higher center frequency, of course).

A third SPW was centered at the C$^{18}$O $J=2-1$ rest frequency (219.567 GHz), and a fourth at the SO $6(5)-5(4)$ rest frequency (219.956 GHz). Each of these SPWS covered the same bandwidth (58.594 MHz) but with *half* as many channels (960 channels) because they share a baseband. Thus they achieve a lower spectral resolution of 83.336 m/s and 83.189 m/s respectively.

To enable self-calibration, our correlator setup sampled the continuum in a fifth SPW centered at 233.012 GHz with 128 channels each 15.625 MHz in width, obtaining the full available 2.0 GHz bandwidth.

The weblog provides a detailed summary of the correlator setup.
````{card}
<center>

<img src="./images/spectral-setup.png" alt="spectral-setup" class="mb-1" width="98%">

</center>
+++
ALMA Band 6 correlator setup ("Science Windows" tab in the weblog).
````



## Pipeline Products

Each scheduling block (TM1 and TM2) was calibrated by the Cycle 8 ALMA pipeline. The final tasks in the pipeline additionally generate imaging products, which we can view to get an initial idea of what the observations show.

### Channel maps (TM1)

````{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/TM1_12CO.mp4" type="video/mp4" alt="pipeline_TM1_12CO">
</video>
<video width="49%" controls>
  <source src="../_static/videos/TM1_13CO.mp4" type="video/mp4" alt="pipeline_TM1_13CO">
</video>
<video width="49%" controls>
  <source src="../_static/videos/TM1_C18O.mp4" type="video/mp4" alt="pipeline_TM1_C18O">
</video>
<video width="49%" controls>
  <source src="../_static/videos/TM1_SO.mp4" type="video/mp4" alt="pipeline_TM1_SO">
</video>
</center>
+++
Pipeline-generated TM1 line images (task `hif_makeimages`).
````

### Channel maps (TM2)

````{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/TM2_12CO.mp4" type="video/mp4" alt="pipeline_TM2_12CO">
</video>
<video width="49%" controls>
  <source src="../_static/videos/TM2_13CO.mp4" type="video/mp4" alt="pipeline_TM2_13CO">
</video>
<video width="49%" controls>
  <source src="../_static/videos/TM2_C18O.mp4" type="video/mp4" alt="pipeline_TM2_C18O">
</video>
<video width="49%" controls>
  <source src="../_static/videos/TM2_SO.mp4" type="video/mp4" alt="pipeline_TM2_SO">
</video>
</center>
+++
Pipeline-generated TM2 line images (task `hif_makeimages`).
````


### Spectral line profiles

Our spectral windows cover a larger frequency range than the emission lines they target. It can be a good idea to take a look at what's happening throughout the whole spectral window though, which we do the quick way here by creating spectral line profiles integrated over the full field of view. Note the different y-axis scale.

````{card}
<center>

<img src="./images/pipeline_Zprofile_spw31.png" alt="12CO-pipeline-line-profile" class="mb-1" width="98%">
<img src="./images/pipeline_Zprofile_spw29.png" alt="13CO-pipeline-line-profile" class="mb-1" width="98%">
<img src="./images/pipeline_Zprofile_spw27.png" alt="C18O-pipeline-line-profile" class="mb-1" width="98%">
<img src="./images/pipeline_Zprofile_spw25.png" alt="SO-pipeline-line-profile" class="mb-1" width="98%">

</center>
+++
Spectral line profiles, integrated over the full FOV. TM1 and TM2 overlaid.
````

````{card}
<center>

<img src="./images/pipeline_Zprofile_allspws_TM1.png" alt="TM1-pipeline-line-profiles-comparison" class="mb-1" width="98%">
<img src="./images/pipeline_Zprofile_allspws_TM2.png" alt="TM2-pipeline-line-profiles-comparison" class="mb-1" width="98%">

</center>
+++
Spectral line profiles, integrated over the full FOV. All four molecules on the same scale.
````
