#  Introduction

This is a guide to the reduction and imaging of <a href="https://almascience.nrao.edu/aq/?observationsProjectCode=2021.1.00690.S" target="_blank">ALMA program 2021.1.00690.S</a> (PI: R. Dong), which is a deep and fine-kinematics gas program towards the AB Aurigae protoplanetary disk. The scripts associated with this guide can be found at the <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">companion github repository</a>. All of the final data products (measurement sets, image cubes, VADPs) are or soon will be publicly available.

::::{grid}
:gutter: 3

:::{grid-item-card}
<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">**Reduction & imaging scripts on github**</a>
:::

:::{grid-item-card}
<a href="https://doi.org/10.11570/24.0087" target="_blank">**Download <sup>13</sup>CO and C<sup>18</sup>O data products**</a>
:::


:::{grid-item-card}
**<sup>12</sup>CO, SO & continuum data products** (Available soon)
:::
::::

Things to keep in mind:

- **The HTML component (this collection of webpages) works together with <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">the scripts</a>.** The HTML component is intended to provide visualizations of the outputs or results after running each part of the scripts. It also provides some written context, explanation or motivation behind the chosen approaches, on a selective basis.

- **The chosen approaches are specific to our program and science goals.** What works for your program might be different!

- **This guide is intended to be a snapshot, and will not be updated over time.** The choices and steps it presents are a function of the wisdom at the time (and the people whose wisdom I was able to receive). Of course, the communal wisdom is constantly changing. Software is continuously changing too. What is presented here may not necessarily hold forever.


As an additional reference, the refereed journal articles where the data are or will be published are linked below. Their methods sections contain complete overlap with the content here.

::::{grid}
:gutter: 2

:::{grid-item-card}

<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">
  <img alt="https://github.com/jjspeedie/workflow.2021.1.0690.S" src="_static/paper1.png">
</a>

<p></p>

<!-- <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">Speedie et al. 2024</a> presents the program's <sup>13</sup>CO and C<sup>13</sup>O line observations. -->
<sup>13</sup>CO and C<sup>13</sup>O line observations (paper 1).

:::

:::{grid-item-card}

<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">
  <img alt="https://github.com/jjspeedie/workflow.2021.1.0690.S" src="_static/paper2.png">
</a>

<p></p>

<!-- The <sup>12</sup>CO and SO line observations will be presented in <a href="https://github.com/jjspeedie/workflow.2021.1.0690.S" target="_blank">Speedie et al. in prep</a>. -->
<sup>12</sup>CO and SO line observations (paper 2).

:::
::::

## The workflow

The guide can be split in half into "reduction" and "imaging" categories. The former is broken into four "steps", three involving purely the continuum data and the fourth involving purely the lines. The "0th" step describes some ways to get prepared to start working with the data. But first, take a look at the [Learning Resources](overview/overview-resources.md) and the big-picture [Breakdown of Our Task](overview/overview-breakdown.md).

```{tableofcontents}
```

---

Sincere thanks go to Ryan Loomis, Sarah Wood and Tristan Ashton at the North American ALMA Science Center (NAASC) for providing science support and technical guidance on this ALMA data as part of a Data Reduction Visit to the NAASC, which was funded by the NAASC. The reduction and imaging of the ALMA data was performed on NAASC computing facilities.

Comments and corrections are much appreciated (especially if you are a student!). Get in touch: jspeedie@uvic.ca.
