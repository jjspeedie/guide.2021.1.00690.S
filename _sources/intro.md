#  Introduction

This is a guide to the reduction and imaging of <a href="https://almascience.nrao.edu/aq/?observationsProjectCode=2021.1.00690.S" target="_blank">ALMA program 2021.1.00690.S</a> (PI: R. Dong), which is a deep and fine-kinematics gas program towards the AB Aurigae protoplanetary disk. The scripts associated with this guide can be found at the <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">companion github repository</a>. All of the final data products (measurement sets, image cubes, VADPs) are publicly available.

::::{grid}
:gutter: 3

:::{grid-item-card}
<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">**Reduction & imaging scripts on github**</a>
:::

:::{grid-item-card}
<a href="https://doi.org/10.11570/24.0087" target="_blank">**Download <sup>13</sup>CO and C<sup>18</sup>O data products**</a>
:::


:::{grid-item-card}
<a href="https://doi.org/10.11570/24.0098" target="_blank">**Download <sup>12</sup>CO, SO & continuum data products**</a>
:::
::::

Things to keep in mind:

- **The HTML component (this collection of webpages) works together with <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">the scripts</a>.** The HTML component is intended to provide visualizations of the outputs or results after running each part of the scripts. It also provides some written context, explanation or motivation behind the chosen approaches, on a selective basis.

- **The chosen approaches are specific to our program and science goals.** What works for your program might be different!

- **This guide is intended to be a snapshot, and will not be updated over time.** The choices and steps it presents are a function of the wisdom at the time. Of course, the communal wisdom is constantly changing. Software is continuously changing too. What is presented here likely won't hold forever.


As an additional reference, the refereed journal articles where the data were published are linked below. Their methods sections contain complete overlap with the content here.

::::{grid}
:gutter: 2

:::{grid-item-card}

<a href="https://www.nature.com/articles/s41586-024-07877-0" target="_blank">
  <img alt="https://www.nature.com/articles/s41586-024-07877-0" src="_static/paper1.jpg">
</a>

<!-- <p></p> -->

<!-- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">Speedie et al. 2024</a> presents the program's <sup>13</sup>CO and C<sup>13</sup>O line observations. -->
<center><sup>13</sup>CO and C<sup>13</sup>O line observations (paper 1). <a href="https://www.nature.com/articles/s41586-024-07877-0" target="_blank">Speedie et al. 2024</a></center>
:::

:::{grid-item-card}

<a href="https://doi.org/10.3847/2041-8213/adb7d5" target="_blank">
  <img alt="https://doi.org/10.3847/2041-8213/adb7d5" src="_static/paper2.jpg">
</a>

<!-- <p></p> -->

<!-- The <sup>12</sup>CO and SO line observations will be presented in <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">Speedie et al. in prep</a>. -->
<center><sup>12</sup>CO and SO line observations (paper 2). <a href="https://doi.org/10.3847/2041-8213/adb7d5" target="_blank">Speedie et al. 2025</a></center>
:::
::::

## The workflow

The guide can be split in half into "reduction" and "imaging" categories. The former is broken into four "steps", three involving purely the continuum data and the fourth involving purely the lines. The "0th" step describes some ways to get prepared to start working with the data. But first, take a look at the [Learning Resources](overview/overview-resources.md) and the big-picture [Breakdown of Our Task](overview/overview-breakdown.md).

```{tableofcontents}
```

## FAQ

```{dropdown} *Where can I find information about the **expanding kernel high-pass filter** technique used in <a href="https://www.nature.com/articles/s41586-024-07877-0" target="_blank">Speedie et al. 2024</a> & <a href="https://doi.org/10.3847/2041-8213/adb7d5" target="_blank">2025</a> to enhance image contrast in moment maps?*

That's in a separate github repository called <a href="https://github.com/jjspeedie/expanding_kernel" target="_blank">``expanding_kernel``, here</a>. 
The python function can be found in <a href="https://github.com/jjspeedie/expanding_kernel/blob/main/expanding_kernel.py" target="_blank">expanding_kernel.py</a> and there is a lengthy demonstration of use provided <a href="https://github.com/jjspeedie/expanding_kernel/blob/main/example_usage.md" target="_blank">here</a>.

```

```{dropdown} *Where can I find information about the **anti-Keplerian masking** used in <a href="https://doi.org/10.3847/2041-8213/adb7d5" target="_blank">Speedie et al. 2025</a> to isolate infall in the <sup>12</sup>CO line data?* 

Making an anti-Keplerian mask is trivial once you've created a Keplerian mask with Rich Teague's <a href="https://github.com/richteague/keplerian_mask" target="_blank">``keplerian_mask``</a> package. It's simply a case of switching the ones to zeros and vice versa. You can find some lines of code doing that in <a href="https://github.com/jjspeedie/keplerian_mask/blob/master/use-case-2021.1.00690.S/make_keplerian_masks.py" target="_blank">this script</a> (lines 74-79 and lines 81-89).

Please note the anti-Keplerian masking is **not applied as a CLEAN mask** during imaging. See details on our approach to the line imaging [here](imaging-lines/imaging-lines-adopted-approach.md).

```



---

## Acknowledgements

Sincere and special thanks go to Ryan Loomis, Sarah Wood and Tristan Ashton at the North American ALMA Science Center (NAASC) for providing science support and technical guidance on this ALMA data as part of a Data Reduction Visit to the NAASC, which was funded by the NAASC. The reduction and imaging of the ALMA data was performed on NAASC computing facilities.

Comments and corrections are much appreciated (especially if you are a student!). Get in touch: jspeedie@uvic.ca.
