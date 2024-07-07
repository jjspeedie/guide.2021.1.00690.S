`````{admonition} Scripts for **Step 1 - Prepare the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_prepare_continuum.py" target="_blank">step1_prepare_continuum.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # necessary for an initial round of selfcal at the end
`````

# Initial Continuum Images

Here we perform initial imaging of the continuum data. We image each execution block, and spectral window, individually. For 8 execution blocks, each with 1 continuum SPW and 4 psuedo-continuum SPWs, that's

**Out motivation for doing this initial imaging is:**

- To check that the channel- and time-averaging didn't do anything noticeably problematic to the data.

- To get a sense of which execution blocks, and which spectral windows, are weak and which are strong (i.e. which have largest visible phase errors, which have largest SNR, etc). This will be useful for informing which EB to choose as a reference for phase alignment. We will (if possible) want to do (at least) one per-spw round of self-calibration, which will only be successful if we have high SNR in every spectral window.

- To get familiar with the current state of the data, so we can later gauge how much or little improvement we see after phase alignment ([Step 2](../step2/step2-align-SBs.md)) and self-calibration ([Step 3](../step3/step3-selfcal-SBs.md)).

The following are (non-interactively) cleaned images of the continuum for each execution block. Top left is an image combining all spectral windows; the other 5 images are for the 5 spectral windows individually.

## SB EB1

````{card}
<center>

<img src="images/ABAur_SB_EB1_initcont.image.jpg" alt="SB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB1_initcont_spw0.image.jpg" alt="SB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB1_initcont_spw1.image.jpg" alt="SB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB1_initcont_spw2.image.jpg" alt="SB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB1_initcont_spw3.image.jpg" alt="SB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB1_initcont_spw4.image.jpg" alt="SB_EB1_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````









## SB EB2

````{card}
<center>

<img src="images/ABAur_SB_EB2_initcont.image.jpg" alt="SB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB2_initcont_spw0.image.jpg" alt="SB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB2_initcont_spw1.image.jpg" alt="SB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB2_initcont_spw2.image.jpg" alt="SB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB2_initcont_spw3.image.jpg" alt="SB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_SB_EB2_initcont_spw4.image.jpg" alt="SB_EB2_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## LB EB1

````{card}
<center>

<img src="images/ABAur_LB_EB1_initcont.image.jpg" alt="LB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB1_initcont_spw0.image.jpg" alt="LB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB1_initcont_spw1.image.jpg" alt="LB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB1_initcont_spw2.image.jpg" alt="LB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB1_initcont_spw3.image.jpg" alt="LB_EB1_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB1_initcont_spw4.image.jpg" alt="LB_EB1_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## LB EB2

````{card}
<center>

<img src="images/ABAur_LB_EB2_initcont.image.jpg" alt="LB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB2_initcont_spw0.image.jpg" alt="LB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB2_initcont_spw1.image.jpg" alt="LB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB2_initcont_spw2.image.jpg" alt="LB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB2_initcont_spw3.image.jpg" alt="LB_EB2_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB2_initcont_spw4.image.jpg" alt="LB_EB2_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## LB EB3

````{card}
<center>

<img src="images/ABAur_LB_EB3_initcont.image.jpg" alt="LB_EB3_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB3_initcont_spw0.image.jpg" alt="LB_EB3_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB3_initcont_spw1.image.jpg" alt="LB_EB3_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB3_initcont_spw2.image.jpg" alt="LB_EB3_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB3_initcont_spw3.image.jpg" alt="LB_EB3_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB3_initcont_spw4.image.jpg" alt="LB_EB3_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## LB EB4

````{card}
<center>

<img src="images/ABAur_LB_EB4_initcont.image.jpg" alt="LB_EB4_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB4_initcont_spw0.image.jpg" alt="LB_EB4_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB4_initcont_spw1.image.jpg" alt="LB_EB4_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB4_initcont_spw2.image.jpg" alt="LB_EB4_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB4_initcont_spw3.image.jpg" alt="LB_EB4_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB4_initcont_spw4.image.jpg" alt="LB_EB4_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## LB EB5

````{card}
<center>

<img src="images/ABAur_LB_EB5_initcont.image.jpg" alt="LB_EB5_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB5_initcont_spw0.image.jpg" alt="LB_EB5_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB5_initcont_spw1.image.jpg" alt="LB_EB5_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB5_initcont_spw2.image.jpg" alt="LB_EB5_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB5_initcont_spw3.image.jpg" alt="LB_EB5_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB5_initcont_spw4.image.jpg" alt="LB_EB5_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## LB EB6

````{card}
<center>

<img src="images/ABAur_LB_EB6_initcont.image.jpg" alt="LB_EB6_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB6_initcont_spw0.image.jpg" alt="LB_EB6_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB6_initcont_spw1.image.jpg" alt="LB_EB6_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB6_initcont_spw2.image.jpg" alt="LB_EB6_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB6_initcont_spw3.image.jpg" alt="LB_EB6_initcont.image" class="mb-1" width="32%">
<img src="images/ABAur_LB_EB6_initcont_spw4.image.jpg" alt="LB_EB6_initcont.image" class="mb-1" width="32%">

</center>
+++
caption
````

## Comparing S, N and SNR across EBs

The following is a summary of the above continuum images (more directly informative for per-spw self calibration).

The horizontal lines indicate the SNR in the execution block if all spws are imaged. It is slightly higher than if we image the continuum spectral window only (spw 0), suggesting that the four 58 MHz bandwidth spectral windows (or more like 40-50 MHz, after line flagging) do add something.

A minimum of ~25 SNR is needed for self calibration. So we should be able to do per-spw self cal on the SB execution blocks. But this plot hints that we might not be able to self-cal the LB execution blocks without either concatenating them together, or concatenating them with the SB data.

````{card}
<center>

<img src="images/ABAur_initcont_SNR_perspw.png" alt="ABAur_initcont_SNR_perspw" class="mb-1" width="70%">

</center>
+++
caption
````


Just for reference, here is the equivalent plot but for [peak intensity] and [measured rms noise]. I calculated SNR as SNR = [peak intensity]/[measured rms noise].

````{card}
<center>

<img src="images/ABAur_initcont_max_perspw.png" alt="ABAur_initcont_max_perspw" class="mb-1" width="49%">
<img src="images/ABAur_initcont_rms_perspw.png" alt="ABAur_initcont_rms_perspw" class="mb-1" width="49%">

</center>
+++
caption
````

The LB executions have lower rms noise per beam than the SB executions, but the SB executions have that much more signal per beam.
