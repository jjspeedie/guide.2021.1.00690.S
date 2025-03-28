# Step 3 Overview & Scripts

In this step, we self-calibrate the continuum and obtain the final continuum measurement set.

````{dropdown} Self calibration is like shimmying up a chimney.
<center>

<img src="images/selfcal-meme.png" alt="selfcal-meme" class="mb-1" width="35%">

</center>
````

`````{admonition} Scripts for **Step 3 - Self-calibration of the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step3_continuum_selfcal.py" target="_blank">step3_continuum_selfcal.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # selfcal functions
`````

````{card}

<img src="images/breakdown-of-task.png" alt="breakdown-of-step3" class="mb-1" width="100%">

````

[Self-Calibration of Short-Baseline Execution Blocks](step3-selfcal-SBs.md): Self-calibration started with the (phase-aligned and concatenated) short-baseline continuum data. We performed a series of phase-only self-calibration iterations, decreasing the solution interval in succession: ``inf, 243s, 120s, 60s, 30s, 18s``. We avoided combining by SPW in the first two rounds to remove any potential per-SPW phase offsets. Between iterations, we updated the model by imaging the data interactively and conservatively with <a href="https://ui.adsabs.harvard.edu/abs/1974A%26AS...15..417H/abstract" target="_blank">Hogbom</a> deconvolution and a Briggs ``robust`` parameter of ``0.5``, setting the ``gain`` parameter to ``0.05`` to guard against cleaning too deeply in a given major cycle. We used a circular clean mask of $3''$ radius, centered on the new common phase center.
We estimated the noise in the CLEAN image within a centered annulus with inner and outer radius $6''$ and $10''$, respectively. We concluded the phase-only self-calibration sequence when the peak SNR increased by a factor less than $10\%$ and the image quality did not visually improve. We then carried out one round of amplitude and phase self-calibration with the solution interval equal to a scan length (``486s``), which improved the peak SNR by $5\%$. Overall, the entire self-calibration process resulted in an increase in the peak SNR of the short-baseline dataset by a factor of $2.2$; the resulting noise was $35\, \mu$Jy/beam ($1.35$ mK) for a $630 \times 930$ mas beam. We concatenated the (newly self-calibrated) short-baseline dataset with the (not self-calibrated, but phase aligned) long-baseline dataset from [from Step 2](../step2/step2-align-LBs.md) and proceeded to self-calibrate the combined dataset.

[Self-Calibration of SB+LB Data](step3-selfcal-SBs+LBs.md): An initial round of per-SPW phase self-calibration was attempted but yielded too many flagged solutions due to low SNR. We started with a solution interval of ``900s`` and stepped down to ``360s``, ``180s`` and ``60s`` before performing one round of amplitude and phase self-calibration (again on a scan length). Overall, this second self-calibration process resulted in peak SNR increase by a factor of $1.6$. The estimated noise was $17.4 \, \mu$Jy/beam (4.2 mK) for a $260\times 360$ mas beam.

[Create Final Continuum Measurement Set](step3-continuum-ms-achieved.md): The final continuum MS is time averaged to 30 seconds to save space.
