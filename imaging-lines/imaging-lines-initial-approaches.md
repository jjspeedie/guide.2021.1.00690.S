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

```{warning}
This page is more of a blog than a guide; more of a journal of experiments. Kept in case some niche aspects can be helpful. Recommend skip to next page: ([adopted approach](imaging-lines-adopted-approach.md).
```

# Initial Approaches

Relevant script: [initial approaches](imaging-lines-initial-approaches.md).
<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/image_lines.py" target="_blank">image_lines.py</a>.

## Cleaning and Masking

The `tclean` task gives the user the option to indicate where in the image to clean. The idea is that, inside the mask, the emission should be real (and therefore included in our model), and outside the mask, any emission should just be noise (and therefore excluded from the model).

For protoplanetary disks, we have some knowledge of how we expect their emission to look throughout the channels, because we expect the bulk of the disk to be Keplerian. [Rich Teague](https://richteague.github.io/) therefore wrote his [keplerian_mask](https://github.com/richteague/keplerian_mask) package, which is widely used for masking when making clean images of disks.

<i>Can we use a Keplerian mask for AB Aur?</i> That would be super convenient, but if we look at the [dirty images](imaging-lines-dirty-images.md) of <sup>12</sup>CO, <sup>13</sup>CO, and even C<sup>18</sup>O, the emission is clearly highly non-Keplerian. **We therefore need to explore other options for masking.**

````{card}
<center>
<video width="50%" controls>
  <source src="../_static/videos/ABAur_12CO.clean.keplerian_mask_m4.mov" type="video/mp4" alt="ABAur_12CO.clean.keplerian_mask_m4">
</video>
</center>
+++
`'r_max':10.0` (arcsec), `'dV0':750.0` (large Doppler width of the line, in m/s), `'dVq':0.0` (Doppler width is not a function of radius), `'zr':0.0` (non-elevated emission), `'target_res':None` (scale the CLEAN beam for the convolution kernel).
````

Ryan foresaw this and gave a couple possible ideas:

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

*What do other people do / can we find examples or guidance in the literature for situations like our own?* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021, MAPS)</a> seem to have had a similar issue of non-Keplerian emission with their re-imaging of GM Aur in <sup>12</sup>CO, and did something different to the MAPS fiducial imaging pipeline (<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract" target="_blank">Czekala et al. 2021</a>). Instead of Rich's custom CO mask, they used auto-multithresh to automatically generate masks in tclean on the fly, using some input threshold parameters. The relevant sentences are (Sec. 2.1):

> We applied the multiscale CLEAN algorithm (Cornwell 2008) with scales of `[0, 0.4, 1", 2"]`. Since <sup>12</sup>CO was also reobserved at higher spectral resolution than the other lines, we reimaged <sup>12</sup>CO with channel widths of 0.1 km/s for better recovery of the kinematic details. Due to the irregular emission morphology, we used CASA’s auto-multithresh algorithm (Kepley et al. 2020) to draw the CLEAN mask. The auto-multithresh algorithm searches the cube for significant emission, beginning with a relatively conservative mask and then expanding to encompass more emission during subsequent major cycles. The mask was initialized with full coverage of the primary beam from 5.2–6.4 km/s, where the emission is the broadest, because auto-multithresh algorithm does not readily mask diffuse emission. After some experimentation, the following auto-multithresh parameters were selected: `sidelobethreshold = 3.0`, `noisethreshold = 4.0`, `lownoisethreshold = 1.5`, and `minbeamfrac = 0.3`. The CLEAN threshold was set to 5 mJy, corresponding to ~3× the rms of line-free channels in the dirty image. --
<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">(Huang et al. 2021)</a>


(label:1stapproach)=
## 1st approach: Masking emission with auto-multithresh and the Huang et al. (2021) parameters

The `sidelobethreshold` and `noisethreshold` parameters <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021)</a> used are both lower (by `1.0`) than the defaults in the *"Table of Standard Salues: 12m (long) b75>300m"* (specified in the <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">Automasking Guide</a>). Effectively, lowering these two parameters makes auto-multithresh "more flexible", allowing the mask to grow a little more into lower signal areas than the default values allow.

### Results

I found that even with lowered `sidelobethreshold` and `noisethreshold` parameters, auto-multithresh **fails to capture extended/diffuse extended emission** in <sup>12</sup>CO and <sup>13</sup>CO cubes. We can see this in the movies below. The problem is most clear to see in the rightmost panels, which show the residuals (what's left after tclean has finished). In all movies, the white contours are the "final" auto-multithresh mask (i.e., the mask used on the last cleaning cycle -- all previous cycles' masks would have been less extended, since the mask can only grow between cycles). There are strong residuals *outside the mask*. This means there is emission that is not being included in the model.

````{card}
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
````

````{card}
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
````

````{card}
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
````

````{card}
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
````

**This is problematic because:**

- If we use JvM-corrected images, the uncaptured emission will be downscaled (by the factor epsilon).

- The cleaning will not actually reach the threshold, meaning the final images will be more shallowly cleaned than we specified. (It's a self-closing loop: tclean/auto-multithresh uses the unmasked regions to estimate the noise left in the residuals, so if it's estimating the noise using the regions with diffuse emission, it will think it's reached the threshold sooner than it has, and therefore stop cleaning, and stop growing the mask.)

(label:2ndapproach)=
## 2nd approach: Masking emission with auto-multithresh and the Huang et al. (2021) parameters, but kickstarting auto-multithresh with a broad mask

Referring back to <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021)</a>, we see they had a solution to the problem of auto-multithresh not masking diffuse emission:

> The mask was initialized with full coverage of the primary beam from 5.2–6.4 km/s, where the emission is the broadest, because auto-multithresh algorithm does not readily mask diffuse emission. --
<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">(Huang et al. 2021)</a>

I then discovered that getting auto-multithresh to actually use a pre-defined mask is non-trivial. The <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">Automasking Guide</a> provides some information at the bottom of the page, under the section titled *Advanced Use Case - Merging User Masks with Automasking*. So, this seems to be a bit niche, but at least it is a known issue.

Kickstarting auto-multithresh with a broad mask involves:

1. Make the (initial, broad) mask that you want auto-multithresh to start with. [For this I actually took Rich Teague's <a href="https://github.com/richteague/keplerian_mask" target="_blank">keplerian_mask</a> code and modified it to give me a broad ellipse at all channels within a range I defined. In hindsight there are probably simpler ways to do this, but at the time I had no easier ideas.]

2. Do one initial round of cleaning with the (initial, broad) mask, and without auto-multithresh. For this round I set `niter=cycleniter=1` (it's important that `niter=cycleniter`, and both `=1` simply so that the least amount of cleaning happens).

3. Restart `tclean`, now with auto-multithresh turned on, and give `tclean` instructions to pick up where the initial clean left off.

For making the (initial, broad) mask, my first approach was to take the sentence "*The mask was initialized with full coverage of the primary beam from 5.2–6.4 km/s, where the emission is the broadest*" (<a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. 2021</a>) to heart, and initialize the broad mask only in the channels where emission is broadest (and therefore have no mask, for this initial round of `tclean`, in the other channels, trusting that auto-multithresh will make its own). I chose the channel ranges based on where auto-multithresh had started failing to capture the emission in [{ref}`label:1stapproach`].

### Results

This seems to have worked well. Auto-multithresh did pick up the broad initial mask and take it from there. It won't shrink its mask in subsequent iterations, so we're stuck with the broad mask. But, this approach does seem to capture the diffuse emission in the clean image yield relatively even residuals inside the mask.

````{card}
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
````

**Room for improvement:** The broad initial mask should encompass an even larger range of channels. In the residuals movie (middle), there are still some residuals outside the auto-multithresh mask (e.g. 4.8 km/s, 6.942 km/s). If we look at the model (*bottom panel*), we can see the multi-scale deconvolver putting many small-Gaussians right up against the edge of the mask, trying to encompass the emission that extends over the sides. This suggests we just need to increase the channel range of the broad initial mask, to include bluer and redder channels.

(label:3rdapproach)=
## 3rd approach: Masking emission with auto-multithresh and the Huang et al. (2021) parameters, but kickstarting auto-multithresh with a broad mask, now over a wider range of channels

Here I did the same thing as [{ref}`label:2ndapproach`], but initializing the broad mask to cover bluer and redder channels.

### Results

This seems to have not worked as well. The 3 problems I see are:

1. The residuals within the mask after cleaning are **not of the same magnitude as the "noise"** outside the mask. There are significant residuals inside the mask that are **spatially uneven**. [This can be seen in the residual movies below.]

2. The cleaning is **uneven in velocity space**. Some channels have extremely large residuals in a discontinuous way from other channels. [A good example of this is at 4.002 km/s in <sup>12</sup>CO.]

3. The tails of <sup>12</sup>CO and <sup>13</sup>CO emission at the bluest and reddest channels in the clean image stop abruptly, **as if they have not been cleaned**. [This can be seen in position-velocity maps below as a truncation of the tails in JvM-corrected images. The downscaled-by-epsilon residuals helps to make the problem really visually obvious.]

````{card}
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
````

````{card}
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
````


````{card}
<img src="./images/v2_robust1.5/v2_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile.png" alt="v2_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">
<img src="./images/v2_robust1.5/v2_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile.png" alt="v2_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">
+++
Line profiles of the JvM-corrected images (another way to see the discontinuous cleaning in the tail channels).
````

**Ideas for improvement:** Perhaps one solution is to clean deeper (i.e., lower the `threshold` at which `tclean` stops). However, I have been setting the cleaning threshold to 3x the rms noise measured in line-free channels in the dirty image, and I would not like to deviate from that (3x or 4x the rms is best/common practice).

There are some reasons making me consider abandoning the broad initial mask idea entirely:

1. I'm generally nervous about using a broad mask (especially one that doesn't shrink). If this was a good idea, then I would think no one would bother with developing Keplerian masks or the auto-multithresh algorithm. I'm concerned that a broad mask **could allow artifacts/non-real emission to be cleaned** (i.e. to be included in the model).

2. Compared to [{ref}`label:1stapproach`], where auto-multithresh was *not* initialized with a broad mask, I found that in the [{ref}`label:2ndapproach`] and [{ref}`label:3rdapproach`], the **number of CLEAN major cycles was lower** (I track the number of major cycles by asking auto-multithresh to save its intermediate masks). This would mean auto-multithresh has less opportunity to adjust the mask.

Thinking back to one of Ryan's ideas: "*Take a dirty image, clean it a little bit, and define a mask by where the emission is over some threshold.*" This seems like a good way that we could develop more precise masks.

(label:4thapproach)=
## 4th approach: Masking emission with auto-multithresh and the Huang et al. (2021) parameters, but kickstarting auto-multithresh with a mask made from a model

### Making a mask from a clean model

After plotting contours of some of the above cleaned images and imagining how well these contours would serve as an initial mask, I found myself thinking about how I could get a smoother mask. This is how I got the idea of using a clean *model* to define a threshold mask.

The order of operations now becomes:

1. Make a model. Do this by cleaning down to a threshold of 10x the rms measured in the dirty image in line-free channels (so, not deeply cleaned, to minimize the chances of capturing unreal emission). For this clean, use a primary beam mask (`usemask='pb'` and `pbmask=0.2`) in all channels, and no auto-multithresh. Also, remove the smallest multiscale Gaussian so that the model is composed of `[0.1, 0.3, 0.6, 1., 2. arcsec]` Gaussians.

2. Translate this model into a mask, using a threshold you determine by experimentation. Currently I'm using 10x the mean. For reference, model units are in Jy/pixel.

3. From here, it's the same as before. Do one initial round of cleaning with the (model) mask, and without auto-multithresh. For this round set `niter=cycleniter=1` (it's important that `niter=cycleniter`, and both `=1` simply so that the least amount of cleaning happens).

4. Restart `tclean`, now with auto-multithresh turned on, and give `tclean` instructions to pick up where the initial clean left off.

Translating a model image into a mask was somewhat non-trivial for me (I didn't find the <a href="https://casadocs.readthedocs.io/en/stable/api/tt/casatasks.imaging.makemask.html?highlight=makemask" target="_blank">makemask</a> and <a href="https://casadocs.readthedocs.io/en/stable/api/tt/casatools.image.html?highlight=calcmask#casatools.image.image.calcmask" target="_blank">ia.calcmask</a> tasks straightforward to use at first). Below is an example of how the model masks look, created from the model image by taking a cut at a threshold value of 10x the mean of the model pixel values.


````{card}
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
````

````{card}
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
````

````{card}
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
````

There perhaps are some rogue white contour blobs (circles near the edge of the field of view) that should be removed. This would have to be done by hand, because increasing the cut threshold value (to e.g. 20x the mean) would shrink the mask so it no longer covers the diffuse emission, which would be defeating the whole point. But the other white contour blobs, within the realm of the disk, are seeds for auto-multithresh to pick up from. That's the beauty of it: this mask doesn't need to be perfect. Auto-multithresh will grow this mask how it needs to.


### Imaging with auto-multithresh kickstarted with the mask from a clean model (unedited)

As a first step, I used the exact masks generated above (i.e., I did no removing of any blobs by hand).

Below is an example of how the initial mask is grown over the course of the auto-multithresh cycles (in this case, C<sup>18</sup>O, 5 major cycles). The solid white regions represent the initial mask, and the white contours is the mask on the very last round:

````{card}
<center>
<video width="50%" controls>
  <source src="../_static/videos/v3_robust1.5/v3_robust1.5_C18O.clean.autothresh1.imview_channels.mp4" type="video/mp4" alt="v3_robust1.5_C18O.clean.autothresh1.imview_channels">
</video>
</center>
+++
C<sup>18</sup>O: Initial mask (made from a cut of the shallowly cleaned model image) compared to the final cleaning cycle (after growth by auto-multithresh).
````

### Results

````{card}
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
````

````{card}
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
````

````{card}
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
````

````{card}
<center>

<img src="./images/v3_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile.png" alt="v3_robust1.5+0.5_12CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">

<img src="./images/v3_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile.png" alt="v3_robust1.5+0.5_13CO.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">

<img src="./images/v3_robust1.5+0.5_C18O.clean.JvMcorr.image.line_profile.png" alt="v3_robust1.5+0.5_C18O.clean.JvMcorr.image.line_profile" class="mb-1" width="48%">

</center>
+++
Line profiles of the JvM-corrected images (a way to see that discontinuous cleaning in the tail channels is still happening).
````

**Ideas for improvement:**

- **Most troubling problem (most apparent at lower robust):** The strange **discontinuous cleaning in velocity space is still present** (e.g. 7.362 km/s in <sup>13</sup>CO). It is still the case with <sup>12</sup>CO and <sup>13</sup>CO that the number of autothresh iterations (i.e. major cycles) is only 1 or 2, which makes me think this could be the reason for the discontinous cleaning in velocity space, because the number of iterations that C<sup>18</sup>O does is ~5, and it looks ok. Perhaps specifying a smaller cleaning `threshold` for <sup>13</sup>CO and <sup>12</sup>CO could fix that by compelling `tclean` to do more cycles?

- The **emission distribution in the background sky changes as a function of channel** -- it looks nice and even/random at the tail channels, and then quite patchy at the central channels. Is this because of a lot of bleeding of signal into sidelobes at channels where the emission is extended/diffuse? [Spoiler alert: It's negative bowling due to missing short uv-spacings; see [{ref}`label:solutions`].]

- Some manual pruning of the blobs around the edges of the field of view might be needed.



## Pause

Let's take stock of where we are.

1. ***At this point,*** the image cubes look like this:

````{card}
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
````

````{card}
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
````

2. ***At this point,*** I discovered that, if I want to re-grid onto the velocity grid displayed at the very top of this page, then I shouldn't be working with measurement sets that have been `cvel2`ed (!). I therefore went back to [step 4](../step4/step4-line-mses-achieved.md) and undid the `cvel2` step, such that all the measurement sets are in the TOPO frame.

3. ***At this point,*** I reached out to the NAASC to arrange a <a href="https://almascience.nrao.edu/documents-and-tools/cycle10/alma-na-arcguide" target="_blank">virtual chat</a> to get some input and new ideas. I received written input from Amanda Kepley and met with Ryan Loomis -- both were extremely helpful. Below is a summary of the new understanding I gained and motivation for the [imaging strategy we consequently adopted for this program](../imaging-lines/imaging-lines-adopted-approach.md) (next page).

(label:solutions)=
# Solutions (after NAASC Virtual Chat with Ryan Loomis)

Outcomes: (1) Amanda Kepley provided a nice idea to borrow some guiding principles from the PHANGS-ALMA pipeline; (2) A meeting with Ryan is upcoming.

Summary of what the problems were:

## Problem 1: tclean consistently not cleaning certain channels

Channel dropouts correspond to "minor cycle stopped at large scale negative or diverging". What is divergence? From an old casaguide called <a href="https://casaguides.nrao.edu/index.php/TCLEAN_and_ALMA" target="_blank">TCLEAN_AND_ALMA</a>:

> If tclean detects:
-- divergence within minor cycle iterations
  -> as an increase of 10% from the minimum peak residual so far
      -> it will stop minor cycle iterations for this plane.

- Version of CASA: modular CASA, version 6.4.3.27

- it happens for different robust parameters

- it happens for C<sup>18</sup>O and SO, which was not as obvious from the line profile

- consistent in absolute velocity, not the channel index (if I image with different channel 'start' parameter, it's still the same result)

```{dropdown} Can you see "an increase of 10% from the minimum peak residual so far" happening in the casalogs? Following channel 51 (dropout channel) in casalogs in ^13^CO v5?

<pre style="background-color: #faf0d4;">
  <b>[13CO v5; 2nd tclean call (initializing tailored mask), channel 51]</b>


  2023-03-07 23:07:41	INFO	task_tclean::MatrixCleaner::validatePsf() 	Peak of PSF = 1 at [1024, 1024]
  2023-03-07 23:07:42	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 0
  2023-03-07 23:07:42	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 1
  2023-03-07 23:07:43	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 2
  2023-03-07 23:07:43	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 3
  2023-03-07 23:07:43	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 4
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 5
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 0
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 1
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 2
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 3
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 4
  2023-03-07 23:07:44	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 5
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	scale 1 = 1 pixels with bias = 1
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	scale 2 = 5 pixels with bias = 1
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	scale 3 = 15 pixels with bias = 1
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	scale 4 = 30 pixels with bias = 1
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	scale 5 = 50 pixels with bias = 1
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	scale 6 = 100 pixels with bias = 1
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	Cleaning using given mask
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	Cleaning pixels with mask values above 0.9
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	Starting iteration
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	
  <b>Initial maximum residual is 1.39906 within the mask</b>

  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	iteration    MaximumResidual   CleanedFlux
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	1      1.39906      0.139906
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	  0    0
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	  1    0
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	  2    0
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	  3    0
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	  4    0.139906
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	  5    0
  2023-03-07 23:07:45	INFO	task_tclean::MatrixCleaner::clean() 	
  <b>Failed to reach stopping threshold</b>

  2023-03-07 23:07:46	INFO	task_tclean::SDAlgorithmBase::deconvolve 	[/lustre/cv/users/jspeedie/data/images_lines/13CO/v5_robust0.5/ABAur_13CO.clean:C1] iters=1->2 [1],
  <b>model=0->0.139905, peakres=0.141461->0.125274, Reached cycleniter</b>
  .

  <b>[13CO v5; 3rd tclean call (cleaning down to threshold with tailored mask and auto-multithresh), channel 51]</b>


  2023-03-07 23:28:46	INFO	SDMaskHandler::autoMaskByMultiThreshold 	*** Start auto-multithresh processing for Channel 1***
  2023-03-07 23:28:46	INFO	SDMaskHandler::autoMaskByMultiThreshold 	Start thresholding: create an initial mask by threshold
  2023-03-07 23:28:46	INFO	SDMaskHandler::autoMaskByMultiThreshold 	End thresholding: time to create the initial threshold mask:  real 0.08s ( user 0.06s, system 0.03s)
  2023-03-07 23:28:46	INFO	SDMaskHandler::autoMaskByMultiThreshold 	Start pruning: the initial threshold mask
  2023-03-07 23:28:47	INFO	SDMaskHandler::YAPruneRegions 	 No regions are removed in pruning process.
  2023-03-07 23:28:47	INFO	SDMaskHandler::autoMaskByMultiThreshold 	End pruning: time to prune the initial threshold mask: real 0.48s (user 0.47s, system 0s)
  2023-03-07 23:28:47	INFO	SDMaskHandler::autoMaskByMultiThreshold 	Start smoothing: the initial threshold mask
  2023-03-07 23:28:48	INFO	SDMaskHandler::autoMaskByMultiThreshold 	End smoothing: time to create the smoothed initial threshold mask: real 1.21s (user 2.06s, system 0.78s)
  2023-03-07 23:28:48	INFO	SDMaskHandler::autoMaskByMultiThreshold 	Start thresholding: create a negative mask
  2023-03-07 23:28:49	INFO	SDMaskHandler::autoMaskByMultiThreshold 	No negative region was found by auotmask.
  2023-03-07 23:28:49	INFO	SDMaskHandler::autoMaskByMultiThreshold 	End thresholding: time to create the negative mask: real 0.8s (user 1s, system 0.26s)

  2023-03-07 23:40:36	INFO	task_tclean::MatrixCleaner::validatePsf() 	Peak of PSF = 1 at [1024, 1024]
  2023-03-07 23:40:37	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 0
  2023-03-07 23:40:37	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 1
  2023-03-07 23:40:38	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 2
  2023-03-07 23:40:38	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 3
  2023-03-07 23:40:39	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 4
  2023-03-07 23:40:39	INFO	task_tclean::MatrixCleaner::makePsfScales() 	Calculating convolutions for scale 5
  2023-03-07 23:40:39	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 0
  2023-03-07 23:40:39	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 1
  2023-03-07 23:40:39	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 2
  2023-03-07 23:40:39	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 3
  2023-03-07 23:40:40	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 4
  2023-03-07 23:40:40	INFO	task_tclean::MatrixCleaner::makeScaleMasks() 	Calculating mask convolution for scale 5
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	scale 1 = 1 pixels with bias = 1
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	scale 2 = 5 pixels with bias = 1
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	scale 3 = 15 pixels with bias = 1
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	scale 4 = 30 pixels with bias = 1
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	scale 5 = 50 pixels with bias = 1
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	scale 6 = 100 pixels with bias = 1
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	Cleaning using given mask
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	Cleaning pixels with mask values above 0.9
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	Starting iteration
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	
  <b>Initial maximum residual is 1.26355 within the mask</b>

  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	iteration    MaximumResidual   CleanedFlux
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	
  <b>Diverging due to large scale?</b>

  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	  0    0
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	  1    0
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	  2    0
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	  3    0
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	  4    0.240085
  2023-03-07 23:40:41	INFO	task_tclean::MatrixCleaner::clean() 	  5    0.195194
  2023-03-07 23:40:41	WARN	task_tclean::SDAlgorithmMSClean::takeOneStep (file src/code/synthesis/ImagerObjects/SDAlgorithmMSClean.cc, line 185)
  <b>MSClean minor cycle stopped at large scale negative or diverging</b>

  2023-03-07 23:40:41	INFO	task_tclean::SDAlgorithmBase::deconvolve 	[/lustre/cv/users/jspeedie/data/images_lines/13CO/v5_robust0.5/ABAur_13CO.clean:C1] iters=54->57 [3],
  <b>model=0.139906->0.37999, peakres=0.126291->0.102837, Exited multiscale minor cycle without reaching any stopping criterion.</b>


  2023-03-08 00:27:32	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	*** Start auto-multithresh processing for Channel 1***
  2023-03-08 00:27:32	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start thresholding: create an initial mask by threshold
  2023-03-08 00:27:32	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End thresholding: time to create the initial threshold mask:  real 0.08s ( user 0.06s, system 0.02s)
  2023-03-08 00:27:32	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start pruning: the initial threshold mask
  2023-03-08 00:27:33	INFO	task_tclean::SDMaskHandler::YAPruneRegions 	 No regions are removed in pruning process.
  2023-03-08 00:27:33	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End pruning: time to prune the initial threshold mask: real 0.49s (user 0.48s, system 0.01s)
  2023-03-08 00:27:33	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start smoothing: the initial threshold mask
  2023-03-08 00:27:34	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End smoothing: time to create the smoothed initial threshold mask: real 1.2s (user 2.07s, system 0.76s)
  2023-03-08 00:27:34	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start grow mask: growing the previous mask
  2023-03-08 00:27:34	INFO	task_tclean::SDMaskHandler::binaryDilation 	grow iter done=1
  2023-03-08 00:27:34	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End grow mask: time to grow the previous mask: real 0.35s (user 0.32s, system 0.03s)
  2023-03-08 00:27:34	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start pruning: on the grow mask
  2023-03-08 00:27:35	INFO	task_tclean::SDMaskHandler::YAPruneRegions 	 No regions are removed in pruning process.
  2023-03-08 00:27:35	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End pruning: time to prune the grow mask: real 0.49s (user 0.48s, system 0.01s)
  2023-03-08 00:27:35	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start smoothing: the grow mask
  2023-03-08 00:27:36	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End smoothing: time to create the smoothed grow mask: real 1.21s (user 2.09s, system 0.75s)
  2023-03-08 00:27:36	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	Start thresholding: create a negative mask
  2023-03-08 00:27:37	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	No negative region was found by auotmask.
  2023-03-08 00:27:37	INFO	task_tclean::SDMaskHandler::autoMaskByMultiThreshold 	End thresholding: time to create the negative mask: real 0.78s (user 1s, system 0.22s)
</pre>
```

This is fundamentally tied to a small number of major cycles being run?


```{dropdown} Problem 2: Missing short spacings

When looking at the central channels of the <sup>12</sup>CO channel map movies, Ryan noticed that we're getting these "negative bowls". He pulled up Table 7.1 of the Technical Handbook and we looked at the maximum recoverable scale (MRS) of our TM2 configuration (C3), which is 7.02 arcsec. We compared this to the emission in one of the central <sup>12</sup>CO channels. Very roughly speaking, you can imagine the emission in one such channel as a Gaussian with a FWHM of 10 arcsec. The Fourier transform of that Gaussian is going to have significant amounts of flux at scales in uv space smaller than what is achieved by the C3 configuration. In other words, due to the MRS of our TM2 data, we don't have any measurements on small enough uv scales, meaning we can't constrain the flux very well on the large spatial scales, and there's probably a lot of flux that we're "resolving out".

There are some imaging "tricks" we can do to deal with the missing short spacings (namely, do more major cycles, see below), but the only way to properly deal with this is to get data on those short spacings.

Recommendation: Request 7m data in Cycle 10 to complete our short spacings.

- Ryan: It will be a couple hours of 7m time and it would dramatically improve the quality of your images.

- 7m data at 230 GHz has a MRS of 29 arcsec (plenty short-enough spacings).

- Throw a couple screengrabs of the negative bowls into the proposal. Ryan thinks such a figure would be very clear and compelling.

- From Table 7.5 of the Technical Handbook, the C6 + C3 + 7m configuration combination has a multiplier for the 7m data of 0.6x the on-source time of the TM1 (C6) data.

- Ask for 0.6x however much on-source time you have for the C6 data. Justify it in the proposal by making up your sensitivity such that it gives that amount of on-source time.

- Sell your proposal: “This data is exquisite in quality, it’s already been able to answer X question, but in order to answer Y question, we really need to get the missing short spacings put in there, and it’ll fully unlock the quality of this data”.

- Jess: Note that exoALMA got C6 + C3 + 7m data.
```

Solution

When you go through a major cycle, you go back from the image plane into the Fourier plane. Specifically, you Fourier transform your clean model (the model that is built up so far) back into the Fourier plane everywhere. This process "fills out" the uv plane - even at spacings where you don't actually have data.

Because we are missing these short spacings, you want to clean "slowly" (i.e. with a lot of major cycles) to try to put as much of the model flux back into your full uv distribution as possible. This is the only thing you can do right now to address the missing short spacings, in the absence of having the [7m] data.

In contrast, imagine that you do the entire clean in one major cycle. Throughout the whole clean, you would never have transformed the model back into the Fourier plane. This means it would have "cleaned in" inaccurate clean components [Jess is not fully clear how exactly]. The trade-off is that doing a major cycle is computationally expensive.

*How to force more major cycles:* Make the minor cycles end more quickly. There are 2 ways to do end a minor cycle: (1) Hit the maximum number of minor cycle iterations, 'cycleniter'; or (2) Hit the maximum minor cycle threshold. The following parameters control option (2):

- Turn up 'cyclefactor': The minor cycle threshold is calculated as [cyclefactor]x[peaksidelobe]. The 'peaksidelobe' is the peak value of your dirty beam's sidelobes (e.g. 7%).

- You want to avoid cleaning INSIDE what is actually a sidelobe. For example, say there's a bright point source at one place in the dirty image. Some fraction of its signal will appear in other places in the image, due to the beam having sidelobes. By setting the minor cycle threshold to cyclefactor*peaksidelobe, you avoid trying to assign clean components inside areas that could possibly only have signal due to this sidelobe-leakage. You want to go back and do a major cycle before you try to clean in that area.

- Currently I have been using a cyclefactor of 1 (the default). Turn cyclefactor up to 1.5 or 2. Start with 2, and see if it doesn't take outrageously long.

- If clean hits cycleniter before it hits the minor cycle threshold, then that means that within one minor cycle, it would have assigned cycleniter clean components. Currently I have had cycleniter set to 300. That many clean components, where the components are Gaussians (due to doing a multiscale clean) can actually be a lot of flux, because the PEAK of the Gaussians are what are assigned values, not their total volumes. You want to clean as little flux in each minor cycle as possible, to ensure that you are not assigning clean components inside sidelobes and are filling out the uv space.

- Turn down 'gain' to 0.05 or 0.02: When clean identifies a pixel to clean, it says "I'm going to take this value I see here and assign it a clean component that is [gain]x[that value]". In other words, if it identifies a 1 Jy pixel to try to clean, it will assign a Gaussian component to have a peak whose value is 'gain' times 1 Jy. The default gain is 0.1, or 10%.

If you change the clean parameters above, you might be able to get away with a broader mask (e.g. pb):

- There's not actually any theoretical basis for tight masking. People have used masking as a way to (1) get around having poor uv coverage, and (2) reduce the number of major cycles they need to run (to save computational time). If you run the clean algorithm as originally designed by Hogbom with every cycle as a major cycle, it should actually work perfectly fine with no mask. If you’re never cleaning very deep in any given major cycle, then clean will never be in the situation where the sidelobes are stronger than the actual emission, and so it should keep assigning correct clean components.

- Cleaning with the broad mask may not be perfect, but you'll be able to get away with a lot more. The broad mask will perform a lot better with this kind of "cautious" clean.

- For measuring source properties after imaging, you can make a tailored mask.




#
