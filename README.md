# catsHTM
The `SLAB-Diffusion` package is a tool for modeling the diffusion of photons through a slab of CSM, e.g. in order to simulate the observables (effective blackbody temperature and radius) of an interacting Supernova.

[![PyPI](https://img.shields.io/pypi/v/SLAB-Diffusion.svg?style=flat-square)](https://pypi.python.org/pypi/SLAB-Diffusion)

```python
>>> import SLAB-Diffusion
>>> 
```

## Documenation

The HDF5/HTM format, designed to store and provide fast access for large astronomical catalogs (with >10^6 rows) is described in the [preliminary documentation](https://webhome.weizmann.ac.il/home/eofek/matlab/doc/catsHTM.html), together with the `Matlab` version.

The `catsHTM` package is also described in a paper by [Soumagnac & Ofek 2018](https://arxiv.org/abs/1805.02666).

## Credit
If you are using SLAB-Diffusion, please reference Soumagnac et al. 2018 

[Bibtex entry for Soumagnac et al. 2018]()

## How to install the `SLAB-Diffusion` code?

### pip

`pip install SLAB-Diffusion`

### Python version
* `python 2`: higher than `2.7.10`
* `python 3`

### Required python packages
* `math`
* `numpy`

## How to make a cone search with ``catsHTM``?

First, you need to specify the path to the directory where the HDF5 formatted catalogs where downloaded (default is `./data`). This will only work if you have previously downloaded the catalogs in HDF5 format (in order to download them, see section on 'How to obtain the formatted catalogs'):

```python
>>> import catsHTM
>>> path='path/to/directory'
```
You can then call the `cone_search` function. For example, to look for the sources in a cone of 100 arcsec centered on RA=0 rad and DEC=0 rad, in the FIRST catalog, type:
```python
>>> cat,colcell, colunits=catsHTM.cone_search('FIRST',0,0,100,catalogs_dir=path)
```
The catalog lines corresponding to the sources within the cone are stored in the `numpy` array `cat`:
```python
>>> print cat
[[  6.28300408e+00  -7.24311612e-05   1.68128476e-01   7.59999990e-01
    6.70588255e-01   9.23669338e-02   4.30000019e+00   0.00000000e+00
    6.20000000e+01   7.13999987e+00   4.32999992e+00   5.32000008e+01
    2.45002071e+06   2.45247496e+06]]
```
If you set the optionnal argument verbose to be true, you will get a line with a summary of your search:
```python
>>> cat,colcell, colunits=catsHTM.cone_search('FIRST',0,0,100,catalogs_dir=path, verbose=True)
>>> print cat
*************
Catalog: FIRST; cone radius: 100 arcsec; cone center: (RA,DEC)=(0,0)
*************
[[  6.28300408e+00  -7.24311612e-05   1.68128476e-01   7.59999990e-01
    6.70588255e-01   9.23669338e-02   4.30000019e+00   0.00000000e+00
    6.20000000e+01   7.13999987e+00   4.32999992e+00   5.32000008e+01
    2.45002071e+06   2.45247496e+06]]
```

The names of the catalog columns are stored in the `numpy` array `colcell`

```python
>>> print colcell
['RA' 'Dec' 'SideProb' 'Fpeak' 'Fint' 'rms' 'Major' 'Minor' 'PosAng'
 'FitMajor' 'FitMinor' 'FitPosAng' 'StartMJD' 'StopMJD']
```
The units of the catalog columns are stored in the `numpy` array `colunits`

```python
>>> print colunits
[u'rad' u'rad' ' ' u'mJy' u'mJy' u'mJy' u'arcsec' u'arcsec' u'deg'
 u'arcsec' u'arcsec' u'deg' u'MJD' u'MJD']
```

