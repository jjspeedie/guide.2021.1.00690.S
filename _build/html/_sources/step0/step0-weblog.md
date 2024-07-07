# Inspecting the Weblog

The importance and helpfulness of the weblog cannot be emphasized enough.

One weblog is generated for each run of the ALMA pipeline. For the present program, that means there are two weblogs -- one for each of the TM1 and TM2 scheduling blocks.

For an all-encompassing and very comprehensive overview of what to look at, see <a href="https://almascience.eso.org/euarcdata/itrain04/weblog.pdf" target="_blank">Reviewing the WebLog by George Bendo</a> (slide 13 is where it gets started).




````{admonition} Find the weblog in the "qa" directory.
:class: tip, dropdown

Once downloaded and untarred, all data should fall into the standardized directory structure:

```{card}
<img src="./images/directory-structure.png" alt="directory-structure" class="mb-1" width="100%">
```

**(1)** The ALMA project code, or program ID. Ours is ``2021.1.00690.S``.

**(2)** The Science Goal ID. These are originally set up by the PI in the OT during proposal preparation. We have just one: ``uid___A001_X15a2_Xb69``.

**(3)** The Group ObsUnitSet (a.k.a. GOUS). In our case there is just one: ``uid___A001_X15a2_Xb6a``.

**(4)** The Member ObsUnitSet (a.k.a MOUS, a.k.a. Scheduling Block, a.k.a. SB). QA2 is carried out at this level. In our case, we have two (``uid___A001_X15a2_Xb6b`` and ``uid___A001_X15a2_Xb6d``) -- one for each array configuration. The long-baseline configuration MOUS is also referred to as TM1, and the short-baseline configuration as TM2. The pipeline is run on each MOUS separately (and thus also delivered to the PI separately) -- at least as of Cycle 8!

Each of our MOUSes contain multiple execution blocks (EBs). QA0 is carried out on the EB level. All of the following directories **(6-11)** contain all the files for each EB in each MOUS, where the file name starts with the EB ID. For example, our TM2 (short-baseline MOUS) directories contain all the files for EB1 ``uid___A002_Xf7ad58_Xd406`` and for EB2 ``uid___A002_Xf8f6a9_X15c79``.

**(5)** A very helpful file that explains the directory structure and file types.

**(6)** Contains the pipeline-generated image products (fits files).

**(7)** Contains the all-important calibration tables, and other things for restoring the pipeline calibration.

**(8)** Contains the blessing that is the Weblog. It also contains the Quality Assurance (QA) reports on the MOUS level (QA1) and the EB level (QA0).

**(9)** Contains the absolutely crucial ``scriptForPI.py`` -- what you need to restore the pipeline calibration.

**(10)** Contains the CASA commands log from the QA2 processing.

**(11)** Contains the data! The raw visibilities in the native ALMA format (the ASDM). In our case:

```{card}
<img src="./images/directory-structure-EBs.png" alt="directory-structure-EBs" class="mb-1" width="100%">
```

More details can be found in <a href="https://almascience.nrao.edu/portal/documents-and-tools/cycle8/alma-qa2-data-products-for-cycle-8" target="_blank">ALMA QA2 Data Products for Cycle 8</a>, Section 3 and 4.

````

There is so much to refer to the weblog for, that it can't and won't be summarized here. For the purposes of the following step ([restoring the pipeline calibration](./step0-restoring-pipeline-calibration.md)), note where the appropriate CASA pipeline version can be found:

````{card}
<center>

<img src="images/weblog-CASA-version.png" alt="weblog-CASA-version" class="mb-1" width="100%">
</center>
+++
The version of CASA run by the pipeline is given on the front page of the weblog, under "Pipeline Summary".
````


## Quality assurance (QA) reports

These are almost like an extremely abridged version of the weblog. Some information is more easily accessed here, but there is little information that can't also be found somewhere in the weblog. (That said, it's nice to read the comments from the astronomer on duty!). For the present program, there are 10 QA reports in total: 8 QA0's for each execution block, and 2 QA2's for each of TM1 and TM2.
