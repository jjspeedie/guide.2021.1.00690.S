`````{admonition} Scripts for **Step 4 - Prepare the lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_prepare_lines.py" target="_blank">step4_prepare_lines.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_detour.py" target="_blank">step4_detour.py</a> # for phase alignment
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://casaguides.nrao.edu/index.php/Analysis_Utilities" target="_blank">analysisUtils (analysis_scripts/)</a> # for channel strings
`````

# Averaging Down the Continuum

Here, we want the exact opposite result as in [Pseudo-continuum Measurement Sets](../step1/step1-pseudo-continuum.md).

We return to working with our very [initial measurement sets](../step0/step0-restoring-pipeline-calibration.md), the ``uid*.ms.split.cal.source`` measurement sets (eight in total, one for each EB). For each EB, we "get rid" of the continuum spectral window (SPW 0) by averaging it down to a single channel, using the ``split`` task and ``width`` list argument. Since our continuum SPW has 128 channels, we average over 128 channels. The continuum SPW will come with us (in its averaged-down state) for the rest of the Step 4 journey, until we eventually split out individual spectral windows and combine them across EBs to create the [final line MSes](step4-line-mses-achieved.md).

`````{tab-set}

````{tab-item} Relevant lines in step4_prepare_lines.py

```python
split(vis         = inputvis,
      field       = 'AB_Aur',
      spw         = data_dict[EB]['cont_spws'], # in hindsight, poorly named; this includes all spws
      outputvis   = outputvis,
      width       = data_dict[EB]['line_width_array'], # averages the cont spw (0) down to 1 channel, and keeps the line spws as they are
      datacolumn  = 'data',
      keepflags   = False)
print("Spectrally averaged continuum dataset saved to %s" % outputvis)
```
````

````{tab-item} Relevant lines in dictionary_data.py

```python
"""######### Parameter choices for Step 1 #########"""

'''For spectral averaging: Spectral windows to be included (all of them). spw 0 is the only pure-continuum spw though'''
cont_spws       = '0, 1, 2, 3, 4'

"""######### Parameter choices for Step 4 #########"""

'''For extracting the spectral lines: We average the continuum spw down, and do no averaging on the line spectral windows'''
line_width_array = [128, 1, 1, 1, 1] # number of channels to average together
```

````

`````
