# Step 1 Overview & Scripts

In this step, we begin our post-processing of the continuum.

`````{admonition} Scripts for **Step 1 - Prepare the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_prepare_continuum.py" target="_blank">step1_prepare_continuum.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # necessary for an initial round of selfcal at the end
`````

````{card}

<img src="images/breakdown-of-task.png" alt="breakdown-of-step1" class="mb-1" width="100%">

````

[Manual Flagging](step1-manual-flags.md): Before we do anything, we should identify data we want to flag out, if any. During inspection of the weblog, we had seen some flaggable issues (bad antennas). But they were deemed not too serious, and we opted to rely on self calibration to fix them.

[Pseudo-continuum Measurement Sets](step1-pseudo-continuum.md): We create pseudo-continuum datasets by flagging the line emission in each line SPW and spectrally averaging. "Pseudo-continuum"
We use the DSHARP function ``get_flagchannels`` to find the channels containing line emission in each SPW. In order to maximize the retained bandwidth (and achieve high SNR for per-SPW self calibration at a later step), we flagged channels $\pm 6$ km/s from the $^{13}$CO $J=2-1$ line center, and $\pm 4$ km/s from the C$^{18}$O $J=2-1$ line center. While these velocity ranges are narrower than the $\pm 15$ km/s and $\pm 25$ km/s velocity ranges flagged by {\sc MAPS} and {\sc DSHARP}, respectively, we confirmed that they capture all tail emission with a buffer of $\geq1$ km/s by imaging the cubes and visually inspecting the channels.  
The continuum SPWs were spectrally averaged into 250 MHz channels (8 bins), whereas the line SPWs were averaged into a single 58.594 MHz channel (equal to the SPW bandwidth).

[Initial Continuum Images](step1-initial-continuum-images.md):

[Initial Self-Calibration](step1-initial-self-calibration.md):
To prepare each dataset for phase alignment, we
<!-- %we followed the philosophy of \texttt{exoALMA} and combined the SPWs in each EB and -->
performed an initial single round of phase self-calibration on each EB separately.
<!-- % This was made possible by the high SNR of the data -->
We obtained the initial model by imaging each EB shallowly and interactively with
<!-- %the result of shallowly and interactively \texttt{CLEAN}ing each EB with  -->
Hogdom deconvolution\cite{hogbom1974} ($\delta$-function clean components). This initial round of self calibration increased the SNR in all EBs and visually improved the images.
