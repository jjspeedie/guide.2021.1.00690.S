# Learning Resources

I relied on the following sources of information to build my understanding of the reduction/calibration/imaging process.

## ALMA Guides / CASA Guides

See the <a href="https://casaguides.nrao.edu/index.php?title=ALMAguides" target="_blank">**ALMAguides**</a> main page.

* <a href="https://casaguides.nrao.edu/index.php?title=ALMA_Cycle_8_Imaging_Pipeline_Reprocessing" target="_blank">**Examples for ALMA Imaging Pipeline Reprocessing.**</a> Cycle 8 Examples: Restoring pipeline calibration, renormalization corrections, reproducing pipeline products, re-imaging: continuum subtraction, aggregate continuum, revising continuum ranges, channel binning, uvtapering.

* <a href="https://casaguides.nrao.edu/index.php?title=Guide_to_the_NA_Imaging_Template" target="_blank">**NA Imaging Template.**</a> Designed to guide the user through the decisions needed when imaging ALMA data:

  * <a href="https://casaguides.nrao.edu/index.php?title=Imaging_Prep" target="_blank">Prepare the Data for Imaging</a>: Workflow, splitting off pipeline calibrated data, list of ms files to image, reviewing the calibration, flagging bad data, flux equalization, combining ms's from multiple executions, splitting off science target data, regridding spectral window, backing up data set. Note the incredible <a href="https://github.com/aakepley/ALMAImagingScript/blob/master/scriptForImagingPrep_template.py" target="_blank">scriptForImagingPrep_template.py</a> and <a href="https://github.com/aakepley/ALMAImagingScript/blob/master/scriptForImaging_template.py" target="_blank">scriptForImaging_template.py</a>.

  * <a href="https://casaguides.nrao.edu/index.php?title=Image_Continuum" target="_blank">Image the Continuum</a>: Averaged continuum ms, imaging parameters, imaging the continuum, exporting the images.

  * <a href="https://casaguides.nrao.edu/index.php?title=Self-Calibration_Template" target="_blank">Self-Calibration</a>: Self-cal on the continuum, phase and amplitude.

  * <a href="https://casaguides.nrao.edu/index.php?title=Image_Line" target="_blank">Spectral Line Imaging</a>: Continuum subtraction, applying continuum self-cal to the line data, imaging line data, exporting the images.

* <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">**Automasking Guide.**</a> For using auto-multithresh to generate cleaning masks; Table of Standard Values, demonstration of varying different parameters, best practices.

**Examples using TW Hya continuum and N2H+ line data:**

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Imaging_CASA_6" target="_blank">**A first look at imaging in CASA 6.2.**</a> Getting the data, starting CASA, CASA basics, getting oriented with the data, inspecting the data, first look at TCLEAN, experiment with TCLEAN, see the effects of calibration and flagging, image the science target (non-interactive/interactive), primary beam correction.

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Self_Calibration_CASA_6" target="_blank">**A first look at self-calibration in CASA 6.2.**</a> Self-calibration (phase and amplitude calibration; multiple rounds). (This webpage appeared to be under construction; it starts repeating itself...)

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Line_Imaging_CASA_6" target="_blank">**A first look at spectral line imaging in CASA 6.2.**</a>Continuum subtraction, imaging the spectral line, primary beam correction.

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Image_Analysis_CASA_6" target="_blank">**A first look at image analysis in CASA 6.2.**</a> Statistics, moments, exporting fits images.

**Miscelleneous:**

* <a href="https://casaguides.nrao.edu/index.php?title=Analysis_Utilities" target="_blank">**Analysis Utilities.**</a> A Python module containing utilities for analysis and plotting.

* <a href="https://casaguides.nrao.edu/index.php?title=ADMIT_Products_and_Usage" target="_blank">**A guide for utilizing ADMIT for your data.**</a> This guide discusses how to use ADMIT and customize it for your data.

* <a href="https://science.nrao.edu/facilities/alma/naasc-workshops/nrao-cd-wm16/Selfcal_Madison.pdf" target="_blank">**When, why, and how to do self-calibration.**</a>Slides by Sabrina Stierwalt.

* <a href="https://casa.nrao.edu/Release4.1.0/doc/UserMan/UserMansu82.html" target="_blank">**Under the Hood: Structure of the Measurement Set.**</a> More information regarding the structure of measurement sets. Know your columns.

## ALMA Docs

* <a href="https://arc.iram.fr/documents/cycle8/ALMA_Cycle8_Technical_Handbook.pdf" target="_blank">**ALMA Cycle 8 2021 Technical Handbook.**</a> Section 10.*.

* <a href="https://almascience.nrao.edu/portal/documents-and-tools/cycle8/alma-qa2-data-products-for-cycle-8" target="_blank">**ALMA QA2 Data Products for Cycle 8.**</a> The whole thing.


## Cycle 9 ALMA Ambassador Workshops

{Download}`Continuum Self Calibration (by A. Towner)<files/Selfcal_continuum_tutorial-withflowchart.pdf>`: Tutorial PDF using TWHya data.

{Download}`Line Self Calibration (by A. Towner)<files/Selfcal_line_tutorial.pdf>`: Tutorial PDF using maser data.


## Key Papers

* <a href="https://ui.adsabs.harvard.edu/abs/2018ApJ...869L..41A/abstract" target="_blank">**Andrews et al. (2018).**</a> DSHARP Large Program (Section 3 and Section 4).

* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....1O/abstract" target="_blank">**Oberg et al. (2021).**</a> MAPS Large Program (Section 3).

* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract" target="_blank">**Czekala et al. (2021).**</a> MAPS Large Program (Section 2, 3, 4, 5; clean strategies and the JvM effect).

* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">**Huang et al. (2021).**</a> MAPS Large Program (Section 2.1; imaging strategies for GM Aur, a disk with wild spiral arms and non-Keplerian emission).

## Scripts

* <a href="https://almascience.eso.org/almadata/lp/DSHARP/" target="_blank">**Reduction/imaging scripts from DSHARP Large Program.**</a> Continuum scripts and CO scripts for each disk, with some differences between disks. Useful for a grand overview, use of functions, choise of parameters, and how to handle multiple observation sets.

* <a href="https://almascience.eso.org/almadata/lp/DSHARP/scripts/reduction_utils.py" target="_blank">**Python functions from DSHARP Large Program (reductions_utils.py).**</a> Very useful functions, wrappers, etc.

**Line imaging scripts from MAPS Large Program (image_v3.py)**: Example of line imaging approach. Also includes Rich Teague's Keplerian mask script and (Ian Czekala's?) JvM correction script. Shared with us by Ryan Loomis; will eventually go public on the <a href="https://alma-maps.info/data.html" target="_blank">MAPS website</a>.

**Phase alignment script from exoALMA Large Program (alignment .py)**: To deal with decoherence between execution blocks; one important step in the self-calibration process. Shared with us by Ryan Loomis; to be released as part of the exoALMA publications.
<!-- <a href="https://" target="_blank">target</a> -->


## NAASC Data Reduction Visit (f2f)

I visited the NAASC/NRAO in Charlottesville, VA for a week and worked with Staff Scientist Ryan Loomis and Data Analysts Sarah Wood and Tristan Ashton. I gained huge insight into topics like: self-calibration (phase alignment), pipeline calibration (galactic CO absorption in our phase calibrator), and line imaging. I cannot recommend this program highly enough. <a href="https://science.nrao.edu/facilities/alma/visitors-shortterm" target="_blank">Learn about f2f visits here!</a>

## ALMA-Provided Resources Specific to Our Program

**The weblog.** This is like the program's bible. Its importance and helpfulness cannot be emphasized enough. We have two in total; one for each of TM1 and TM2.

**Quality assurance (QA) reports**. These are like an extremely abridged version of the weblog; some information is more easily accessed here, but only a few certain aspects can't be found anywhere else. We have 10 QA reports in total: 8 QA0's for each execution block, and 2 QA2's for each of TM1 and TM2.
