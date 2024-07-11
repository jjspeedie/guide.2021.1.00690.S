# Useful Dictionaries

The <a href="https://almascience.eso.org/almadata/lp/DSHARP/" target="_blank">DSHARP Large Program scripts</a>  (e.g. <a href="https://almascience.eso.org/almadata/lp/DSHARP/scripts/Elias27_continuum.py" target="_blank">Elias27_continuum.py</a>) start with the creation of a dictionary, ``data_params``, to store key information and keep things organized. The <a href="https://alma-maps.info/data.html" target="_blank">MAPS Large Program</a> imaging pipeline does a similar thing, but keeps the dictionaries in individual files (e.g. ``linedictionary.py``, ``diskdictionary.py``). I emulated these programs and employed the dictionaries below.

## Data dictionary

<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a>: Dictionary of data file names, paths, and properties used during reduction. This is a dictionary that you build up as you go along. It is especially useful for keeping track of the many measurement sets generated during each step leading up to the final MSes for imaging.

`````{admonition} **data_dict** is used for the following steps:
:class: tip
* [Step 1 - Prepare the continuum](../step1/step1-summary.md).
* [Step 2 - Phase alignment](../step2/step2-summary.md).
* [Step 3 - Self-calibration of the continuum](../step3/step3-summary.md).
* [Step 4 - Prepare the lines](../step4/step4-summary.md).
* [Imaging - Continuum](../imaging-cont/imaging-cont-procedure.md).
* [Imaging - Lines](../imaging-lines/imaging-lines-procedure.md).
`````

## Mask dictionary

<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_mask.py" target="_blank">dictionary_mask.py</a>: Dictionary of masking parameters for all lines and the continuum. In the case of the lines, it stores the parameters for <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/keplerian_mask.py" target="_blank">keplerian_mask.py</a>
(by <a href="https://github.com/richteague/keplerian_mask" target="_blank">Rich Teague</a>).


`````{admonition} **mask_dict** is used for the following steps:
:class: tip
* [Imaging - Continuum](../imaging-cont/imaging-cont-procedure.md).
* [Imaging - Lines](../imaging-lines/imaging-lines-procedure.md).
`````

## Line dictionary

<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_lines.py" target="_blank">dictionary_lines.py</a>: Dictionary of emission line properties and spectral parameters for line imaging. This dictionary also keeps track of the ~12 different sets of line images made while we were experimenting with our approach (``_v1``, ``_v2``, ``_v3`` etc; see [Initial Approaches](../imaging-lines/imaging-lines-initial-approaches.md)).

`````{admonition} **line_dict** is used for the following steps:
:class: tip
* [Imaging - Lines](../imaging-lines/imaging-lines-procedure.md).
`````

## Disk dictionary

<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a>: Dictionary of physical properties of the AB Aur system. This dictionary comes in handy for generation of Keplerian masks for the line imaging, and later during science it's a nice place to store the physical disk parameters for many different uses.

`````{admonition} **disk_dict** is used for the following steps:
:class: tip
* [Imaging - Lines](../imaging-lines/imaging-lines-procedure.md).
`````
