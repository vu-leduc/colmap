COLMAP
======

About
-----

COLMAP is a general-purpose Structure-from-Motion (SfM) and Multi-View Stereo
(MVS) pipeline with a graphical and command-line interface. It offers a wide
range of features for reconstruction of ordered and unordered image collections.
The software is licensed under the new BSD license. If you use this project for
your research, please cite:

    @inproceedings{schoenberger2016sfm,
        author={Sch\"{o}nberger, Johannes Lutz and Frahm, Jan-Michael},
        title={Structure-from-Motion Revisited},
        booktitle={Conference on Computer Vision and Pattern Recognition (CVPR)},
        year={2016},
    }

    @inproceedings{schoenberger2016mvs,
        author={Sch\"{o}nberger, Johannes Lutz and Zheng, Enliang and Pollefeys, Marc and Frahm, Jan-Michael},
        title={Pixelwise View Selection for Unstructured Multi-View Stereo},
        booktitle={European Conference on Computer Vision (ECCV)},
        year={2016},
    }

If you use the image retrieval / vocabulary tree engine, please also cite:

    @inproceedings{schoenberger2016vote,
        author={Sch\"{o}nberger, Johannes Lutz and Price, True and Sattler, Torsten and Frahm, Jan-Michael and Pollefeys, Marc},
        title={A Vote-and-Verify Strategy for Fast Spatial Verification in Image Retrieval},
        booktitle={Asian Conference on Computer Vision (ACCV)},
        year={2016},
    }

The latest source code is available at https://github.com/colmap/colmap. COLMAP
builds on top of existing works and when using specific algorithms within
COLMAP, please also cite the original authors, as specified in the source code.


Download
--------

Executables for Windows and Mac and other resources can be downloaded from
https://demuc.de/colmap/. Executables for Linux/Unix/BSD are available at
https://repology.org/metapackage/colmap/versions. To build COLMAP from source,
please see https://colmap.github.io/install.html.

Getting Started
---------------

1. Download the pre-built binaries from https://demuc.de/colmap/ or build the
   library manually as described in the documentation.
2. Download one of the provided datasets at https://demuc.de/colmap/datasets/
   or use your own images.
3. Use the **automatic reconstruction** to easily build models
   with a single click or command.

# Installation
Dependencies from the default Ubuntu repositories:
```bash
sudo apt-get install \
    git \
    cmake \
    ninja-build \
    build-essential \
    libboost-program-options-dev \
    libboost-filesystem-dev \
    libboost-graph-dev \
    libboost-system-dev \
    libeigen3-dev \
    libflann-dev \
    libfreeimage-dev \
    libmetis-dev \
    libgoogle-glog-dev \
    libgtest-dev \
    libsqlite3-dev \
    libglew-dev \
    qtbase5-dev \
    libqt5opengl5-dev \
    libcgal-dev \
    libceres-dev
```

To compile with `CUDA support`, install the following packages:
```bash
sudo apt-get install -y \
    nvidia-cuda-toolkit \
    nvidia-cuda-toolkit-gcc
```

Under Ubuntu 22.04, there is a problem when compiling with Ubuntu’s default CUDA package and GCC, and you must compile against GCC 10:

```bash
sudo apt-get install gcc-10 g++-10
export CC=/usr/bin/gcc-10
export CXX=/usr/bin/g++-10
export CUDAHOSTCXX=/usr/bin/g++-10
# ... and then run CMake against COLMAP's sources.
```

Configure and compile COLMAP:
```bash
git clone https://github.com/colmap/colmap.git
cd colmap
git checkout dev
mkdir build
cd build
cmake .. -GNinja -DCMAKE_CUDA_ARCHITECTURES=native
ninja
sudo ninja install
```

## Issues that may occur
While running cmake, you may encouter `Compilation error ptxas fatal : Value 'sm_30' is not defined for option 'gpu-name'`. In such the case, you can resolve by `sudo apt remove nvidia-cuda-toolkit`. This issue is due to the fact that you might have an old installation of nvidia-cuda-toolkit installed via apt-get (like me).

While  running `ninja` command, you might also get some errors like:
```bash
 -ldl && :
 /usr/bin/ld: /usr/lib/x86_64-linux-gnu/libfreeimage.so: undefined reference to `TIFFFieldTag@LIBTIFF_4.0'
 /usr/bin/ld: /usr/lib/x86_64-linux-gnu/libfreeimage.so: undefined reference to `TIFFFieldName@LIBTIFF_4.0'
 /usr/bin/ld: /usr/lib/x86_64-linux-gnu/libfreeimage.so: undefined reference to `TIFFFieldReadCount@LIBTIFF_4.0'
 /usr/bin/ld: /usr/lib/x86_64-linux-gnu/libfreeimage.so: undefined reference to `TIFFFieldPassCount@LIBTIFF_4.0'
 /usr/bin/ld: /usr/lib/x86_64-linux-gnu/libfreeimage.so: undefined reference to `TIFFFieldDataType@LIBTIFF_4.0'
 /usr/bin/ld: /usr/lib/x86_64-linux-gnu/libfreeimage.so: undefined reference to `_TIFFDataSize@LIBTIFF_4.0'
 /usr/bin/ld: /usr/lib/libceres.so.1.14.0: undefined reference to `google::kLogSiteUninitialized'
 collect2: error: ld returned 1 exit status
 ninja: build stopped: subcommand failed.
```

To resolve this problem, if you're using conda,  you can run `conda uninstall libtiff`

Documentation
-------------

The documentation is available at https://colmap.github.io/.


Support
-------

Please, use GitHub Discussions at https://github.com/colmap/colmap/discussions
for questions and the GitHub issue tracker at https://github.com/colmap/colmap
for bug reports, feature requests/additions, etc.


Acknowledgments
---------------

The library was originally written by Johannes L. Schönberger
(https://demuc.de/) with funding provided by his PhD advisors Jan-Michael Frahm
and Marc Pollefeys. Since then the project has benefited from countless
community contributions, including bug fixes, improvements, new features,
third-party tooling, and community support.


Contribution
------------

Contributions (bug reports, bug fixes, improvements, etc.) are very welcome and
should be submitted in the form of new issues and/or pull requests on GitHub.


License
-------

The COLMAP library is licensed under the new BSD license. Note that this text
refers only to the license for COLMAP itself, independent of its thirdparty
dependencies, which are separately licensed. Building COLMAP with these
dependencies may affect the resulting COLMAP license.

    Copyright (c) 2023, ETH Zurich and UNC Chapel Hill.
    All rights reserved.

    Redistribution and use in source and binary forms, with or without
    modification, are permitted provided that the following conditions are met:

        * Redistributions of source code must retain the above copyright
          notice, this list of conditions and the following disclaimer.

        * Redistributions in binary form must reproduce the above copyright
          notice, this list of conditions and the following disclaimer in the
          documentation and/or other materials provided with the distribution.

        * Neither the name of ETH Zurich and UNC Chapel Hill nor the names of
          its contributors may be used to endorse or promote products derived
          from this software without specific prior written permission.

    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
    AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
    IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
    ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR CONTRIBUTORS BE
    LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
    CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
    SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
    INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
    CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
    ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
    POSSIBILITY OF SUCH DAMAGE.

