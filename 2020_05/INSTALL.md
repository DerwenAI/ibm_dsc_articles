Using `conda` for the required installations works like magic.
Except when it doesn't.

If it's the latter case ... after about 2–3 hours of chasing answers and
comments on StackOverflow, swearing, pouring through GitHub issues to
test every elusive option mentioned, swearing some more, inadvertently
frightening the cat, etc., you may get portions of geoplot to install
correctly.

One difficulty is that geoplot builds atop several other packages.
Some may trigger the infamous "conda: Solving environment" infinite
spinner.

Nonetheless, conda is a favorite of many people for installing Python
packages. It's especially brilliant to use for Jupyter, spaCy, etc.
Anaconda has published notes about how to improve its performance, as
a possible workaround:

<https://www.anaconda.com/understanding-and-improving-condas-performance/>

QuantStack released a conda-compatible package manager called mamba
which is much faster, although no guarantees about resolving these
installation issues:

<https://medium.com/@wolfv/making-conda-fast-again-4da4debfb3b7>

While developing this tutorial, conda installers failed on an
up-to-date macOS laptop, then again on a pristine cloud server
instance running Ubuntu 18.04 LTS. That indicates trouble ahead in
Python installation land...

Another alternative is to use pip and PyPi. One of the differences
between conda and pip is how the latter can also build
[wheels](https://pythonwheels.com/) as binary distributions. That
leads to faster installation for pure Python packages. However, when a
library builds on top of low-level libraries in C or C++ (or FORTRAN)
then it may be necessary to skip the binaries – ignore the
pre-compiled wheels – and instead force compilation from source code
within your environment.

We've tried to save people some time and agony by describing an
installation recipe that works on a pristine Ubuntu 18.04 LTS
server. First, install the libraries that may require admin
privileges:

```
sudo apt-get update
sudo apt-get install virtualenv python-pip python-dev python3-dev

sudo apt-get install libproj-dev proj-data proj-bin
sudo apt-get install libgeos-dev
sudo apt-get install libspatialindex-dev
```

Then create a virtual environment for Python3 and activate it:

```
virtualenv -p python3 ~/venv
source ~/venv/bin/activate
```

Now install the Python dependencies into that virtual environment:

```
pip install -r requirements.txt

pip install shapely --no-binary shapely 
pip install git+https://github.com/SciTools/cartopy.git --no-binary cartopy
pip install pysal --no-binary pysal

pip install geopandas
pip install geoplot
```

Notice two subtle points about this approach:

  * `Cython` and `descartes` get installed early in the sequence
  * `shapely`, `cartopy`, and `pysal` require the `--no-binary` option

Okay, that approach – or something similar – should work on a recent
release of Ubuntu/Debian Linux.

BTW, compared with what the installation of geospatial libraries
required a decade ago, these steps are simple!

If you have Windows you'll probably have other issues to
resolve. YMMV.

If you're using a Mac, well there's [`brew`](https://brew.sh/) and
many swear by it, while many others swear at it, since use of `brew`
may cause other installed dependencies to get mangled.
