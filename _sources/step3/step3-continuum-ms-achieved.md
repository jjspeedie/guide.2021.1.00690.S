`````{admonition} Scripts for **Step 3 - Self-calibration of the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step3_continuum_selfcal.py" target="_blank">step3_continuum_selfcal.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # selfcal functions
`````

# Create Final Continuum Measurement Set

To save storage space, we now time average to 30 seconds. This does nothing to affect the data, so long as it's done after self-calibration (because we want to get as low ``solint`` as possible, and because time-binning changes the weights which can make ``plotms`` wonky).

````python
""" Save the final MS """
chosenvis          = data_dict['NRAO_path']+data_dict['BB_concat']['contp0'].replace('p0.ms', 'ap.ms')
final_cont_ms      = 'ABAur_continuum.bin30s.ms'
split(vis=chosenvis, outputvis=final_cont_ms, spw='', timebin='30s', datacolumn='data')
listobs(vis=final_cont_ms, listfile=final_cont_ms+'.listobs.txt')
os.system('tar cvzf backups/' + final_cont_ms+'.tgz ' + final_cont_ms)
````

<div style="background-color:#FAE5D3;">

````{card} Final continuum measurement set achieved! 🥳

* **ABAur_continuum.bin30s.ms (524 MB)**

(Available to download soon)

````
</div>
