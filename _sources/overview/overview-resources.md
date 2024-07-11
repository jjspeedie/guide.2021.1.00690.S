# Learning Resources

Here's a list of information sources that I found useful for building an understanding of the reduction, calibration and imaging processes.

````{card} CASA Guides

See the <a href="https://casaguides.nrao.edu/index.php?title=ALMAguides" target="_blank">ALMAguides</a> main page.

* <a href="https://casaguides.nrao.edu/index.php?title=ALMA_Cycle_8_Imaging_Pipeline_Reprocessing" target="_blank">Examples for ALMA Imaging Pipeline Reprocessing</a> (Cycle 8 examples). Covers: Restoring the pipeline calibration, renormalization corrections, reproducing pipeline products, and re-imaging, including continuum subtraction, the aggregate continuum, revising continuum ranges, channel binning, and uvtapering.

* <a href="https://casaguides.nrao.edu/index.php?title=Guide_to_the_NA_Imaging_Template" target="_blank">NA Imaging Template.</a> Designed to guide the user through the decisions needed when imaging ALMA data:

  * <a href="https://casaguides.nrao.edu/index.php?title=Imaging_Prep" target="_blank">Prepare the Data for Imaging</a>: Workflow, splitting off pipeline calibrated data, listing MS files to image, reviewing the calibration, flagging bad data, flux equalization, combining MSes from multiple executions, splitting off science target data, regridding spectral window, and backing up data set. Note the incredible <a href="https://github.com/aakepley/ALMAImagingScript/blob/master/scriptForImagingPrep_template.py" target="_blank">scriptForImagingPrep_template.py</a> and <a href="https://github.com/aakepley/ALMAImagingScript/blob/master/scriptForImaging_template.py" target="_blank">scriptForImaging_template.py</a>.

  * <a href="https://casaguides.nrao.edu/index.php?title=Image_Continuum" target="_blank">Image the Continuum</a>: Creating an averaged continuum MS, imaging parameters, imaging the continuum, exporting the images.

  * <a href="https://casaguides.nrao.edu/index.php?title=Self-Calibration_Template" target="_blank">Self-Calibration</a>: Self-calibration on the continuum, including phase and amplitude self-cal.

  * <a href="https://casaguides.nrao.edu/index.php?title=Image_Line" target="_blank">Spectral Line Imaging</a>: Continuum subtraction, applying continuum self-cal to the line data, imaging line data, exporting the images.

* <a href="https://casaguides.nrao.edu/index.php/Automasking_Guide" target="_blank">Automasking Guide.</a> For using auto-multithresh to generate cleaning masks. Provides <u>Table of Standard Values</u> (!), and demonstration of varying different parameters, as well as best practices.

````

````{card} CASA Guides Examples: With TW Hya continuum and N2H+ line data

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Imaging_CASA_6" target="_blank">A first look at imaging in CASA 6.2.</a> Getting the data, starting CASA, CASA basics, getting oriented with the data, inspecting the data, first look at TCLEAN, experimenting with TCLEAN, seeing the effects of calibration and flagging, imaging the science target (non-interactive/interactive), primary beam correction.

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Self_Calibration_CASA_6" target="_blank">A first look at self-calibration in CASA 6.2.</a> Self-calibration (phase and amplitude calibration; multiple rounds).

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Line_Imaging_CASA_6" target="_blank">A first look at spectral line imaging in CASA 6.2.</a> Continuum subtraction, imaging the spectral line, primary beam correction.

* <a href="https://casaguides.nrao.edu/index.php?title=First_Look_at_Image_Analysis_CASA_6" target="_blank">A first look at image analysis in CASA 6.2.</a> Statistics, moments, exporting fits images.

````

````{card} CASA Guides: Miscelleneous

* <a href="https://casaguides.nrao.edu/index.php?title=Analysis_Utilities" target="_blank">Analysis Utilities.</a> A Python module containing utilities for analysis and plotting.

* <a href="https://casaguides.nrao.edu/index.php?title=ADMIT_Products_and_Usage" target="_blank">A guide for utilizing ADMIT for your data.</a> This guide discusses how to use ADMIT and customize it for your data.

* <a href="https://science.nrao.edu/facilities/alma/naasc-workshops/nrao-cd-wm16/Selfcal_Madison.pdf" target="_blank">When, why, and how to do self-calibration.</a> Slides by Sabrina Stierwalt.

* <a href="https://casa.nrao.edu/Release4.1.0/doc/UserMan/UserMansu82.html" target="_blank">Under the Hood: Structure of the Measurement Set.</a> More information regarding the structure of measurement sets. Know your columns!

````

````{card} ALMA Docs

* <a href="https://arc.iram.fr/documents/cycle8/ALMA_Cycle8_Technical_Handbook.pdf" target="_blank">ALMA Cycle 8 2021 Technical Handbook.</a> All of Section 10.

* <a href="https://almascience.nrao.edu/portal/documents-and-tools/cycle8/alma-qa2-data-products-for-cycle-8" target="_blank">ALMA QA2 Data Products for Cycle 8.</a> The whole document.

````

````{card} ALMA Primer View Series

*"The <a href="https://www.youtube.com/@almaprimer920/videos" target="_blank">ALMA Primer Series</a> is an effort to help inform astronomers about topics in interferometry and specifically how to get the most out of their own ALMA data. The team has members from National Research Council of Canada (NRC Herzberg), the National Radio Astronomy Observatory (NRAO) and from universities across North America. The series is not yet complete; new videos are in production covering a broad range of topics covering radio interferometry, calibration, imaging, and more."*

````

````{card} Cycle 9 ALMA Ambassador Workshop (Allison Towner)

{Download}`Continuum Self Calibration (by Allison Towner)<files/Selfcal_continuum_tutorial-withflowchart.pdf>`: Tutorial PDF using TWHya data.

{Download}`Line Self Calibration (by Allison Towner)<files/Selfcal_line_tutorial.pdf>`: Tutorial PDF using maser data.

````

````{card} Key Papers

* <a href="https://ui.adsabs.harvard.edu/abs/2018ApJ...869L..41A/abstract" target="_blank">Andrews et al. (2018).</a> DSHARP Large Program (Section 3 and Section 4).

* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....1O/abstract" target="_blank">Oberg et al. (2021).</a> MAPS Large Program (Section 3).

* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257....2C/abstract" target="_blank">Czekala et al. (2021).</a> MAPS Large Program (Section 2, 3, 4, 5; clean strategies and the JvM effect).

* <a href="https://ui.adsabs.harvard.edu/abs/2021ApJS..257...19H/abstract" target="_blank">Huang et al. (2021).</a> MAPS Large Program (Section 2.1; imaging strategies for GM Aur, a disk with wild spiral arms and non-Keplerian emission).

````

````{card} Scripts

* <a href="https://almascience.eso.org/almadata/lp/DSHARP/" target="_blank">Reduction/imaging scripts from DSHARP Large Program.</a> Continuum scripts and CO scripts for each disk, with some differences between disks. Useful for a grand overview, use of functions, choise of parameters, and how to handle multiple observation sets.

* <a href="https://almascience.eso.org/almadata/lp/DSHARP/scripts/reduction_utils.py" target="_blank">Python functions from DSHARP Large Program (reductions_utils.py).</a> Very useful functions, wrappers, etc.

* <a href="https://alma-maps.info/data.html" target="_blank">Line imaging scripts from MAPS Large Program (image_v3.py)</a>: Example of line imaging approach; Keplerian mask script and JvM correction script.

* Phase alignment script from exoALMA Large Program: To deal with decoherence between execution blocks; one important step in the self-calibration process. To be released as part of the exoALMA publications.

````

<!-- <a href="https://" target="_blank">target</a> -->

````{card} Data Reduction Visit to the NAASC (f2f)

I visited the North American ALMA Science Center (NAASC) in Charlottesville, VA for a week in Nov. 2022 and worked with Staff Scientist Ryan Loomis and Data Analysts Sarah Wood and Tristan Ashton. Their science support and guidance with the reduction and imaging of the ALMA data was invaluable. It was during this week that the big picture (the workflow [Breakdown of Our Task](overview-breakdown.md)) came together for me. The visit was fully funded by the NAASC and computational resources were provided on NAASC/NRAO clusters. I cannot recommend this program highly enough. <a href="https://science.nrao.edu/facilities/alma/visitors-shortterm" target="_blank">Learn about f2f visits here!</a>

````
