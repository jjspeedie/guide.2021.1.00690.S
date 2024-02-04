`````{admonition} Scripts for **Step 1 - Prepare the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_prepare_continuum.py" target="_blank">step1_prepare_continuum.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # necessary for an initial round of selfcal at the end
`````

# Manual Flagging

There are some flaggable issues we identified during inspection of the weblog, namely bad antennas during Tsys measurements in both the SB and LB data. For example:

<img src="images/tsys-eg1-uid___A002_Xfbb255_X2286.ms.h_tsyscal.s6_3.tsyscal.tbl-tsys_vs_freq-time.DV17.spw23.png" alt="tsys-eg1" class="bg-primary mb-1" width="49%">
<img src="images/tsys-eg2-tsys-uid___A002_Xf8f6a9_X15c79.ms-summary.spw21.png" alt="tsys-eg2" class="bg-primary mb-1" width="49%">


However, the guidance I was given is that self calibration will take care of them for us. As such, I'll neglect any manual flagging for now.
