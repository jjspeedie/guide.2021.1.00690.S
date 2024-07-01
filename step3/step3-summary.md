# Step 3 Overview & Scripts

`````{admonition} Scripts for **Step 3 - Self-calibration of the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step3_continuum_selfcal.py" target="_blank">step3_continuum_selfcal.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # selfcal functions
`````

[Self-Calibration of Short-Baseline Execution Blocks](step3-selfcal-SBs.md): Self-calibration started with the (phase-aligned and concatenated) short-baseline continuum data. We performed a series of phase-only self-calibration iterations, decreasing the solution interval in succession: inf, 243s, 120s, 60s, 30s, 18s. We avoided combining by SPW in the first two rounds to remove any potential per-SPW phase offsets. Between iterations, we updated the model by imaging the data interactively and conservatively with Hogbom deconvolution\cite{hogbom1974} and a Briggs robust parameter of 0.5, setting the \texttt{gain} parameter to $0.05$ to guard against cleaning too deeply in a given major cycle. We used a circular clean mask of $3''$ radius, centered on the new common phase center. %  $3''$ in radius.
We estimated the noise in the \texttt{CLEAN} image within a centered annulus with inner and outer radius $6''$ and $10''$, respectively. We concluded the phase-only self-calibration sequence when the peak SNR increased by a factor less than $10\%$ and the image quality did not visually improve. We then carried out one round of amplitude and phase self-calibration with the solution interval equal to a scan length (486s), which improved the peak SNR by a factor of $5\%$. Overall, the entire self-calibration process resulted in an increase in the peak SNR of the short-baseline dataset by a factor of $2.2$; the resulting noise was $35\, \mu$Jy/beam ($1.35$ mK) for a $630 \times 930$ mas beam.

We concatenated the (newly self-calibrated) short-baseline dataset with the (not self-calibrated, but phase aligned) long-baseline dataset and proceeded to self-calibrate the combined dataset.
To avoid a bug\footnote{Error in Calibrater::solve: Mismatch between Solution frequencies and existing CalTable frequencies. Documented in \url{https://github.com/e-merlin/eMERLIN_CASA_pipeline/issues/70}} in the \texttt{gaincal} task %\js{I believe this is documented officially, somewhere}
in {\sc CASA} 6.2.1, it was necessary to switch to {\sc CASA} 6.4.1.

[Self-Calibration of SB+LB Data](step3-selfcal-SBs+LBs.md): An initial round of per-SPW phase self-calibration was attempted but yielded too many flagged solutions due to low SNR. We started with a solution interval of 900s and stepped down to 360s, 180s and 60s before performing one round of amplitude and phase self-calibration (again on a scan length). This second self-calibration process resulted in peak SNR increase by a factor of $1.6$. The estimated noise was $17.4 \, \mu$Jy/beam (4.2 mK) for a $260\times 360$ mas beam. 

[Create Final Continuum Measurement Set](step3-continuum-ms-achieved.md):
