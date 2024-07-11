# Step 2 Overview & Scripts

In this step, we align the phase centers of all execution blocks to a common phase center, using the source's continuum morphology and assuming it is not variable in time.


`````{admonition} Scripts for **Step 2 - Phase alignment**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step2_phase_alignment.py" target="_blank">step2_phase_alignment.py</a> # main script (using modular CASA)
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://www.exoalma.com/home" target="_blank">alignment.py</a> # exoALMA visibility alignment functions
- <a href="https://www.exoalma.com/home" target="_blank">example_alignment_usage.py</a> # exoALMA alignment example  
`````
<!-- https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/alignment.py -->

````{card}

<img src="images/breakdown-of-task.png" alt="breakdown-of-step2" class="mb-1" width="100%">

````


[Align Long-Baseline Execution Blocks](step2-align-LBs.md): We selected one of the long-baseline execution blocks to serve as the reference EB, to whose phase center all other EBs are aligned. The LB1 execution block (phase center: ``J2000 04:55:45.854900 +30.33.03.73320``; observed 2022-07-17) was chosen as the reference EB as it was observed in the most favorable weather conditions and had the highest SNR in the [initial images](../step1/step1-initial-continuum-images.md).

[Align Short-Baseline Execution Blocks](step2-align-SBs.md): This procedure was repeated to align the two short-baseline EBs to the common phase center, this time taking the aligned concatenated long-baseline dataset as the reference in order to maximize the potential for overlap of *uv* points in the common grid. We then concatenated the shifted short-baseline EBs into a single phase-aligned short-baseline dataset.  

[Summary of Phase Shifts](step2-summary-of-shifts.md): A summary of the applied phase shifts.
