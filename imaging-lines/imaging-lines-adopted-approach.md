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

# Adopted Approach

Relevant script: [adopted approach](imaging-lines-adopted-approach.md).
<a href="https://github.com/jjspeedie/workflow.2021.1.0690.S/blob/main/major_image_lines.py" target="_blank">major_image_lines.py</a>

All imaging was performed with the {\sc CASA} \texttt{tclean} task.
% Our imaging strategy diverged from that of the {\sc DSHARP}\cite{andrews2018-dsharp1} and {\sc MAPS}\cite{oberg2021-maps1} programs.
We used the multiscale %, multifrequency synthesis (assuming a flat spectrum)
deconvolution algorithm\cite{cornwell2008} with
% The adopted
(Gaussian) deconvolution scales [$0.02''$, $0.1''$, $0.3''$, $0.6''$, $1.0''$].
We did not image with a Keplerian mask so as not to restrict our ability to observe non-Keplerian emission.
After experimentation with {\sc CASA}'s auto-multithresh masking algorithm\cite{kepley2020-automultithresh}, we adopted  
an imaging strategy similar to {\sc PHANGS-ALMA}\cite{leroy2021-phangsalma},  

```
# Cautious/conservative clean:
cycleniter             = 80    # Jess: Maximum number of minor-cycle iterations (per plane) before triggering a major cycle
cyclefactor            = 3.0   # Ryan: 3x max_psf_sidelobe_level as minor cycle threshold (default is 1.0)
gain                   = 0.02  # Ryan: assign clean component peaks to 2% of pixel value (default is 0.1)
minpsffraction         = 0.5   # PHANGS: cycle threshold is never lower than 0.5 times the peak residual (default: 0.05)
```

in which we clean conservatively, with a broad mask (\texttt{usemask='pb'} and \texttt{pbmask=0.2}), forcing frequent major cycles\footnote{The $^{13}$CO robust 0.5 cube underwent 198 major cycles and the C$^{18}$O cube underwent 76.}.
To achieve frequent major cycles we set
the maximum number of minor cycle iterations per channel to \texttt{cycleniter=80},
the minor cycle threshold to \texttt{max\_psf\_sidelobe\_level=3.0} and \texttt{minpsffraction=0.5},
and the maximum assigned clean component to \texttt{gain=0.02} times the peak residual.
We adopted a Briggs robust weighting scheme, and generated two sets of image cubes; one with a robust value of $0.5$ and a second with robust $1.5$.
The corresponding beam sizes for $^{13}$CO are $237\times175$ mas, $1.2^\circ$ for robust $0.5$ and $390\times274$ mas, $-1.4^\circ$ for robust $1.5$. %(with similar results for C$^{18}$O
We imaged \rev{with a FOV} out to the primary beam FWHM ($38''$) with $0.02''$ pixels ($9$ or $12$ pixels per synthesized beam minor or major axis, respectively). % 0.175 x 0.237'' beam
We imaged in LSRK velocity channels at $42$ m/s for $^{13}$CO and $84$ m/s for C$^{18}$O respectively (nearly native channel spacing).
The \texttt{CLEAN} threshold was set to $5\times$ the rms noise measured in $20$ line-free channels %(first and last 10 channels)
of the dirty image cube.
We applied JvM correction\cite{JvM1995-correction, czekala2021-maps2} and primary beam correction. The rms \rev{noise in} the resulting $^{13}$CO \rev{cubes imaged with robust $0.5$ and robust $1.5$} is $2.0$ mJy/beam and $1.2$ mJy/beam respectively, \rev{and $0.6$ mJy/beam in the C$^{18}$O cube imaged with robust $1.5$.}
