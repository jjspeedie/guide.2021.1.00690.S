`````{admonition} The tasks in this chapter use the following scripts:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_prepare_lines.py" target="_blank">step4_prepare_lines.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_detour.py" target="_blank">step4_detour.py</a> # for phase alignment
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a> # loads disk_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://casaguides.nrao.edu/index.php/Analysis_Utilities" target="_blank">analysisUtils (analysis_scripts/)</a> # for channel strings
`````

# Apply Self-Calibration Solutions

It would be most intuitive to concatenate the SB line data, and then concatenate that SB data with the LB data, and apply the self calibration tables to those two giant measurement sets. However, at this point, we have just 1.2 TB left of disk space on cvpost, and each line ms is ~50 GB. Not only would concatenating use up a lot of diskspace, it would also take a lot of time to apply the phase solutions to the giant concatenation. As such, Ryan recommended we keep the data in their separate execution blocks, and then at the very end, split out each spectral window and combine the corresponding spectral windows across executions.


The difficulty we thus face is: We generated our self calibration tables using (SB EB1 + SB EB2), and (SB EB1 + SB EB2 + LB EB1 + LB EB2 +LB EB3 + LB EB4 +LB EB5 + LB EB6). This means that each calibration table is big, and contains solutions for all those EBs. But we now want to apply each calibration table to only a subset of the data it was generated with. In other words, although the SB calibration tables have solutions for SB EB1 and SB EB2, we want to only apply the solutions for SB EB1 to the SB EB1 line ms, and then separately apply the solutions for SB EB2 to the SB EB2 line ms. How do we do that?
