`````{admonition} Scripts for **Step 4 - Prepare the lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_prepare_lines.py" target="_blank">step4_prepare_lines.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step4_detour.py" target="_blank">step4_detour.py</a> # for phase alignment
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://casaguides.nrao.edu/index.php/Analysis_Utilities" target="_blank">analysisUtils (analysis_scripts/)</a> # for channel strings
`````

# Continuum Subtraction

We perform continuum subtraction in *uv*-space with CASA task ``uvcontsub``.

Channels used to fit the continuum are the inverse of those used to flag the spectral lines in [Pseudo-continuum Measurement Sets](../step1/step1-pseudo-continuum.md). We again use the DSHARP function ``get_flagchannels`` (<a href="https://almascience.eso.org/almadata/lp/DSHARP/scripts/reduction_utils.py" target="_blank">reductions_utils.py</a>) using the same velocity ranges selected in [Step 1](../step1/step1-pseudo-continuum.md), and then "flip" them using the <a href="https://casaguides.nrao.edu/index.php/Analysis_Utilities" target="_blank">analysisUtils</a> function ``invertChannelRanges``:

`````{tab-set}

````{tab-item} Relevant lines in step4_prepare_lines.py

```python
flagchannels_string = get_flagchannels(ms_file          = inputvis,
                                       ms_dict          = data_dict[EB],
                                       velocity_range   = data_dict[EB]['velocity_ranges'])
fitspw = au.invertChannelRanges(flagchannels_string, vis=inputvis)
```
````

````{tab-item} Relevant lines in dictionary_data.py

```python
velocity_ranges = np.array([np.array([ddisk.disk_dict['v_sys']-3., ddisk.disk_dict['v_sys']+3.]),
                            np.array([ddisk.disk_dict['v_sys']-4., ddisk.disk_dict['v_sys']+4.]),
                            np.array([ddisk.disk_dict['v_sys']-6., ddisk.disk_dict['v_sys']+6.]),
                            np.array([ddisk.disk_dict['v_sys']-10., ddisk.disk_dict['v_sys']+10.])])
```

````

`````

Here are the resulting channels in each spectral window to be used by ``uvcontsub`` to fit the continuum, formatted as the necessary strings:

```console
Flagchannels input string for SB_EB1: '1:517~589,       2:504~600,       3:961~1251,        4:556~1059'
                              fitspw:  1:0~516;590~959, 2:0~503;601~959, 3:0~960;1252~1919, 4:0~555;1060~1919
Flagchannels input string for SB_EB2: '1:517~589,       2:504~600,       3:962~1251,        4:554~1058'
                              fitspw:  1:0~516;590~959, 2:0~503;601~959, 3:0~961;1252~1919, 4:0~553;1059~1919
Flagchannels input string for LB_EB1: '1:516~589,       2:504~600,       3:960~1249,        4:553~1057'
                              fitspw:  1:0~515;590~959, 2:0~503;601~959, 3:0~959;1250~1919, 4:0~552;1058~1919
Flagchannels input string for LB_EB2: '1:517~589,       2:504~600,       3:960~1249,        4:553~1057'
                              fitspw:  1:0~516;590~959, 2:0~503;601~959, 3:0~959;1250~1919, 4:0~552;1058~1919
Flagchannels input string for LB_EB3: '1:517~589,       2:505~601,       3:960~1249,        4:553~1057'
                              fitspw:  1:0~516;590~959, 2:0~504;602~959, 3:0~959;1250~1919, 4:0~552;1058~1919
Flagchannels input string for LB_EB4: '1:516~589,       2:504~600,       3:960~1249,        4:553~1057'
                              fitspw:  1:0~515;590~959, 2:0~503;601~959, 3:0~959;1250~1919, 4:0~552;1058~1919
Flagchannels input string for LB_EB5: '1:516~588,       2:504~600,       3:960~1250,        4:553~1057'
                              fitspw:  1:0~515;589~959, 2:0~503;601~959, 3:0~959;1251~1919, 4:0~552;1058~1919
Flagchannels input string for LB_EB6: '1:517~589,       2:505~601,       3:960~1249,        4:553~1057'
                              fitspw:  1:0~516;590~959, 2:0~504;602~959, 3:0~959;1250~1919, 4:0~552;1058~1919
```

The call to ``uvcontsub`` will re-index our line spectral windows.

`````{tab-set}

````{tab-item} Relevant lines in step4_prepare_lines.py

```python
for EB in data_dict['EBs']:            # this takes 1hr10min per LB EB
    inputvis            = data_dict['NRAO_path']+data_dict[EB]['_initlines_selfcal.ms']
    outputvis           = data_dict['NRAO_path']+data_dict[EB]['_initlines_selfcal.ms.contsub']
    spw                 = '1, 2, 3, 4' # only line spws; they will be renumbered 0,1,2,3
    combine             = ''           # break at scan, field, and spw
    fitorder            = 1            # order of polynomial fit; default is 0; DSHARP uses 1 so we copy them
    solint              = 'int'        # Timescale for per-baseline fit. default (recommended): ‘int’, i.e. no time averaging, do a fit for each integration and let the noisy fits average out in the image.continuum
    excludechans        = False        # the channels in fitspw will be used to fit the continuum
    want_cont           = False        # we don't need another ms to hold the continuum estimate

    os.system('rm -rf ' + outputvis)
    uvcontsub(vis=inputvis, spw=spw, combine=combine, fitorder=fitorder,
                       solint=solint, excludechans=excludechans, want_cont=want_cont,
                       fitspw=fitspw)
    listobs(vis=outputvis, listfile=outputvis+'.listobs.txt')
```
````

`````


Here is the before-and-after, for SB EB 1, for spectral windows SO, C<sup>18</sup>O, <sup>13</sup>CO, and <sup>12</sup>CO (left to right):

````{card} Example before/after continuum subtraction (SB EB 1)

<img src="../_static/gifs/ABAur_SB_EB1_initlines_selfcal_contsub_spw1.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">
<img src="../_static/gifs/ABAur_SB_EB1_initlines_selfcal_contsub_spw2.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">
<img src="../_static/gifs/ABAur_SB_EB1_initlines_selfcal_contsub_spw3.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">
<img src="../_static/gifs/ABAur_SB_EB1_initlines_selfcal_contsub_spw4.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">

+++
**Amplitude vs. channel, before and after continuum subtraction.** These plots were made with ``avgtime='1e8'``, ``avgscan=True`` and ``avgbaseline=True``.
````

<!-- The results for the other EBs are similar, although none that look as clear as SB EB1. Here for example is LB EB5:

````{card} Example before/after continuum subtraction (LB EB 5)
<img src="../_static/gifs/ABAur_LB_EB5_initlines_selfcal_contsub_spw1.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">
<img src="../_static/gifs/ABAur_LB_EB5_initlines_selfcal_contsub_spw2.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">
<img src="../_static/gifs/ABAur_LB_EB5_initlines_selfcal_contsub_spw3.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">
<img src="../_static/gifs/ABAur_LB_EB5_initlines_selfcal_contsub_spw4.gif" alt="SB_contsub_spw1" class="mb-1" width="24%">

+++
These plots were made with ``avgtime='1e8'``, ``avgscan=True`` and ``avgbaseline=True``.
```` -->


`````{dropdown} Velocity re-gridding with cvel2?

We do not regrid the measurement sets onto a common velocity grid using the ``cvel2`` task; we let ``tclean`` do this during imaging so as not to bin already-binned data.

However, we did regrid the measurement sets in an early version. Here is some information on what happens if you do that.

1. A listobs can nicely show that a measurement set has been successfully regridded. Below for example is the relevant section of a listobs for LB EB1 spectral window for SO, before and after regridding with the the ``cvel2`` task:

```console
Spectral Windows:  (1 unique spectral windows and 1 unique polarization setups)
  SpwID  Name                                       #Chans   Frame   Ch0(MHz)  ChanWid(kHz)  TotBW(kHz) CtrFreq(MHz) BBC Num  Corrs
  0      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   TOPO  219985.475       -61.035     58593.8 219956.2084        1  XX  YY
```

Notice "Frame" changes from TOPO to LSRK:

```console
Spectral Windows:  (1 unique spectral windows and 1 unique polarization setups)
  SpwID  Name                                       #Chans   Frame   Ch0(MHz)  ChanWid(kHz)  TotBW(kHz) CtrFreq(MHz) BBC Num  Corrs
  0      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.920       -61.033     58592.0 219949.6544        1  XX  YY
```

2. We can also check by looking at the channel frequencies in each execution block and each spectral window. Below is a gif showing how they become aligned after regridding.

SO:

````{card}
<img src="../_static/gifs/cvel2-before-after-spw0.gif" alt="SB_contsub_spw1" class="mb-1" width="99%">
````

C<sup>18</sup>O:

````{card}
<img src="../_static/gifs/cvel2-before-after-spw1.gif" alt="SB_contsub_spw1" class="mb-1" width="99%">
````

<sup>13</sup>CO:

````{card}
<img src="../_static/gifs/cvel2-before-after-spw2.gif" alt="SB_contsub_spw1" class="mb-1" width="99%">
````

<sup>12</sup>CO:

````{card}
<img src="../_static/gifs/cvel2-before-after-spw3.gif" alt="SB_contsub_spw1" class="mb-1" width="99%">
````

`````
<!-- Velocity re-gridded MSes (e.g. ABAur_12CO.bin30s.ms.cvel2) are available. -->


<!--
```{dropdown} Re-investigating the effect of cvel2 velocity regridding
I was interested to know whether cvel2 had aligned the channel frequencies perfectly (or at least, to within a channel width). For example, here's the Spectral Window section of the listobs output for ABAur_SO.bin30s.ms.cvel2:


Spectral Windows:  (8 unique spectral windows and 1 unique polarization setups)
  SpwID  Name                                       #Chans   Frame   Ch0(MHz)  ChanWid(kHz)  TotBW(kHz) CtrFreq(MHz) BBC Num  Corrs
  0      X392063246#ALMA_RB_06#BB_1#SW-01#FULL_RES     960   LSRK  219978.952       -61.041     58599.8 219949.6829        1  XX  YY
  1      X392063246#ALMA_RB_06#BB_1#SW-01#FULL_RES     960   LSRK  219978.944       -61.039     58597.7 219949.6754        1  XX  YY
  2      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.920       -61.033     58592.0 219949.6544        1  XX  YY
  3      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.925       -61.033     58591.8 219949.6595        1  XX  YY
  4      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.934       -61.033     58591.8 219949.6688        1  XX  YY
  5      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.918       -61.033     58591.7 219949.6531        1  XX  YY
  6      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.909       -61.033     58591.6 219949.6434        1  XX  YY
  7      X2090867609#ALMA_RB_06#BB_1#SW-01#FULL_RES    960   LSRK  219978.936       -61.033     58591.6 219949.6707        1  XX  YY


Looking at the frequency of the first channel (column Ch0), I see that the difference between Ch0 of SB EB1 (first row) and Ch0 of the other EBs is: -8 kHz, -32 kHz, -27 kHz, -18 kHz, -34 kHz, -43 kHz, and -16 kHz. So I guess you could say they are all aligned to within a channel width (61 kHz).
Doing the same exercise for the ABAur_13CO.bin30s.ms.cvel2:

SpwID  Name                                       #Chans   Frame   Ch0(MHz)  ChanWid(kHz)  TotBW(kHz) CtrFreq(MHz) BBC Num  Corrs
  0      X392063246#ALMA_RB_06#BB_2#SW-01#FULL_RES    1920   LSRK  220428.185       -30.521     58599.8 220398.9008        2  XX  YY
  1      X392063246#ALMA_RB_06#BB_2#SW-01#FULL_RES    1920   LSRK  220428.186       -30.520     58597.7 220398.9022        2  XX  YY
  2      X2090867609#ALMA_RB_06#BB_2#SW-01#FULL_RES   1920   LSRK  220428.133       -30.517     58592.0 220398.8520        2  XX  YY
  3      X2090867609#ALMA_RB_06#BB_2#SW-01#FULL_RES   1920   LSRK  220428.136       -30.517     58591.8 220398.8557        2  XX  YY
  4      X2090867609#ALMA_RB_06#BB_2#SW-01#FULL_RES   1920   LSRK  220428.145       -30.517     58591.8 220398.8647        2  XX  YY
  5      X2090867609#ALMA_RB_06#BB_2#SW-01#FULL_RES   1920   LSRK  220428.129       -30.517     58591.7 220398.8485        2  XX  YY
  6      X2090867609#ALMA_RB_06#BB_2#SW-01#FULL_RES   1920   LSRK  220428.149       -30.516     58591.6 220398.8684        2  XX  YY
  7      X2090867609#ALMA_RB_06#BB_2#SW-01#FULL_RES   1920   LSRK  220428.146       -30.516     58591.6 220398.8654        2  XX  YY

The difference in Ch0 between EBs is: 1 kHz, -52 kHz, -49 kHz, -40 kHz, -56 kHz, -36 kHz, and -39 kHz. All but one of these differences are larger than the channel width (30 kHz). Is this concerning?
``` -->
