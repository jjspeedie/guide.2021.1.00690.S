<!-- `````{admonition} Scripts for **Imaging - Lines**:
:class: tip
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/major_image_lines.py" target="_blank">major_image_lines.py</a> # main script ([adopted approach](imaging-lines-adopted-approach.md))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/image_lines.py" target="_blank">image_lines.py</a> # earlier main script ([initial approaches](imaging-lines-initial-approaches.md))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_mask.py" target="_blank">dictionary_mask.py</a> # loads mask_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_data.py" target="_blank">dictionary_data.py</a> # loads data_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_disk.py" target="_blank">dictionary_disk.py</a> # loads disk_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/dictionary_lines.py" target="_blank">dictionary_lines.py</a> # loads line_dict
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/JvM_correction_casa6.py" target="_blank">JvM_correction_casa6.py</a> # MAPS JvM correction script ([Czekala et al. 2021](https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract))
- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/keplerian_mask.py" target="_blank">keplerian_mask.py</a> # modified version of [keplerian_mask](https://github.com/richteague/keplerian_mask) by [Rich Teague](https://richteague.github.io/)
`````

`````{admonition} Visibility Data for **Imaging - Lines** (obtained after [step 4](../step4/step4-line-mses-achieved.md)):
:class: tip
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_12CO.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_13CO.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0087/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_C18O.bin30s.ms.contsub</a>
- <a href="https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/24.0098/data/2021.1.00690.S/measurement_sets" target="_blank">ABAur_SO.bin30s.ms.contsub</a>
````` -->

`````{warning} 
This page is a journal of experiments and initial approaches to the line imaging. It is intended to serve as a blog more than anything else. I've kept a record of these experiments on the off chance that some aspects could be helpful to others in some niche cases. The imaging script corresponding to these initial experiments is <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/image_lines.py" target="_blank">image_lines.py</a>.

The main take-aways from these initial (unsuccessful) approaches are summarized on the next page, [Summary of Challenges Motivating the Adopted Imaging Strategy](imaging-lines-procedure.md). The final approach taken for the published line images is described on the last page, [Adopted Imaging Strategy](imaging-lines-adopted-approach.md). The corresponding imaging script is <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/major_image_lines.py" target="_blank">major_image_lines.py</a>.
`````

# Journal of Challenges and Initial Experiments


## Over-arching Challenge: Masking for Clean

`````{admonition} Cleaning and Masking
:class: note, dropdown

The `tclean` task gives the user the option to indicate where in the image to clean. The idea is that, inside the mask, the emission should be real (and therefore included in our model), and outside the mask, any emission should just be noise (and therefore excluded from the model).

For protoplanetary disks, we have some knowledge of where we expect their emission to appear throughout the channels, because we expect the bulk of the disk to be rotating Keplerian. [Rich Teague](https://richteague.github.io/) therefore wrote his [keplerian_mask](https://github.com/richteague/keplerian_mask) package, which is widely used for masking when making clean images of disks.
`````

`````{admonition} Problem: Appropriate clean mask for AB Aur?
:class: warning, dropdown

<i>Can we use a Keplerian mask for AB Aur?</i> That would be super convenient, but if we look at the [dirty images](imaging-lines-dirty-images.md) of <sup>12</sup>CO, <sup>13</sup>CO, and even C<sup>18</sup>O, the emission is clearly highly non-Keplerian. **We therefore need to explore other options for masking.**

````{card}
<center>
<video width="50%" controls>
  <source src="../_static/videos/ABAur_12CO.clean.keplerian_mask_m4.mov" type="video/mp4" alt="ABAur_12CO.clean.keplerian_mask_m4">
</video>
</center>
+++
Overlay of a Keplerian mask (pink contours) with the <sup>12</sup>CO image cube data. Keplerian mask parameters: `'r_max':10.0` (arcsec), `'dV0':750.0` (large Doppler width of the line, in m/s), `'dVq':0.0` (Doppler width is not a function of radius), `'zr':0.0` (non-elevated emission), `'target_res':None` (scale the CLEAN beam for the convolution kernel).
````

`````



`````{admonition} Possible solutions: Ways to make clean masks for AB Aur
:class: tip, dropdown

Ryan foresaw our need to explore other options for masking and gave a couple possible ideas:

1. Use manually drawn masks. This involves spending (potentially a lot of) time upfront to define the masks by hand, but then you have them and can reuse them continuously. <a href="https://alma-maps.info/" target="_blank">MAPS</a> did this for their <sup>12</sup>CO images (Rich Teague took the time to draw the masks for <sup>12</sup>CO by hand, and then they used Keplerian masks for everything else). Here's some central channels of Rich's custom CO mask for GM Aur:

````{card}
<center>
<video width="50%" controls>
  <source src="../_static/videos/MAPS_CO_custom_mask_GMAur_CO_220GHz.bin_30s.dirty.mask.mp4" type="video/mp4" alt="MAPS_CO_custom_mask_GMAur_CO_220GHz.bin_30s.dirty.mask">
</video>
</center>
+++
`CO_custom_mask_GMAur_CO_220GHz.bin_30s.dirty.mask` (<a href="https://alma-maps.info/data.html" target="_blank">MAPS</a>). From this, I'm gathering it's hard to draw perfectly smooth mask edges.
````


2. Use a Keplerian mask to define a "starting" mask, and then edit it by hand from there. In other words, save time by not drawing a mask from scratch.

3. Use <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">automasking ('auto-multithresh')</a>. This works well but is slow. Auto-multithresh is flexible; it draws an initial mask, and then updates it (grows it) during subsequent clean cycles. Here the time investment is re-spent every time you clean.

4. Take a dirty image, clean it a little bit, and define a mask based on the regions where the emission is over some threshold value.

5. Bounce back and forth. There's no good recipe that works for everything. Try a couple different things, see what works, and go with that.


`````



`````{admonition} More possible solutions: Huang+2021 (MAPS) approach to clean mask for GM Aur
:class: tip, dropdown

*Can we find examples or guidance in the literature for situations like our own?*

 <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021, MAPS)</a> seem to have had a similar issue of non-Keplerian emission with their re-imaging of GM Aur in <sup>12</sup>CO, and did something different to the MAPS fiducial imaging pipeline (<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract" target="_blank">Czekala et al. 2021</a>). Instead of Rich's custom CO mask, they used auto-multithresh to automatically generate masks in tclean on the fly, using some input threshold parameters. The relevant sentences are (Sec. 2.1):

> We applied the multiscale CLEAN algorithm (Cornwell 2008) with scales of `[0, 0.4, 1", 2"]`. Since <sup>12</sup>CO was also reobserved at higher spectral resolution than the other lines, we reimaged <sup>12</sup>CO with channel widths of 0.1 km/s for better recovery of the kinematic details. Due to the irregular emission morphology, we used CASA’s auto-multithresh algorithm (Kepley et al. 2020) to draw the CLEAN mask. The auto-multithresh algorithm searches the cube for significant emission, beginning with a relatively conservative mask and then expanding to encompass more emission during subsequent major cycles. The mask was initialized with full coverage of the primary beam from 5.2–6.4 km/s, where the emission is the broadest, because auto-multithresh algorithm does not readily mask diffuse emission. After some experimentation, the following auto-multithresh parameters were selected: `sidelobethreshold = 3.0`, `noisethreshold = 4.0`, `lownoisethreshold = 1.5`, and `minbeamfrac = 0.3`. The CLEAN threshold was set to 5 mJy, corresponding to ~3× the rms of line-free channels in the dirty image. --
<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">(Huang et al. 2021)</a>


`````




## 1st round of imaging experiments


`````{admonition} 1st imaging approach taken: Masking emission with auto-multithresh and the Huang et al. (2021) parameters
:class: note, dropdown

The `sidelobethreshold` and `noisethreshold` parameters <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021)</a> used are both lower (by `1.0`) than the defaults in the *"Table of Standard Salues: 12m (long) b75>300m"* (specified in the <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">Automasking Guide</a>). Effectively, lowering these two parameters makes auto-multithresh "more flexible", allowing the mask to grow a little more into lower signal areas than the default values allow.

`````



`````{admonition} Results: Auto-multithresh fails to capture extended/diffuse extended emission. There is emission that is not being included in the model.
:class: warning, dropdown


I found that even with lowered `sidelobethreshold` and `noisethreshold` parameters, auto-multithresh **fails to capture extended/diffuse extended emission** in <sup>12</sup>CO and <sup>13</sup>CO cubes. We can see this in the movies below. The problem is most clear to see in the rightmost panels, which show the residuals (what's left after tclean has finished). In all movies, the white contours are the "final" auto-multithresh mask (i.e., the mask used on the last cleaning cycle -- all previous cycles' masks would have been less extended, since the mask can only grow between cycles). There are strong residuals *outside the mask*. This means there is emission that is not being included in the model. **This is problematic because:**

- If we use JvM-corrected images, the uncaptured emission will be downscaled (by the factor epsilon).

- The cleaning will not actually reach the threshold, meaning the final images will be more shallowly cleaned than we specified. (It's a self-closing loop: tclean/auto-multithresh uses the unmasked regions to estimate the noise left in the residuals, so if it's estimating the noise using the regions with diffuse emission, it will think it's reached the threshold sooner than it has, and therefore stop cleaning, and stop growing the mask.)


```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_12CO.check.masking.mp4" type="video/mp4" alt="v1_robust1.5_12CO.check.masking">
</video>
<video width="47%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_12CO.check.masking.residual.mp4" type="video/mp4" alt="v1_robust1.5_12CO.check.masking.residual">
</video>
</center>
+++
<sup>12</sup>CO: Final CLEAN image (*left*) and final CLEAN residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle.
```

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_13CO.check.masking.mp4" type="video/mp4" alt="v1_robust1.5_13CO.check.masking">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_13CO.check.masking.residual.mp4" type="video/mp4" alt="v1_robust1.5_13CO.check.masking.residual">
</video>
</center>
+++
<sup>13</sup>CO: Final CLEAN image (*left*) and final CLEAN residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle.
```

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_C18O.check.masking.mp4" type="video/mp4" alt="v1_robust1.5_C18O.check.masking">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_C18O.check.masking.residual.mp4" type="video/mp4" alt="v1_robust1.5_C18O.check.masking.residual">
</video>
</center>
+++
C<sup>18</sup>O: Final CLEAN image (*left*) and final CLEAN residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle. [The problem is not *as* bad for C<sup>18</sup>O.]
```

```{card}
<center>
<video width="47%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_SO.check.masking.mp4" type="video/mp4" alt="v1_robust1.5_SO.check.masking">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v1_robust1.5/v1_robust1.5_SO.check.masking.residual.mp4" type="video/mp4" alt="v1_robust1.5_SO.check.masking.residual">
</video>
</center>
+++
SO: Final CLEAN image (*left*) and final CLEAN residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle. [Hard to say with SO because we're so close to the noise floor already - perhaps `sidelobethreshold` and `noisethreshold` parameters could actually be raised for SO.]
```


`````














## 2nd round of imaging experiments


`````{admonition} 2nd imaging approach taken: Masking emission with auto-multithresh and the Huang et al. (2021) parameters, but kickstarting auto-multithresh with a broad mask
:class: note, dropdown

Referring back to <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021)</a>, we see they had a solution to the problem of auto-multithresh not masking diffuse emission:

> The mask was initialized with full coverage of the primary beam from 5.2–6.4 km/s, where the emission is the broadest, because auto-multithresh algorithm does not readily mask diffuse emission. --
<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">(Huang et al. 2021)</a>

I then discovered that getting auto-multithresh to actually use a pre-defined mask is non-trivial. The <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">Automasking Guide</a> provides some information at the bottom of the page, under the section titled *Advanced Use Case - Merging User Masks with Automasking*. So, this seems to be a bit niche, but at least it is a known issue.

Kickstarting auto-multithresh with a broad mask involves:

1. Make the (initial, broad) mask that you want auto-multithresh to start with. [For this I actually took Rich Teague's <a href="https://github.com/richteague/keplerian_mask" target="_blank">keplerian_mask</a> code and modified it to give me a broad ellipse at all channels within a range I defined. In hindsight there are probably simpler ways to do this, but at the time I had no easier ideas.]

2. Do one initial round of cleaning with the (initial, broad) mask, and without auto-multithresh. For this round I set `niter=cycleniter=1` (it's important that `niter=cycleniter`, and both `=1` simply so that the least amount of cleaning happens).

3. Restart `tclean`, now with auto-multithresh turned on, and give `tclean` instructions to pick up where the initial clean left off.

For making the (initial, broad) mask, my first approach was to take the sentence "*The mask was initialized with full coverage of the primary beam from 5.2–6.4 km/s, where the emission is the broadest*" (<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. 2021</a>) to heart, and initialize the broad mask only in the channels where emission is broadest (and therefore have no mask, for this initial round of `tclean`, in the other channels, trusting that auto-multithresh will make its own). I chose the channel ranges based on where auto-multithresh had started failing to capture the emission in the "1st round of imaging experiments".


`````



`````{admonition} Results: It works, but the broad initial mask should encompass an even larger range of channels
:class: warning, dropdown



This seems to have worked well. Auto-multithresh did pick up the broad initial mask and take it from there. It won't shrink its mask in subsequent iterations, so we're stuck with the broad mask. But, this approach does seem to capture the diffuse emission in the clean image yield relatively even residuals inside the mask.

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v2_robust1.5_old/v2_robust1.5_13CO.check.masking.after.entire.clean.mp4" type="video/mp4" alt="v2_robust1.5_13CO.check.masking.after.entire.clean">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v2_robust1.5_old/v2_robust1.5_13CO.check.masking.after.entire.clean.residual.mp4" type="video/mp4" alt="v2_robust1.5_13CO.check.masking.after.entire.clean.residual">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v2_robust1.5_old/v2_robust1.5_13CO.check.masking.after.entire.clean.model.mp4" type="video/mp4" alt="v2_robust1.5_13CO.check.masking.after.entire.clean.model">
</video>
</center>
+++
<sup>13</sup>CO, after the re-started CLEAN: Final CLEAN image (*left*), residuals (*right*), and model (*bottom). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle. The broad initial mask is in place between 4.926 - 6.9 km/s.
```

**Room for improvement:** The broad initial mask should encompass an even larger range of channels. In the residuals movie (middle), there are still some residuals outside the auto-multithresh mask (e.g. 4.8 km/s, 6.942 km/s). If we look at the model (*bottom panel*), we can see the multi-scale deconvolver putting many small-Gaussians right up against the edge of the mask, trying to encompass the emission that extends over the sides. This suggests we just need to increase the channel range of the broad initial mask, to include bluer and redder channels.



`````




## 3rd round of imaging experiments


`````{admonition} 3rd imaging approach taken: Masking emission with auto-multithresh and the Huang et al. (2021) parameters, but kickstarting auto-multithresh with a broad mask, now over a wider range of channels
:class: note, dropdown

Here I did the same thing as the 2nd round of imaging experiments, but initializing the broad mask to cover bluer and redder channels.

`````



`````{admonition} Results: Significant residuals left inside the mask, cleaning is discontinuous in velocity space, tail channels not cleaned at all ("channel dropout")
:class: warning, dropdown


This seems to have not worked as well. The 3 problems I see are:

1. The residuals within the mask after cleaning are **not of the same magnitude as the "noise"** outside the mask. There are significant residuals inside the mask that are **spatially uneven**. [This can be seen in the residual movies below.]

2. The cleaning is **uneven in velocity space**. Some channels have extremely large residuals in a discontinuous way from other channels. [A good example of this is at 4.002 km/s in <sup>12</sup>CO.]

3. The tails of <sup>12</sup>CO and <sup>13</sup>CO emission at the bluest and reddest channels in the clean image stop abruptly, **as if they have not been cleaned**. [This can be seen in position-velocity maps below as a truncation of the tails in JvM-corrected images. The downscaled-by-epsilon residuals helps to make the problem really visually obvious.]

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v2_robust1.5/v2_robust1.5_13CO.clean.image.imview_channels.mp4" type="video/mp4" alt="v2_robust1.5_13CO.clean.image.imview_channels">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v2_robust1.5/v2_robust1.5_13CO.clean.residual.imview_channels.mp4" type="video/mp4" alt="v2_robust1.5_13CO.clean.residual.imview_channels">
</video>

<img src="./images/v2_robust1.5/ABAur_13CO.clean.JvMcorr.image_test000.png" alt="ABAur_13CO.clean.JvMcorr.image" class="mb-1" width="98%">
</center>
+++
<sup>13</sup>CO, after the re-started CLEAN: Final CLEAN image (*left*) and residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle. The broad initial mask is in place between 4.296 - 7.488 km/s. *Bottom:* Position-velocity diagram along the disk major axis of the JvM-corrected CLEAN image.
```

```{card}
<center>
<video width="51%" controls>
  <source src="../_static/videos/v2_robust1.5/v2_robust1.5_12CO.clean.image.imview_channels.mp4" type="video/mp4" alt="v2_robust1.5_12CO.clean.image.imview_channels">
</video>
<video width="47%" controls>
  <source src="../_static/videos/v2_robust1.5/v2_robust1.5_12CO.clean.residual.imview_channels.mp4" type="video/mp4" alt="v2_robust1.5_12CO.clean.residual.imview_channels">
</video>

<img src="./images/v2_robust1.5/ABAur_12CO.clean.JvMcorr.image_test000.png" alt="ABAur_12CO.clean.JvMcorr.image" class="mb-1" width="98%">
</center>
+++
<sup>12</sup>CO, after the re-started CLEAN: Final CLEAN image (*left*) and residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle. The broad initial mask is in place between 3.204 - 8.244 km/s. *Bottom:* Position-velocity diagram along the disk major axis of the JvM-corrected CLEAN image.
```


```{card}
<img src="./images/v2_robust1.5/v2_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile.png" alt="v2_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">
<img src="./images/v2_robust1.5/v2_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile.png" alt="v2_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">
+++
Line profiles of the JvM-corrected images (another way to see the discontinuous cleaning in the tail channels).
```


`````







## 4th round of imaging experiments


`````{admonition} 4th imaging approach taken: Masking emission with auto-multithresh and the Huang et al. (2021) parameters, but kickstarting auto-multithresh with a mask made from a model
:class: note, dropdown

Thinking back to one of Ryan's ideas: "*Take a dirty image, clean it a little bit, and define a mask by where the emission is over some threshold.*" This seems like a good way that we could develop more precise masks.

`````



`````{admonition} Figuring out how to make a mask from a clean model
:class: note, dropdown


After plotting contours of some of the above cleaned images and imagining how well these contours would serve as an initial mask, I found myself thinking about how I could get a smoother mask. This is how I got the idea of using a clean *model* to define a threshold mask.

The order of operations now becomes:

1. Make a model. Do this by cleaning down to a threshold of 10x the rms measured in the dirty image in line-free channels (so, not deeply cleaned, to minimize the chances of capturing unreal emission). For this clean, use a primary beam mask (`usemask='pb'` and `pbmask=0.2`) in all channels, and no auto-multithresh. Also, remove the smallest multiscale Gaussian so that the model is composed of `[0.1, 0.3, 0.6, 1., 2. arcsec]` Gaussians.

2. Translate this model into a mask, using a threshold you determine by experimentation. Currently I'm using 10x the mean. For reference, model units are in Jy/pixel.

3. From here, it's the same as before. Do one initial round of cleaning with the (model) mask, and without auto-multithresh. For this round set `niter=cycleniter=1` (it's important that `niter=cycleniter`, and both `=1` simply so that the least amount of cleaning happens).

4. Restart `tclean`, now with auto-multithresh turned on, and give `tclean` instructions to pick up where the initial clean left off.

Translating a model image into a mask was somewhat non-trivial for me (I didn't find the <a href="https://casadocs.readthedocs.io/en/stable/api/tt/casatasks.imaging.makemask.html?highlight=makemask" target="_blank">makemask</a> and <a href="https://casadocs.readthedocs.io/en/stable/api/tt/casatools.image.html?highlight=calcmask#casatools.image.image.calcmask" target="_blank">ia.calcmask</a> tasks straightforward to use at first). Below is an example of how the model masks look, created from the model image by taking a cut at a threshold value of 10x the mean of the model pixel values.


```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v2_initial_mask/v2_initial_mask_13CO.initial.mask.model.imview_channels.mp4" type="video/mp4" alt="v2_initial_mask_13CO.initial.mask.model.imview_channels">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v2_initial_mask/v2_initial_mask_13CO.initial.mask.residual.imview_channels.mp4" type="video/mp4" alt="v2_initial_mask_13CO.initial.mask.residual.imview_channels">
</video>
</center>
+++
<sup>13</sup>CO, after shallow initial CLEAN: Model image (*left*) and residuals (*right*) from a shallow CLEAN (whose purpose is just to make a smooth model). White contours are a cut at 10x the mean of the model pixel values, and will be used as the mask for the next step.
```

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v2_initial_mask/v2_initial_mask_12CO.initial.mask.model.imview_channels.mp4" type="video/mp4" alt="v2_initial_mask_12CO.initial.mask.model.imview_channels">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v2_initial_mask/v2_initial_mask_12CO.initial.mask.image.imview_channels.mp4" type="video/mp4" alt="v2_initial_mask_12CO.initial.mask.image.imview_channels">
</video>
</center>
+++
<sup>12</sup>CO, after shallow initial CLEAN: Model image (*left*) and CLEAN image (*right*) from a shallow CLEAN (whose purpose is just to make a smooth model). White contours are a cut at 10x the mean of the model pixel values, and will be used as the mask for the next step.
```

```{card}
<center>
<video width="51%" controls>
  <source src="../_static/videos/v2_initial_mask/v2_initial_mask_C18O.initial.mask.model.imview_channels.mp4" type="video/mp4" alt="v2_initial_mask_C18O.initial.mask.model.imview_channels">
</video>
<video width="46%" controls>
  <source src="../_static/videos/v2_initial_mask/v2_initial_mask_12CO.initial.mask.image.imview_channels.mp4" type="video/mp4" alt="v2_initial_mask_C18O.initial.mask.image.imview_channels">
</video>
</center>
+++
C<sup>18</sup>O, after shallow initial CLEAN: Model image (*left*) and CLEAN image (*right*) from a shallow CLEAN (whose purpose is just to make a smooth model). White contours are a cut at 10x the mean of the model pixel values, and will be used as the mask for the next step.
```

There perhaps are some rogue white contour blobs (circles near the edge of the field of view) that should be removed. This would have to be done by hand, because increasing the cut threshold value (to e.g. 20x the mean) would shrink the mask so it no longer covers the diffuse emission, which would be defeating the whole point. But the other white contour blobs, within the realm of the disk, are seeds for auto-multithresh to pick up from. That's the beauty of it: this mask doesn't need to be perfect. Auto-multithresh will grow this mask how it needs to.

`````

`````{admonition} Imaging with auto-multithresh kickstarted with the mask from a clean model
:class: note, dropdown

As a first step, I used the exact masks generated above (i.e., I did no removing of any blobs by hand).

Below is an example of how the initial mask is grown over the course of the auto-multithresh cycles (in this case, C<sup>18</sup>O, 5 major cycles). The solid white regions represent the initial mask, and the white contours is the mask on the very last round:

```{card}
<center>
<video width="50%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_C18O.clean.autothresh1.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_C18O.clean.autothresh1.imview_channels">
</video>
</center>
+++
C<sup>18</sup>O: Initial mask (made from a cut of the shallowly cleaned model image) compared to the final cleaning cycle (after growth by auto-multithresh).
```


`````



`````{admonition} Results: Cleaning is still discontinuous in velocity space, very few major cycles, negative bowling in central channels
:class: warning, dropdown


- **Most troubling problem (most apparent at lower robust):** The strange **discontinuous cleaning in velocity space is still present** (e.g. 7.362 km/s in <sup>13</sup>CO). It is still the case with <sup>12</sup>CO and <sup>13</sup>CO that the number of autothresh iterations (i.e. major cycles) is only 1 or 2, which makes me think this could be the reason for the discontinous cleaning in velocity space.

- The **emission distribution in the background sky changes as a function of channel** -- it looks nice and even/random at the tail channels, and then quite patchy at the central channels. [Spoiler alert: It's negative bowling due to missing short uv-spacings. See [next page](imaging-lines-procedure.md).]

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_12CO.clean.JvMcorr.image.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_12CO.clean.JvMcorr.image.imview_channels">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_12CO.clean.residual.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_12CO.clean.residual.imview_channels">
</video>
</center>
+++
<sup>12</sup>CO, after the re-started CLEAN: Final CLEAN JvM-corrected image (*left*) and residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle.
```

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_13CO.clean.image.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_13CO.clean.image.imview_channels">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_13CO.clean.residual.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_13CO.clean.residual.imview_channels">
</video>
</center>
+++
<sup>13</sup>CO, after the re-started CLEAN: Final CLEAN image (*left*) and residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle.
```

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_C18O.clean.image.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_C18O.clean.image.imview_channels">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_C18O.clean.residual.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_C18O.clean.residual.imview_channels">
</video>
</center>
+++
C<sup>18</sup>O, after the re-started CLEAN: Final CLEAN image (*left*) and residuals (*right*). White contours in both panels show the final auto-multithresh mask, after the last cleaning cycle.
```

```{card}
<center>

<img src="./images/v3_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile.png" alt="v3_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">

<img src="./images/v3_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile.png" alt="v3_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">

<img src="./images/v3_robust1.5+0.5_C18O.clean.JvMcorr.image.line_profile.png" alt="v3_robust1.5+0.5_C18O.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">

</center>
+++
Line profiles of the JvM-corrected images (a way to see that discontinuous cleaning in the tail channels is still happening).
```


`````






## Pause to reflect


Let's take stock of where we are after all these experiments. At this point, ...

`````{admonition} ... the image cubes look like this: 
:class: note, dropdown

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust0.5/v3_robust0.5_12CO.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust0.5_12CO.clean.JvMcorr.image.channelpans">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust0.5/v3_robust0.5_13CO.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust0.5_13CO.clean.JvMcorr.image.channelpans">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust0.5/v3_robust0.5_C18O.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust0.5_C18O.clean.JvMcorr.image.channelpans">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust0.5/v3a_robust0.5_SO.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust0.5_SO.clean.JvMcorr.image.channelpans">
</video>
</center>
+++
JvM-corrected image cubes of <sup>12</sup>CO, <sup>13</sup>CO, C<sup>18</sup>O and SO, imaged with Briggs `robust=0.5`.
```

```{card}
<center>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_12CO.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust1.5_12CO.clean.JvMcorr.image.channelpans">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_13CO.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust1.5_13CO.clean.JvMcorr.image.channelpans">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_C18O.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust1.5_C18O.clean.JvMcorr.image.channelpans">
</video>
<video width="49%" controls>
  <source src="../_static/videos/v3_robust1.5/v3a_robust1.5_SO.clean.JvMcorr.image.channelpans.mp4" type="video/mp4" alt="v3_robust1.5_SO.clean.JvMcorr.image.channelpans">
</video>
</center>
+++
JvM-corrected image cubes of <sup>12</sup>CO, <sup>13</sup>CO, C<sup>18</sup>O and SO, imaged with Briggs `robust=1.5`.
```

`````


`````{admonition} ... I discovered that, if I want to re-grid onto a chosen velocity grid, then I shouldn't be working with measurement sets that have already had cvel2 applied (!). 
:class: note, dropdown

I therefore went back to [step 4](../step4/step4-line-mses-achieved.md) and undid the `cvel2` step, such that all the measurement sets are in the TOPO frame.

`````



`````{admonition} ... I reached out to the NAASC to arrange a <a href="https://almascience.nrao.edu/documents-and-tools/cycle10/alma-na-arcguide" target="_blank">virtual chat</a> to get some input and new ideas. 
:class: tip, dropdown

I received written input from Amanda Kepley and met with Ryan Loomis -- both were extremely helpful. The [next page](../imaging-lines/imaging-lines-procedure.md) gives a summary of the new understanding I gained and motivation for the imaging strategy we consequently adopted for this program.

`````




