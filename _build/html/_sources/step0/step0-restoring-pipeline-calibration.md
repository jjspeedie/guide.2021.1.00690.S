# Restoring the Pipeline Calibration

This was actually done for me the second time by NRAO; but the first time, I did it like this.


## Restoring the pipeline calibration using ``scriptForPI.py``

Note on where we begin:
We downloaded the entire data set from the ALMA Archive and restored the
pipeline calibration using scriptForPI.py to create .ms files for each execution.

## Splitting out the science spectral windows and target source

We then split out the science spectral windows, using the code:

```python
# In a CASA terminal, in e.g., member.uid___A001_X15a2_Xb6d/calibrated/
import glob
vislist = glob.glob('*[!_t].ms')  # should be ['uid___A002_Xf7ad58_Xd406.ms', 'uid___A002_Xf8f6a9_X15c79.ms']
for myvis in vislist:
    msmd.open(myvis)
    targetspws = msmd.spwsforintent('OBSERVE_TARGET*')
    sciencespws = []
    for myspw in targetspws:
        if msmd.nchan(myspw)>4:
            sciencespws.append(myspw)
    sciencespws = ','.join(map(str,sciencespws))
    msmd.close()
    split(vis=myvis,outputvis=myvis+'.split.cal',spw=sciencespws)
```

So, the ``.ms.split.cal`` measurement sets contain the science target AND the calibrators.

We then saved the original flags, using the code:

```python
# In a CASA terminal, in e.g., member.uid___A001_X15a2_Xb6d/calibrated/
import glob
vislist=glob.glob('*.ms.split.cal')
for vis in vislist:
    flagmanager(vis=vis,
                mode='save',
                versionname='original_flags')
```

After that, we split off the science target, and saved those flags, using the code:

```python
# In a CASA terminal, in e.g., member.uid___A001_X15a2_Xb6d/calibrated/
for vis in vislist:
    outputvis = vis+'.source'
    split(vis=vis,
      intent='*TARGET*', # split off the target sources by intent
      outputvis=outputvis,
      datacolumn='data')
    os.system('rm -rf ' + outputvis + '.flagversions')
    flagmanager(vis=outputvis,
                mode='save',
                versionname='original_flags')
```

In summary, we start [step 1](../step1/step1-manual-flags.md) with 8 separate measurement sets (e.g. ``uid___A002_Xf7ad58_Xd406.ms.split.cal.source``) which contain only the science spectral windows for only the science target.
