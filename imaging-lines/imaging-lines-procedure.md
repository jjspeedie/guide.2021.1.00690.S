`````{admonition} Scripts for **Imaging - Lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/major_image_lines.py" target="_blank">major_image_lines.py</a> # main script ([adopted approach](imaging-lines-adopted-approach.md))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/image_lines.py" target="_blank">image_lines.py</a> # earlier main script ([initial approaches](imaging-lines-initial-approaches.md))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_mask.py" target="_blank">dictionary_mask.py</a> # loads mask_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a> # loads disk_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_lines.py" target="_blank">dictionary_lines.py</a> # loads line_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/JvM_correction_casa6.py" target="_blank">JvM_correction_casa6.py</a> # MAPS JvM correction script ([Czekala et al. 2021](https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/keplerian_mask.py" target="_blank">keplerian_mask.py</a> # modified version of [keplerian_mask](https://github.com/richteague/keplerian_mask) by [Rich Teague](https://richteague.github.io/)

````{card} And data (obtained after [step 4](../step4/step4-line-mses-achieved.md)):
- <a href="https://www.canfar.net/storage/vault/list/jspeedie/2021.1.00690.S/private/measurement_sets" target="_blank">ABAur_12CO.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/jspeedie/2021.1.00690.S/private/measurement_sets" target="_blank">ABAur_13CO.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/jspeedie/2021.1.00690.S/private/measurement_sets" target="_blank">ABAur_C18O.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/jspeedie/2021.1.00690.S/private/measurement_sets" target="_blank">ABAur_SO.bin30s.ms.contsub</a>
`````

# Procedure


````{card}

```{image} images/line_imaging_procedure.jpg
:alt: line_imaging_procedure
:class: mb-1
:width: 100%
:align: center
```
+++
caption
````

## Velocity Regridding and Channel Selection

Note [dirty images](imaging-lines-dirty-images) and [initial approaches](imaging-lines-initial-approaches.md) were done on cvel2 data. [adopted approach](imaging-lines-adopted-approach.md) was done without cvel2.
