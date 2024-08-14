`````{admonition} Scripts for **Step 2 - Phase alignment**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step2_phase_alignment.py" target="_blank">step2_phase_alignment.py</a> # main script (using modular CASA)
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://www.exoalma.com/home" target="_blank">alignment.py</a> # exoALMA visibility alignment functions
`````
<!-- https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/alignment.py -->

# Summary of Phase Shifts

Here is a table of the results compiled from the previous two pages.

````{card}
<center>

<img src="images/phase-alignment-table.png" alt="images/phase-alignment-table" class="mb-1" width="100%">

</center>
+++
Each row pertains to a single EB-EB comparison. The grey-coloured MSes are ones that have been shifted; those rows are the "checks" where we expect the offsets to be small. When the reference and comparison MSes are the same MS (as in the top row), the offset is zero.
````


Here's a visualization of the values of the required offsets on the sky, in comparison to the size of the [initial continuum image](../step1/step1-initial-continuum-images.md) beam of each EB. The numbers written next to each beam are ``[the hypotenuse of the deltaRA-deltaDec offset]/[the beam minor axis]``. The required offsets range 8-21% of a beam minor axis for the LB EBs, and 6-40% of a beam for the SB EBs.


````{card}
<center>

<img src="images/offsets.png" alt="images/offsets" class="mb-1" width="85%">

</center>
````

The offset for SB EB2 (yellow in the above figure) was definitely noticeable in the [initial continuum images](../step1/step1-initial-continuum-images.md):

````{card}
<center>

<img src="images/SBEB1-SBEB2-blink.gif" alt="images/SBEB1-SBEB2-blink" class="mb-1" width="65%">

</center>
````
