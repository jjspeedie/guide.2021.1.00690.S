`````{admonition} Scripts for **Step 1 - Prepare the continuum**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_prepare_continuum.py" target="_blank">step1_prepare_continuum.py</a> # main script
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a> # loads disk_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/step1_utils.py" target="_blank">step1_utils.py</a> # loads multiple functions
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/selfcal_utils.py" target="_blank">selfcal_utils.py</a> # necessary for an initial round of selfcal at the end
`````

# Initial Self-Calibration

In preparation for the phase alignment, Ryan suggested we do a single roung of self-calibration on each execution block, just to get the phases looking as good as possible.

`````{admonition} Something to do differently...
:class: tip
What do we take as our initial model (the self-cal results depend greatly on this)? What deconvolver and beam do we use in the tclean step (the SNR of our solutions depend on this)?
`````

Before we start self calibration, we need to decide on our initial model. There are many options, such as:

* A (not very deeply) cleaned image (I think it is conventional to go with this)

* A model made from analytic fit to the visibilities (this was a suggestion from Ryan)

* An axisymmetric model, ie. azimuthal average of a (not very deeply) cleaned image (another suggestion from Ryan)

* The (not very deeply) cleaned image of the best EB, aligned? For example, for LB2-6, use LB1? (an idea of Jess's)

For now, we will go with a (not very deeply, but interactively) cleaned image.

There are also other considerations:

* What deconvolver do you use? For now, we will use hogbom (Ryan suggests delta functions, i.e. hogbom, are a better basis set for continuum rings than Gaussians, i.e. multi-scale)

* What beam (robust, uvtaper?) do you use? For now, we will use robust 0.5 and no uvtaper to keep it simple, and have something to improve upon later.

**What we take as the initial model**: A not very deeply, and interactively, cleaned image. These do not look as good as the "initial continuum images" above, because they are not cleaned as deeply. What matters here is that we trust the model column phases; the amplitudes are not important at this stage.

## The results of this initial round of per-EB self-cal

The SNR increased in all cases (some more than others). Visually, note the colorbar scale sometimes jumps significantly (is not the same as the gif blinks back and forth).

### SB EBs

<img src="images/SB_EB1_model_selfcal.gif" alt="SB_EB1_model_selfcal" class="mb-1" width="49%">
<img src="images/SB_EB2_model_selfcal.gif" alt="SB_EB2_model_selfcal" class="mb-1" width="49%">

### LB EBs

<img src="images/LB_EB1_model_selfcal.gif" alt="LB_EB1_model_selfcal" class="mb-1" width="49%">
<img src="images/LB_EB2_model_selfcal.gif" alt="LB_EB2_model_selfcal" class="mb-1" width="49%">
<img src="images/LB_EB3_model_selfcal.gif" alt="LB_EB3_model_selfcal" class="mb-1" width="49%">
<img src="images/LB_EB4_model_selfcal.gif" alt="LB_EB4_model_selfcal" class="mb-1" width="49%">
<img src="images/LB_EB5_model_selfcal.gif" alt="LB_EB5_model_selfcal" class="mb-1" width="49%">
<img src="images/LB_EB6_model_selfcal.gif" alt="LB_EB6_model_selfcal" class="mb-1" width="49%">
