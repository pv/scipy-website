.. _building.linux:

===========================================
Building NumPy & SciPy From Source on Linux
===========================================

.. toctree::
   :hidden:

   linux-distspecific


Introduction : source and binaries
----------------------------------

* On Linux, Scipy and Numpy official releases are source-code
  only. Installing Numpy and Scipy from source is reasonably easy;
  However, both packages depend on other software, some of which can
  be challenging to install, or shipped with incompatibilities by
  major Linux distributions. Hopefully, you can install Numpy and
  Scipy without any software outside the necessary tools to build
  python extensions, as most dependencies are optional.

* Most major Linux distributions now ship Numpy and Scipy and,
  although the situation is not completely optimal, those binary
  packages are now reasonably reliable to use. Many other binary
  options are also available, ranging from individually made packages
  by some scipy developers for a specific Linux version, to whole
  commercially-supported scientific distributions. However, keep in
  mind that if you want to use the last improvements done to Numpy
  and Scipy on Linux, you often need to build it from sources.

You will find below generic installation instructions, and some
further advice for most major distributions is in
:ref:`building.linux-distspecific`.


Generic instructions
--------------------

To build Numpy and Scipy, you will need to have the following software
installed

- C compiler (gcc)
- For Scipy: Fortran compiler (gfortran)
- Python development headers (python-dev, python-devel)
- BLAS library (libblas-dev, blas-devel)
- LAPACK library (liblapack-dev, lapack-devel)

Typically, your operating system vendor provides all of these. Typical
package names are indicated in the above list.

Numpy and Scipy are ordinary Python packages, so you will need to
decide whether to install them system-wide or only for yourself, in the
usual way.  Typical system-wide installation is done by::

    python setup.py build
    sudo python setup.py install --prefix=/usr/local

and, on Python 2.6 or newer, you can install also only for yourself::

    python setup.py install --user

For more options, refer to the `Python module installation documentation
<http://docs.python.org/install/index.html>`__.

You can select the C compiler to use in the build by::

    python setup.py build --help-compiler
    python setup.py build --compiler=gnu95

and similarly for the Fortran compiler::

    python setup.py build --help-fcompiler
    python setup.py build --fcompiler=gnu95

If your LAPACK and BLAS libraries are located in non-standard places,
you can specify them by doing::

    BLAS=/usr/lib/libblas.so LAPACK=/usr/lib/liblapack.so python setup.py build

Above, correct the paths according to your setup.

.. note::

   If you want to install using the Python egg machinery instead of
   standard installation, use ``setupegg.py``. This is important in
   some cases, as packages installed as eggs have priority over a
   standard installation.

After successful installation, be sure to do

    >>> import numpy
    >>> print numpy.__version__
    >>> print numpy.__file__
    >>> numpy.test()

to check that (i) Python finds the correct version of Numpy, (ii) it
finds it from the location where you installed it, and (iii) that your
installation is working as expected. If installation is correct,
``numpy.test()`` reports no failed tests or errors.


Building with MKL
#################

.. todo::

   Explain how to do this.


Lapack and Atlas problems
#########################

In some cases, ``numpy.test()`` reveals problems in the BLAS and
LAPACK linear algebra libraries. You can recognize these if the
failing tests have to do with linear algebra routines such as SVD.

When there are issues, you have the following options:

1) Check if your OS vendor provides updated LAPACK or BLAS packages
   fixing these problems.

2) Check if fixed packages are available from third parties.

3) Build LAPACK and BLAS yourself.

Some instructions for 2) and 3) for different Linux distributions
can be found in :ref:`building.linux-distspecific`.
