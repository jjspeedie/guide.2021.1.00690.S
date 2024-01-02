`````{admonition} The tasks in this chapter use the following scripts:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step2_phase_alignment.py" target="_blank">step2_phase_alignment.py</a> # main script (using modular CASA)
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- alignment.py # exoALMA visibility alignment functions (not yet public)
`````
<!-- https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/alignment.py -->

# Align Short-Baseline Execution Blocks

In order to increase the chances of overlap (i.e. increase the number of grid cells containing visibility points from both the reference and comparison ms), we concatenate all six LB EBs together, and use the concatenation as the reference measurement set to which to align the SB executions.

## SB EB1

```{image} images/ABAur_SB_EB1_initcont_selfcal.ms_alignment_uv_grid.png
:alt: ABAur_SB_EB1_initcont_selfcal.ms_alignment_uv_grid
:class: mb-1
:width: 100%
:align: center
```

## SB EB2

```{image} images/ABAur_SB_EB2_initcont_selfcal.ms_alignment_uv_grid.png
:alt: ABAur_SB_EB2_initcont_selfcal.ms_alignment_uv_grid
:class: mb-1
:width: 100%
:align: center
```

Again, after aligning the EBs, we rerun the code on the aligned EBs to check that their offsets are small (i.e. a fraction of a cell size).
