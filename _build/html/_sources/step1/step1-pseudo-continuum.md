# Pseudocontinuum Measurement Sets

We want to remove our spectral lines to create a continuum-only measurement set. To do that, we have to take into account Doppler shifting of the lines (in the TOPO frame) over the course of the year.

I used functions from the DSHARP reduction_utils.py script to identify which channels to flag in each spectral window, given the rest frequency of the spectral line, and a choice of velocity range.

I chose the velocity ranges myself, based on plots of amplitude vs. frequency. The ranges I chose are smaller than what MAPS or DSHARP did (+/- 15 km/s and +/- 25 km/s, respectively), but I wanted to preserve as much bandwidth as possible, and my selections looked reasonable to me in plots of amplitude vs. frequency. Later, during imaging of the cubes, I confirmed my selected ranges did not include channels containing any line emission.


## SB EB1

<img src="images/SB1_setup.png" alt="SB1_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-SB_EB1.png" alt="SB1_spectral_averaging" class="mb-1" width="100%">

`````{admonition} In hindsight...
:class: tip
In hindsight (from Step 4), I should've made these plots with avgtime='1e8', avgscan=True and avgbaseline=True. It would've been a lot clearer.
`````

## SB EB2

<img src="images/SB2_setup.png" alt="SB2_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-SB_EB2.png" alt="SB2_spectral_averaging" class="mb-1" width="100%">

## LB EB1

<img src="images/LB1_setup.png" alt="LB1_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-LB_EB1.png" alt="LB1_spectral_averaging" class="mb-1" width="100%">

## LB EB2

<img src="images/LB2_setup.png" alt="LB2_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-LB_EB2.png" alt="LB2_spectral_averaging" class="mb-1" width="100%">


## LB EB3

<img src="images/LB3_setup.png" alt="LB3_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-LB_EB3.png" alt="LB3_spectral_averaging" class="mb-1" width="100%">

## LB EB4

<img src="images/LB4_setup.png" alt="LB4_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-LB_EB4.png" alt="LB4_spectral_averaging" class="mb-1" width="100%">

## LB EB5

<img src="images/LB5_setup.png" alt="LB5_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-LB_EB5.png" alt="LB5_spectral_averaging" class="mb-1" width="100%">

## LB EB6

<img src="images/LB6_setup.png" alt="LB6_setup" class="mb-1" width="100%">
<img src="images/spectral-averaging-LB_EB6.png" alt="LB6_spectral_averaging" class="mb-1" width="100%">
