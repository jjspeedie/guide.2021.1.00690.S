`````{admonition} Scripts for **Step 4 - Prepare the lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_prepare_lines.py" target="_blank">step4_prepare_lines.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_detour.py" target="_blank">step4_detour.py</a> # for phase alignment
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://casaguides.nrao.edu/index.php/Analysis_Utilities" target="_blank">analysisUtils (analysis_scripts/)</a> # for channel strings
`````

# Create Final Line Measurement Sets

Finally, we split out the individual spectral windows from each EB, and then combine them across EBs. We do this for both the continuum-subtracted and non-continuum-subtracted data, accounting for the new SPW-indexing in the former:

```python
""" First do non-continuum-subtracted ms's """
for spwi,molecule in enumerate(molecules):
    ms_list_to_concatenate = []
    for EB in data_dict['EBs']:
        ms_list_to_concatenate.append(data_dict['NRAO_path']+data_dict[EB]['_initlines_selfcal.ms'].replace('.ms', '_spw'+str(spwi)+'.ms'))

    print('For molecule: ', molecule)
    print('Combining spectral window '+str(spwi)+' across these measurement sets:', ms_list_to_concatenate)

    final_line_ms = 'ABAur_'+molecule+'.bin30s.ms'

    os.system('rm -rf %s*' % final_line_ms)
    concat(vis          = ms_list_to_concatenate,
           concatvis    = final_line_ms,
           dirtol       = '0.1arcsec',
           copypointing = False)
    listobs(vis=final_line_ms, listfile=final_line_ms+'.listobs.txt')
    os.system('tar cvzf backups/' + final_line_ms+'.tgz ' + final_line_ms)

""" Second do continuum-subtracted ms's (contains spws 0,1,2,3) """
for spwi,molecule in enumerate(molecules):
    ms_list_to_concatenate = []
    for EB in data_dict['EBs']:
        ms_list_to_concatenate.append(data_dict['NRAO_path']+data_dict[EB]['_initlines_selfcal.ms'].replace('.ms', '_spw'+str(spwi)+'.ms')+'.contsub')

    print('For molecule: ', molecule)
    print('Combining spectral window '+str(spwi)+' across these measurement sets:', ms_list_to_concatenate)

    final_line_ms = 'ABAur_'+molecule+'.bin30s.ms.contsub'

    os.system('rm -rf %s*' % final_line_ms)
    concat(vis          = ms_list_to_concatenate,
           concatvis    = final_line_ms,
           dirtol       = '0.1arcsec',
           copypointing = False)
    listobs(vis=final_line_ms, listfile=final_line_ms+'.listobs.txt')
    os.system('tar cvzf backups/' + final_line_ms+'.tgz ' + final_line_ms)
```

<!-- (I tried to follow the file naming conventions of the MAPS datasets.) -->

<div style="background-color:#e1f2fc;">

````{card} Final line measurement sets achieved! 🥳
Continuum-subtracted spectral line measurement sets:

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_12CO.bin30s.ms.contsub (13.5 GB)</a>**

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_13CO.bin30s.ms.contsub (13 GB)</a>**

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_C18O.bin30s.ms.contsub (6.9 GB)</a>**

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_SO.bin30s.ms.contsub (6.8 GB)</a>**

Non-continuum-subtracted spectral line measurement sets:

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_12CO.bin30s.ms (13.5 GB)</a>**

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_13CO.bin30s.ms (13 GB)</a>**

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_C18O.bin30s.ms (6.9 GB)</a>**

* **<a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_SO.bin30s.ms (6.8 GB)</a>**

````
</div>
