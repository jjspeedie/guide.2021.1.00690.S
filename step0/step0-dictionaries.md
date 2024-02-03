# Useful Dictionaries

## Data dictionary

Dictionary of data file names, paths, and properties used during reduction.

## Line dictionary

Dictionary of emission line properties and spectral parameters for imaging.

## Mask dictionary

Dictionary of masking parameters for all lines and the continuum.

## Disk dictionary

Dictionary of physical properties of the AB Aur system for many different uses.
When applicable/possible, I've tried to cite the *original* paper who found each value.


step 1
dictionary_data.py # loads data_dict

step 2
dictionary_data.py # loads data_dict

step 3
dictionary_data.py # loads data_dict

step 4
dictionary_data.py # loads data_dict

imaging cont
dictionary_mask.py # loads mask_dict
dictionary_data.py # loads data_dict

imaging lines
dictionary_mask.py # loads mask_dict
dictionary_data.py # loads data_dict
dictionary_disk.py # loads disk_dict
mport dictionary_lines as dlines # contains line_dict
