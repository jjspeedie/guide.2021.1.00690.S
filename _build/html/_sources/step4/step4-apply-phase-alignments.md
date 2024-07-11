`````{admonition} Scripts for **Step 4 - Prepare the lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_prepare_lines.py" target="_blank">step4_prepare_lines.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_detour.py" target="_blank">step4_detour.py</a> # for phase alignment
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://casaguides.nrao.edu/index.php/Analysis_Utilities" target="_blank">analysisUtils (analysis_scripts/)</a> # for channel strings
`````

# Apply Phase Shifts

In [Step 2](../step2/step2-summary-of-shifts.md), we used the continuum to compute the phase shifts necesssary to align our execution blocks. Here we simply take those pre-computed offsets and apply those same shifts to the line MSes. We take a "detour" from the main <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_prepare_lines.py" target="_blank">step4_prepare_lines.py</a> script to the <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_detour.py" target="_blank">step4_detour.py</a> in order to work in modular CASA. We again do the alignments in two steps (long baseline data, then short baseline data), though we could have fed in all MSes in one call.

## Align Long-Baseline Execution Blocks

````{card}
| EB      | R.A. offset (arcsec) | Dec. offset (arcsec) |
|---------|----------|-----------|
|     LB EB 1 |     0 (ref)         |     0 (ref)        |
|     LB EB 2 |     -0.0198       |     +0.0047      |
|     LB EB 3 |     -0.0127       |     +0.0013       |
|     LB EB 4 |     +0.0237       |     -0.0219      |
|     LB EB 5 |     -0.0207      |     -0.0105       |
|     LB EB 6 |     -0.0046     |     -0.0276        |
+++
**Long baseline execution blocks:** Phase offsets between the phase center of each EB and the reference (LB EB1) found in [Step 2](../step2/step2-align-LBs.md).
````



1. **Select the reference execution block.** We are not *computing* any phase offsets here, but the code requires feeding in a reference.

```python
reference_for_LB_alignment  = ddata.data_dict['LB_EB1']['_initlines.ms']
```

It's not necessary to specify the continuum spectral window ID or set the grid this time.

2. **Set the offsets to be applied (from [Step 2](../step2/step2-summary-of-shifts.md)).**

```python
alignment_offsets   = []
#insert offsets from the alignment output
alignment_offsets.append([0,0])
alignment_offsets.append([-0.019783,0.0046808])
alignment_offsets.append([-0.012707,0.001336])
alignment_offsets.append([0.023685,-0.021869])
alignment_offsets.append([-0.020729,-0.01054])
alignment_offsets.append([-0.0045512,-0.0276])
```

3. **Apply the shifts.**

```python
alignment.align_measurement_sets(reference_ms       = reference_for_LB_alignment,
                                 align_ms           = offset_LB_EBs,
                                 align_offsets      = alignment_offsets)
```

4. **Check that it worked.** The "RA", "Decl" and "Epoch" columns in each EB's listobs should be "04:55:45.854900 +30.33.03.73320 J2000".

```python
"""Check that the phase center of each EB is: 04:55:45.854900 +30.33.03.73320 J2000"""
for EB in ddata.data_dict['LB_EBs']:
    vis          = ddata.data_dict['NRAO_path']+ddata.data_dict[EB]['_initlines_shift.ms']
    casatasks.listobs(vis=vis, listfile=vis+'.listobs.txt')
```

## Align Short-Baseline Execution Blocks

````{card}
| EB      | R.A. offset (arcsec) | Dec. offset (arcsec) |
|---------|----------|-----------|
|     LB EB 1 |     (ref)         |     (ref)        |
|     SB EB 1 |     -0.0131       |     +0.0395        |
|     SB EB 2 |     +0.1192        |     -0.1922       |
+++
**Short baseline execution blocks:** Phase offsets between the phase center of each EB and the reference (LB EB1) found in [Step2](../step2/step2-align-LBs.md).
````

5. **Repeat the above steps 1-4 but with the SB phase offsets and SB MSes.**

```python
alignment_offsets   = []
#insert offsets from the alignment output
alignment_offsets.append([-0.013133,0.03949])
alignment_offsets.append([0.11922,-0.19222])

alignment.align_measurement_sets(reference_ms       = reference_for_SB_alignment,
                                 align_ms           = offset_SB_EBs,
                                 align_offsets      = alignment_offsets)
```
