# Direct X-ray Spectra Deprojection

This page contains the source code for the Direct Spectral Deprojection code described in the appendix of [Sanders & Fabian (2007)](http://adsabs.harvard.edu/abs/2007MNRAS.381.1381S) and tested and detailed further by [Russell, Sanders & Fabian (2008)](http://adsabs.harvard.edu/abs/2008MNRAS.390.1207R).

## Installation

You need to have Python 3, numpy and astropy installed.

## Instructions

You need to have numbered ungrouped spectra for each shell. Assign background files to the spectra with the BACKSCAL keyword. The XFLTxxxx header keywords in the spectrum need to be defined as for the projct model in Xspec:

```
XFLT0001 = outer radius of shell in some units
XFLT0002...0003 are ignored
XFLT0004 = starting angle (optional)
XFLT0005 = stopping angle (optional)
XLFT.... = more starting and stopping angles as required
          (assumes 360 degrees if no angles are specified)
          Only spherical geometry is currently allowed.
```

Just run the script as
```
deproject_spectra.py ann_ .spec 1 10 0. ann_ .deproj
```

If the input spectra are called `ann_1.spec` to `ann_10.spec`, writing `ann_1.deproj` to `ann_10.deproj`. In detail the arguments are:
```
ann_    = input prefix
.spec   = input suffix
1       = spectrum starting number
10      = number of spectra
0.      = inner radius of 1st spectrum (same units as XFLT0001)
ann_    = prefix of output files
.deproj = suffix of output files
```

## Notes

* Output spectra are normalised to have unit volume (in the same units as the XFLT0001 keywords).  You need this volume to convert norms to densities, etc.
* If a background is defined in the spectrum in the BACKFILE keyword, it is subtracted first before deprojecting.
* Poisson errors are assumed in the input spectra and backgrounds.
* Spectra are automatically grouped by the program (to have 25 cts in each channel for each spectrum, using the same channels for all spectra).
* You can just fit the deprojected spectra in xspec with simple models. 

## Bug reports and questions
Please use the bug tracker on this github page.
