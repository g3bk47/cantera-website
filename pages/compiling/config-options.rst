.. title: Configuration Options

.. _scons-config:

.. jumbotron::

   .. raw:: html

      <h1 class="display-3">Configuration Options</h1>

   .. class:: lead

      This document lists the options available for compiling Cantera with
      SCons. This list is for the current release of Cantera, version 2.5.1. For
      the development version, see `this list <config-options-dev.html>`_.

   The default values are operating-system dependent. To see the defaults for your current operating
   system, run the command:

   .. code:: bash

      scons help

   from the command prompt.

   The following options can be passed to SCons to customize the Cantera
   build process. They should be given in the form:

   .. code:: bash

      scons build option1=value1 option2=value2

   Variables set in this way will be stored in the ``cantera.conf`` file and reused
   automatically on subsequent invocations of SCons. Alternatively, the
   configuration options can be entered directly into ``cantera.conf`` before
   running ``scons build``. The format of this file is:

   .. code:: python

      option1 = 'value1'
      option2 = 'value2'

Options List
^^^^^^^^^^^^

.. _msvc-version:

* ``msvc_version``: [ ``string`` ]
    Version of Visual Studio to use. The default is the newest
    installed version. Specify ``12.0`` for Visual Studio 2013 or ``14.0``
    for Visual Studio 2015. Windows MSVC only.

    - default: ``''``

.. _target-arch:

* ``target_arch``: [ ``amd64`` | ``x86`` ]
    Target architecture. The default is the same architecture as the
    installed version of Python. Windows only.

    - default: ``''``

.. _toolchain:

* ``toolchain``: [ ``msvc`` | ``mingw`` | ``intel`` ]
    The preferred compiler toolchain. Windows only.

    - default:

      - ``g++`` is on the path, MSVC is not on the path, and ``msvc_version``
        is not specified: ``'mingw'``
      - Otherwise: ``'msvc'``

.. _cxx:

* ``CXX``: [ ``string`` ]
    The C++ compiler to use.

    - default: ``''``

.. _cc:

* ``CC``: [ ``string`` ]
    The C compiler to use. This is only used to compile CVODE.

    - default: ``''``

.. _prefix:

* ``prefix``: [ ``path/to/prefix`` ]
    Set this to the directory where Cantera should be installed.

    - default:

      - Linux / macOS / other Unix systems: ``'/usr/local'``
      - Windows: ``'C:\Program Files\Cantera'``

.. _libdirname:

* ``libdirname``: [ ``path/to/libdirname`` ]
    Set this to the directory where Cantera libraries should be installed.
    Some distributions (for example, Fedora/RHEL) use ``lib64`` instead of ``lib`` on 64-bit systems
    or could use some other library directory name instead of ``lib`` depends
    on architecture and profile (for example, Gentoo ``libx32`` on x32 profile).
    If user didn't set ``libdirname`` configuration variable set it to default value ``lib``

    - default: ``'lib'``

.. _python-package:

* ``python_package``: [ ``y`` | ``n`` | ``new`` | ``full`` | ``minimal`` | ``none`` | ``default`` ]
    If you plan to work in Python, then you need the ``full`` Cantera Python
    package. If, on the other hand, you will only use Cantera from some
    other language (for example, MATLAB or Fortran 90/95) and only need Python
    to process CTI files, then you only need a ``minimal`` subset of the
    package and Cython and NumPy are not necessary. The ``none`` option
    doesn't install any components of the Python interface. The default
    behavior is to build the full Python module for whichever version of
    Python is running SCons if the required prerequisites (NumPy and
    Cython) are installed. Note: ``y`` is a synonym for ``full`` and ``n``
    is a synonym for ``none``.

    - default: ``'default'``

.. _python-cmd:

* ``python_cmd``: [ ``path/to/python_cmd`` ]
    Cantera needs to know where to find the Python interpreter. If
    PYTHON_CMD is not set, then the configuration process will use the
    same Python interpreter being used by SCons.

    - default: ``''``

.. _python-prefix:

* ``python_prefix``: [ ``path/to/python_prefix`` ]
    Use this option if you want to install the Cantera Python package to
    an alternate location. On Unix-like systems, the default is the same
    as the ``prefix`` option. If the ``python_prefix`` option is set to
    the empty string or the ``prefix`` option is not set, then the package
    will be installed to the system default ``site-packages`` directory.
    To install to the current user's ``site-packages`` directory, use
    ``python_prefix=USER``.

    - default:

      - Windows: ``''``
      - Otherwise: ``'$prefix'``

.. _python3-package:

* ``python3_package``: [ ``y`` | ``n`` | ``full`` | ``minimal`` | ``none`` | ``default`` ]
    Deprecated synonym for the ``python_package`` option. Will be overridden
    if ``python_package`` is set.

    - default: ``'default'``

.. _python3-cmd:

* ``python3_cmd``: [ ``path/to/python3_cmd`` ]
    Deprecated synonym for the ``python_cmd`` option. Will be overridden
    if ``python_cmd`` is set.

    - default: ``''``

.. _python3-prefix:

* ``python3_prefix``: [ ``path/to/python3_prefix`` ]
    Deprecated synonym for the ``python_prefix`` option. Will be overridden
    if ``python_prefix`` is set.

    - default: ``''``

.. _matlab-toolbox:

* ``matlab_toolbox``: [ ``y`` | ``n`` | ``default`` ]
    This variable controls whether the MATLAB toolbox will be built. If
    set to ``y``, you will also need to set the value of the ``matlab_path``
    variable. If set to ``default``, the MATLAB toolbox will be built if
    ``matlab_path`` is set.

    - default: ``'default'``

.. _matlab-path:

* ``matlab_path``: [ ``path/to/matlab_path`` ]
    Path to the MATLAB install directory. This should be the directory
    containing the ``extern``, ``bin``, etc. subdirectories. Typical values
    are: ``"C:/Program Files/MATLAB/R2011a"`` on Windows,
    ``"/Applications/MATLAB_R2011a.app"`` on OS X, or
    ``"/opt/MATLAB/R2011a"`` on Linux.

    - default: ``''``

.. _f90-interface:

* ``f90_interface``: [ ``y`` | ``n`` | ``default`` ]
    This variable controls whether the Fortran 90/95 interface will be
    built. If set to ``default``, the builder will look for a compatible
    Fortran compiler in the ``PATH`` environment variable, and compile
    the Fortran 90 interface if one is found.

    - default: ``'default'``

.. _fortran:

* ``FORTRAN``: [ ``path/to/FORTRAN`` ]
    The Fortran (90) compiler. If unspecified, the builder will look for
    a compatible compiler (pgfortran, gfortran, ifort, g95) in the ``PATH`` environment
    variable. Used only for compiling the Fortran 90 interface.

    - default: ``''``

.. _FORTRANFLAGS:

* ``FORTRANFLAGS``: [ ``string`` ]
    Compilation options for the Fortran (90) compiler.

    - default: ``'-O3'``

.. _coverage:

* ``coverage``: [ ``yes`` | ``no`` ]
    Enable collection of code coverage information with gcov.
    Available only when compiling with gcc.

    - default: ``'no'``

.. _doxygen-docs:

* ``doxygen_docs``: [ ``yes`` | ``no`` ]
    Build HTML documentation for the C++ interface using Doxygen.

    - default: ``'no'``

.. _sphinx-docs:

* ``sphinx_docs``: [ ``yes`` | ``no`` ]
    Build HTML documentation for Cantera using Sphinx.

    - default: ``'no'``

.. _sphinx-cmd:

* ``sphinx_cmd``: [ ``path/to/sphinx_cmd`` ]
    Command to use for building the Sphinx documentation.

    - default: ``'sphinx-build'``

.. _sphinx-options:

* ``sphinx_options``: [ ``string`` ]
    Options passed to the ``sphinx_cmd`` command line. Separate multiple
    options with spaces, for example, ``"-W --keep-going"``.

    - default: ``''``

.. _system-eigen:

* ``system_eigen``: [ ``y`` | ``n`` | ``default`` ]
    Select whether to use Eigen from a system installation (``y``), from a
    Git submodule (``n``), or to decide automatically (``default``). If Eigen
    is not installed directly into a system include directory, for example, it is
    installed in ``/opt/include/eigen3/Eigen``, then you will need to add
    ``/opt/include/eigen3`` to ``extra_inc_dirs``.

    - default: ``'default'``

.. _system-fmt:

* ``system_fmt``: [ ``y`` | ``n`` | ``default`` ]
    Select whether to use the fmt library from a system installation
    (``y``), from a Git submodule (``n``), or to decide automatically
    (``default``).

    - default: ``'default'``

.. _system-yamlcpp:

* ``system_yamlcpp``: [ ``y`` | ``n`` | ``default`` ]
    Select whether to use the yaml-cpp library from a system installation
    (``y``), from a Git submodule (``n``), or to decide automatically
    (``default``). If yaml-cpp is not installed directly into system
    include and library directories, then you will need to add those
    directories to ``extra_inc_dirs`` and ``extra_lib_dirs``.

    - default: ``'default'``

.. _system-sundials:

* ``system_sundials``: [ ``y`` | ``n`` | ``default`` ]
    Select whether to use SUNDIALS from a system installation (``y``), from
    a Git submodule (``n``), or to decide automatically (``default``).
    Specifying ``sundials_include`` or ``sundials_libdir`` changes the
    default to ``y``.

    - default: ``'default'``

.. _sundials-include:

* ``sundials_include``: [ ``path/to/sundials_include`` ]
    The directory where the SUNDIALS header files are installed. This
    should be the directory that contains the ``"cvodes"``, ``"nvector"``, etc.
    subdirectories. Not needed if the headers are installed in a
    standard location, for example, ``/usr/include``.

    - default: ``''``

.. _sundials-libdir:

* ``sundials_libdir``: [ ``path/to/sundials_libdir`` ]
    The directory where the SUNDIALS static libraries are installed.
    Not needed if the libraries are installed in a standard location,
    for example, ``/usr/lib``.

    - default: ``''``

.. _blas-lapack-libs:

* ``blas_lapack_libs``: [ ``string`` ]
    Cantera can use BLAS and LAPACK libraries available on your system if
    you have optimized versions available (for example, Intel MKL). Otherwise,
    Cantera will use Eigen for linear algebra support. To use BLAS
    and LAPACK, set ``blas_lapack_libs`` to the the list of libraries
    that should be passed to the linker, separated by commas, for example,
    ``"lapack,blas"`` or ``"lapack,f77blas,cblas,atlas"``. Eigen is required
    whether or not BLAS/LAPACK are used.

    - default: ``''``

.. _blas-lapack-dir:

* ``blas_lapack_dir``: [ ``path/to/blas_lapack_dir`` ]
    Directory containing the libraries specified by ``blas_lapack_libs``. Not
    needed if the libraries are installed in a standard location, for example,
    ``/usr/lib``.

    - default: ``''``

.. _lapack-names:

* ``lapack_names``: [ ``lower`` | ``upper`` ]
    Set depending on whether the procedure names in the specified
    libraries are lowercase or uppercase. If you don't know, run ``nm`` on
    the library file (for example, ``"nm libblas.a"``).

    - default: ``'lower'``

.. _lapack-ftn-trailing-underscore:

* ``lapack_ftn_trailing_underscore``: [ ``yes`` | ``no`` ]
    Controls whether the LAPACK functions have a trailing underscore
    in the Fortran libraries.

    - default: ``'yes'``

.. _lapack-ftn-string-len-at-end:

* ``lapack_ftn_string_len_at_end``: [ ``yes`` | ``no`` ]
    Controls whether the LAPACK functions have the string length
    argument at the end of the argument list (``yes``) or after
    each argument (``no``) in the Fortran libraries.

    - default: ``'yes'``

.. _system-googletest:

* ``system_googletest``: [ ``y`` | ``n`` | ``unspecified`` | ``default`` ]
    Select whether to use gtest/gmock from system
    installation (``y``), from a Git submodule (``n``), or to decide
    automatically (``default``). Deprecated option, please use ``googletest`` instead.
    This option is suppressed by ``googletest`` option.

    - default: ``'unspecified'``

.. _googletest:

* ``googletest``: [ ``default`` | ``system`` | ``submodule`` | ``none`` ]
    Select whether to use gtest/gmock from system
    installation (``system``), from a Git submodule (``submodule``), to decide
    automatically (``default``) or don't look for gtest/gmock (``none``)
    and don't run tests that depend on gtest/gmock. If this option is
    set then it suppresses the deprecated ``system_googletest`` option.

    - default: ``'default'``

.. _env-vars:

* ``env_vars``: [ ``string`` ]
    Environment variables to propagate through to SCons. Either the
    string ``"all"`` or a comma separated list of variable names, for example,
    ``LD_LIBRARY_PATH,HOME``.

    - default: ``''``

.. _use-pch:

* ``use_pch``: [ ``yes`` | ``no`` ]
    Use a precompiled-header to speed up compilation

    - default:

      - If using the Intel C/C++ compiler: ``'no'``
      - Otherwise: ``'yes'``

.. _cxx-flags:

* ``cxx_flags``: [ ``string`` ]
    Compiler flags passed to the C++ compiler only. Separate multiple
    options with spaces, for example, ``"cxx_flags='-g -Wextra -O3 --std=c++11'"``

    - default:

      - If using GCC: ``'-std=c++0x'``
      - If using GCC on Cygwin: ``'-std=gnu++0x'``
      - If using MSVC: ``'/EHsc'``
      - If using Clang: ``'-std=c++11'``
      - If using ICC: ``'-std=c++0x'``

.. _cc-flags:

* ``cc_flags``: [ ``string`` ]
    Compiler flags passed to both the C and C++ compilers, regardless of optimization level.

    - default:

      - If using GCC: ``'-std=c++0x'``
      - If using GCC on Cygwin: ``'-std=gnu++0x'``
      - If using MSVC: ``'/EHsc'``
      - If using Clang: ``'-std=c++11'``
      - If using ICC: ``'-std=c++0x'``

.. _thread-flags:

* ``thread_flags``: [ ``string`` ]
    Compiler and linker flags for POSIX multithreading support.

    - default:

      - If compiling on Windows: ``''``
      - Otherwise: ``'-pthread'``

.. _optimize:

* ``optimize``: [ ``yes`` | ``no`` ]
    Enable extra compiler optimizations specified by the
    ``optimize_flags`` variable, instead of the flags specified by the
    ``no_optimize_flags`` variable.

    - default: ``'yes'``

.. _optimize-flags:

* ``optimize_flags``: [ ``string`` ]
    Additional compiler flags passed to the C/C++ compiler when ``optimize=yes``.

    - default:

      - If using GCC: ``'-O3 -Wno-inline'``
      - If using MSVC: ``'/O2'``
      - If using Clang: ``'-O3'``
      - If using ICC: ``'-O3'``

.. _no-optimize-flags:

* ``no_optimize_flags``: [ ``string`` ]
    Additional compiler flags passed to the C/C++ compiler when ``optimize=no``.

    - default:

      - If using MSVC: ``'/Od /Ob0'``
      - Otherwise: ``'-O0'``

.. _debug:

* ``debug``: [ ``yes`` | ``no`` ]
    Enable compiler debugging symbols.

    - default: ``'yes'``

.. _debug-flags:

* ``debug_flags``: [ ``string`` ]
    Additional compiler flags passed to the C/C++ compiler when ``debug=yes``.

    - default:

      - If using MSVC: ``'/Zi /Fd${TARGET}.pdb'``
      - Otherwise: ``'-g'``

.. _no-debug-flags:

* ``no_debug_flags``: [ ``string`` ]
    Additional compiler flags passed to the C/C++ compiler when ``debug=no``.

    - default: ``''``

.. _debug-linker-flags:

* ``debug_linker_flags``: [ ``string`` ]
    Additional options passed to the linker when ``debug=yes``.

    - default:

      - If using MSVC: ``'/DEBUG'``
      - Otherwise: ``''``

.. _no-debug-linker-flags:

* ``no_debug_linker_flags``: [ ``string`` ]
    Additional options passed to the linker when ``debug=no``.

    - default: ``''``

.. _warning-flags:

* ``warning_flags``: [ ``string`` ]
    Additional compiler flags passed to the C/C++ compiler to enable
    extra warnings. Used only when compiling source code that is part
    of Cantera (for example, excluding code in the ``ext`` directory).

    - default:

      - If using MSVC: ``'/W3'``
      - If using ICC: ``'-Wcheck'``
      - Otherwise: ``'-Wall'``

.. _extra-inc-dirs:

* ``extra_inc_dirs``: [ ``string`` ]
    Additional directories to search for header files, with multiple
    directories separated by colons (\*nix, macOS) or semicolons (Windows)

    - default: ``''``

.. _extra-lib-dirs:

* ``extra_lib_dirs``: [ ``string`` ]
    Additional directories to search for libraries, with multiple
    directories separated by colons (\*nix, macOS) or semicolons (Windows)

    - default: ``''``

.. _boost-inc-dir:

* ``boost_inc_dir``: [ ``path/to/boost_inc_dir`` ]
    Location of the Boost header files. Not needed if the headers are
    installed in a standard location, for example, ``/usr/include``.

    - default: ``''``

.. _stage-dir:

* ``stage_dir``: [ ``path/to/stage_dir`` ]
    Directory relative to the Cantera source directory to be
    used as a staging area for building for example, a Debian
    package. If specified, 'scons install' will install files
    to ``stage_dir/prefix/...``.

    - default: ``''``

.. _verbose:

* ``VERBOSE``: [ ``yes`` | ``no`` ]
    Create verbose output about what SCons is doing.

    - default: ``'no'``

.. _gtest-flags:

* ``gtest_flags``: [ ``string`` ]
    Additional options passed to each GTest test suite, for example,
    '--gtest_filter=*pattern*'. Separate multiple options with spaces.

    - default: ``''``

.. _renamed-shared-libraries:

* ``renamed_shared_libraries``: [ ``yes`` | ``no`` ]
    If this option is turned on, the shared libraries that are created
    will be renamed to have a ``_shared`` extension added to their base name.
    If not, the base names will be the same as the static libraries.
    In some cases this simplifies subsequent linking environments with
    static libraries and avoids a bug with using valgrind with
    the ``-static`` linking flag.

    - default: ``'yes'``

.. _versioned-shared-library:

* ``versioned_shared_library``: [ ``yes`` | ``no`` ]
    If enabled, create a versioned shared library, with symlinks to the
    more generic library name, for example, ``libcantera_shared.so.2.5.0`` as the
    actual library and ``libcantera_shared.so`` and ``libcantera_shared.so.2``
    as symlinks.

    - default:

      - If compiling with MinGW or when using SCons < 2.4.0: ``'no'``
      - Otherwise: ``'yes'``

.. _use-rpath-linkage:

* ``use_rpath_linkage``: [ ``yes`` | ``no`` ]
    If enabled, link to all shared libraries using ``rpath``, i.e., a fixed
    run-time search path for dynamic library loading.

    - default: ``'yes'``

.. _layout:

* ``layout``: [ ``standard`` | ``compact`` | ``debian`` ]
    The layout of the directory structure. ``standard`` installs files to
    several subdirectories under 'prefix', for example, ``prefix/bin``,
    ``prefix/include/cantera``, ``prefix/lib`` etc. This layout is best used in
    conjunction with ``"prefix='/usr/local'"``. ``compact`` puts all installed
    files in the subdirectory defined by 'prefix'. This layout is best
    with a prefix like ``/opt/cantera``. ``debian`` installs to the stage
    directory in a layout used for generating Debian packages.

    - default:

      - Windows: ``'compact'``
      - Otherwise: ``'standard'``

.. _fast-fail-tests:

* ``fast_fail_tests``: [ ``yes`` | ``no`` ]
    If enabled, tests will exit at the first failure.

    - default: ``'no'``

