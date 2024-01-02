`````{admonition} The tasks in this chapter use the following scripts:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step3_continuum_selfcal.py" target="_blank">step3_continuum_selfcal.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a> # loads disk_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # selfcal functions
`````

# Create final continuum measurement set

To save storage space, we now time average to 30 seconds. This apparently does nothing to hurt/affect the data, so long as it's done after self-calibration (because we want to get as low solint as possible, and because time-binning changes the weights which can make plotms wonky).

`````{admonition} Achieved!
:class: tip
#######################################################################
#################### Continuum measurement set ########################
#######################################################################

  524 MB	      ABAur_continuum.bin30s.ms
`````

<!-- >#######################################################################
>#################### Continuum measurement set ########################
>#######################################################################
>
>  524 MB	      ABAur_continuum.bin30s.ms -->

<!-- ````{card}
Content of the top card.

{bdg-primary}`example-badge`

````

```{card}
Jess might add here: Figures showing inspection of flux recovery.
```


```{glue} sorted_means_fig
:doc: executable/output-insert.md
``` -->
