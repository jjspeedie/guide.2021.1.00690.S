# Learning Resources

I relied on the following sources of information to build my understanding of the reduction/calibration/imaging process.

## NAASC data reduction visit

**f2f data reduction visit.** Worked with Ryan Loomis and DA's Sarah Wood and Tristan Ashton. I gained huge insight into topics like: self-calibration (phase alignment), pipeline calibration (galactic CO absorption in our phase calibrator), and line imaging. Learn about f2f visits [here](https://science.nrao.edu/facilities/alma/visitors-shortterm).

## ALMA-provided resources specific to the program

**The weblog.** This is like the program's bible. Its importance and helpfulness cannot be emphasized enough. We have two in total; one for each of TM1 and TM2.

**Quality assurance (QA) reports**. These are like an extremely abridged version of the weblog; some information is more easily accessed here, but only a few certain aspects can't be found anywhere else. We have 10 in total; 8 QA0's for each execution block, and 2 QA2's for each of TM1 and TM2.


## Key papers

[**Andrews et al. (2018)**](https://ui.adsabs.harvard.edu/abs/2018ApJ...869L..41A/abstract), DSHARP Large Program (Section 3 and Section 4).

[**Oberg et al. (2021)**](https://ui.adsabs.harvard.edu/abs/2021ApJS..257....1O/abstract), MAPS Large Program (Section 3).

[**Czekala et al. (2021)**](https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract), MAPS Large Program (Clean strategies and the JvM effect).

[**Huang et al. (2021)**](https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract), MAPS Large Program (spiral arms in the massive GM Aur disk).

## Scripts

[**Reduction/imaging scripts from DSHARP Large Program**](https://almascience.eso.org/almadata/lp/DSHARP/): Continuum scripts and CO scripts for each disk, with some differences between disks. Useful for a grand overview, use of functions, choise of parameters, and how to handle multiple observation sets.

[**Python functions from DSHARP Large Program (reductions_utils.py)**](https://almascience.eso.org/almadata/lp/DSHARP/scripts/reduction_utils.py): Useful wrapper functions, etc.

**Phase alignment script from exoALMA Large Program (alignment .py)**: To deal with decoherence between execution blocks; one important step in the self-calibration process. Shared with us by Ryan Loomis; to be released as part of the exoALMA publications.

**Line imaging scripts from MAPS Large Program (image_v3.py)**: Example of line imaging approach. Also includes Rich Teague's Keplerian mask script and (Ian Czekala's?) JvM correction script. Shared with us by Ryan Loomis; will eventually go public on the MAPS website.


## ALMAguides/CASAguides

See [**CASAguides**](https://casaguides.nrao.edu/index.php?title=ALMAguides) main page.

[**Examples for ALMA Imaging Pipeline Reprocessing**](https://casaguides.nrao.edu/index.php?title=ALMA_Cycle_8_Imaging_Pipeline_Reprocessing) [Cycle 8 Examples]: Restoring pipeline calibration, renormalization corrections, reproducing pipeline products, re-imaging: continuum subtraction, aggregate continuum, revising continuum ranges, channel binning, uvtapering.

[**NA Imaging Template**](https://casaguides.nrao.edu/index.php?title=Guide_to_the_NA_Imaging_Template) designed to guide the user through the decisions needed when imaging ALMA data.

* [**Prepare the Data for Imaging**](https://casaguides.nrao.edu/index.php?title=Imaging_Prep): Workflow, splitting off pipeline calibrated data, list of ms files to image, reviewing the calibration, flagging bad data, flux equalization, combining ms's from multiple executions, splitting off science target data, regridding spectral window, backing up data set. Note the incredible [scriptForImagingPrep_template.py](https://github.com/aakepley/ALMAImagingScript/blob/master/scriptForImagingPrep_template.py) and [scriptForImaging_template.py](https://github.com/aakepley/ALMAImagingScript/blob/master/scriptForImaging_template.py).

* [**Image the Continuum**](https://casaguides.nrao.edu/index.php?title=Image_Continuum): Averaged continuum ms, imaging parameters, imaging the continuum, exporting the images.

* [**Self-Calibration**](https://casaguides.nrao.edu/index.php?title=Self-Calibration_Template): Self-cal on the continuum, phase and amplitude.

* [**Spectral Line Imaging**](https://casaguides.nrao.edu/index.php?title=Image_Line): Continuum subtraction, applying continuum self-cal to the line data, imaging line data, exporting the images.

[**Automasking Guide**](https://casaguides.nrao.edu/index.php/Automasking_Guide) for using auto-multithresh to generate cleaning masks; Table of Standard Values, demonstration of varying different parameters, best practices.

**Examples using TW Hya continuum and N2H+ line data, already calibrated:**

* [**A first look at imaging in CASA 6.2**](https://casaguides.nrao.edu/index.php?title=First_Look_at_Imaging_CASA_6): Getting the data, starting CASA, CASA basics, getting oriented with the data, inspecting the data, first look at TCLEAN, experiment with TCLEAN, see the effects of calibration and flagging, image the science target (non-interactive/interactive), primary beam correction.

* [**A first look at self-calibration in CASA 6.2**](https://casaguides.nrao.edu/index.php?title=First_Look_at_Self_Calibration_CASA_6): Self-calibration (phase and amplitude calibration; multiple rounds). (This webpage appeared to be under construction; it starts repeating itself...)

* [**A first look at spectral line imaging in CASA 6.2**](https://casaguides.nrao.edu/index.php?title=First_Look_at_Line_Imaging_CASA_6): Continuum subtraction, imaging the spectral line, primary beam correction.

* [**A first look at image analysis in CASA 6.2**](https://casaguides.nrao.edu/index.php?title=First_Look_at_Image_Analysis_CASA_6): Statistics, moments, exporting fits images.


**Some auxiliary things:**

* [**Analysis Utilities**](https://casaguides.nrao.edu/index.php?title=Analysis_Utilities): A Python module containing utilities for analysis and plotting.

* [**A guide for utilizing ADMIT for your data**](https://casaguides.nrao.edu/index.php?title=ADMIT_Products_and_Usage): This guide discusses how to use ADMIT and customize it for your data.

* [**When, why, and how to do self-calibration**](https://science.nrao.edu/facilities/alma/naasc-workshops/nrao-cd-wm16/Selfcal_Madison.pdf): Slides by Sabrina Stierwalt

* [**Under the Hood: Structure of the Measurement Set**](https://casa.nrao.edu/Release4.1.0/doc/UserMan/UserMansu82.html): More information regarding the structure of measurement sets. Know your columns.


## ALMA docs

[**ALMA Cycle 8 2021 Technical Handbook**](https://arc.iram.fr/documents/cycle8/ALMA_Cycle8_Technical_Handbook.pdf): Section 10.*.

[**ALMA QA2 Data Products for Cycle 8**](https://almascience.nrao.edu/portal/documents-and-tools/cycle8/alma-qa2-data-products-for-cycle-8): The whole thing.


## ALMA workshops

{Download}`Continuum Self Calibration (by A. Towner)<files/Selfcal_continuum_tutorial-withflowchart.pdf>`: Tutorial PDF using TWHya data.

{Download}`Line Self Calibration (by A. Towner)<files/Selfcal_line_tutorial.pdf>`: Tutorial PDF using maser data.
