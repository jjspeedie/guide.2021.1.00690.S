`````{admonition} Scripts for **Step 2 - Phase alignment**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step2_phase_alignment.py" target="_blank">step2_phase_alignment.py</a> # main script (using modular CASA)
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- alignment.py # exoALMA visibility alignment functions (not yet public)
`````
<!-- https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/alignment.py -->

# Summary of Phase Shifts

````{card}
<center>

<img src="images/phase-alignment-table.png" alt="images/phase-alignment-table" class="mb-1" width="100%">

</center>
+++
caption
````


Out of interest, here are how the values of the required offsets look on the sky, in comparison to the init_cont beam of each EB. The numbers written next to each beam are [the hypotenuse of the deltaRA-deltaDec offset]/[the beam minor axis]. So the required offsets range 8-21% of a beam minor axis for the LB EBs, and 6-40% of a beam for the SB EBs. The offset for SB EB2 (yellow) was definitely noticeable in the init_cont images.


````{card}
<center>

<img src="images/offsets.png" alt="images/offsets" class="mb-1" width="85%">

</center>
+++
caption
````
