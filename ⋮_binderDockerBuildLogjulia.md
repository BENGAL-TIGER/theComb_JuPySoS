Waiting for build to start...
Picked Git content provider.
Cloning into '/tmp/repo2dockerls8m3anc'...
HEAD is now at 1b7fbbb Update postBuild
Building conda environment for python=Using JuliaBuildPack builder
Building conda environment for python=Building conda environment for python=Step 1/46 : FROM buildpack-deps:bionic
 ---> 0b95c752ed47
Step 2/46 : ENV DEBIAN_FRONTEND=noninteractive
 ---> Using cache
 ---> 6900a0d98371
Step 3/46 : RUN apt-get update &&     apt-get install --yes --no-install-recommends locales &&     apt-get purge &&     apt-get clean &&     rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> b0301fa2a671
Step 4/46 : RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen &&     locale-gen
 ---> Using cache
 ---> fbfae3f315f4
Step 5/46 : ENV LC_ALL en_US.UTF-8
 ---> Using cache
 ---> 1cb99993389b
Step 6/46 : ENV LANG en_US.UTF-8
 ---> Using cache
 ---> e89d628971f7
Step 7/46 : ENV LANGUAGE en_US.UTF-8
 ---> Using cache
 ---> 8cda6dbbea5a
Step 8/46 : ENV SHELL /bin/bash
 ---> Using cache
 ---> 0ac8825a6715
Step 9/46 : ARG NB_USER
 ---> Using cache
 ---> ab49176325de
Step 10/46 : ARG NB_UID
 ---> Using cache
 ---> e22eeb721d95
Step 11/46 : ENV USER ${NB_USER}
 ---> Using cache
 ---> a4a87d58969a
Step 12/46 : ENV HOME /home/${NB_USER}
 ---> Using cache
 ---> 489e79986ae5
Step 13/46 : RUN adduser --disabled-password     --gecos "Default user"     --uid ${NB_UID}     ${NB_USER}
 ---> Using cache
 ---> ba281389dd2e
Step 14/46 : WORKDIR ${HOME}
 ---> Using cache
 ---> b3a82f0c94a3
Step 15/46 : RUN wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key |  apt-key add - &&     DISTRO="bionic" &&     echo "deb https://deb.nodesource.com/node_10.x $DISTRO main" >> /etc/apt/sources.list.d/nodesource.list &&     echo "deb-src https://deb.nodesource.com/node_10.x $DISTRO main" >> /etc/apt/sources.list.d/nodesource.list
 ---> Using cache
 ---> 98bc132d0044
Step 16/46 : RUN apt-get update &&     apt-get install --yes --no-install-recommends        less        nodejs        unzip        && apt-get purge &&     apt-get clean &&     rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> 55b2da2ac215
Step 17/46 : EXPOSE 8888
 ---> Using cache
 ---> 047f936d6a0e
Step 18/46 : ENV APP_BASE /srv
 ---> Using cache
 ---> 4420a49ecf89
Step 19/46 : ENV CONDA_DIR ${APP_BASE}/conda
 ---> Using cache
 ---> ecce48c48c40
Step 20/46 : ENV NB_PYTHON_PREFIX ${CONDA_DIR}
 ---> Using cache
 ---> 8b9e799aec49
Step 21/46 : ENV KERNEL_PYTHON_PREFIX ${NB_PYTHON_PREFIX}
 ---> Using cache
 ---> 2e977f3fdcb2
Step 22/46 : ENV JULIA_PATH ${APP_BASE}/julia
 ---> Using cache
 ---> abbcade494e2
Step 23/46 : ENV JULIA_HOME ${JULIA_PATH}/bin
 ---> Using cache
 ---> 522b86fcdfa1
Step 24/46 : ENV JULIA_BINDIR ${JULIA_HOME}
 ---> Using cache
 ---> f6ef157c817f
Step 25/46 : ENV JULIA_PKGDIR ${JULIA_PATH}/pkg
 ---> Using cache
 ---> 3877bab9e0a0
Step 26/46 : ENV JULIA_VERSION 0.6.4
 ---> Using cache
 ---> 8577f9b8e537
Step 27/46 : ENV JUPYTER ${NB_PYTHON_PREFIX}/bin/jupyter
 ---> Using cache
 ---> e45dfeeb4c4a
Step 28/46 : ENV PATH ${CONDA_DIR}/bin:$HOME/.local/bin:${JULIA_HOME}:${PATH}
 ---> Using cache
 ---> 1d4b03a783c9
Step 29/46 : COPY julia/install-repo-dependencies.jl /tmp/install-repo-dependencies.jl
 ---> Using cache
 ---> a5cc5355f90d
Step 30/46 : COPY conda/install-miniconda.bash /tmp/install-miniconda.bash
 ---> Using cache
 ---> e08cde0d630f
Step 31/46 : COPY conda/environment.frozen.yml /tmp/environment.yml
 ---> Using cache
 ---> d2a6e273b175
Step 32/46 : RUN bash /tmp/install-miniconda.bash && rm /tmp/install-miniconda.bash /tmp/environment.yml
 ---> Using cache
 ---> e7c5a5e2f59f
Step 33/46 : RUN mkdir -p ${JULIA_PATH} && curl -sSL "https://julialang-s3.julialang.org/bin/linux/x64/${JULIA_VERSION%[.-]*}/julia-${JULIA_VERSION}-linux-x86_64.tar.gz" | tar -xz -C ${JULIA_PATH} --strip-components 1
 ---> Using cache
 ---> 7205e4da2021
Step 34/46 : RUN mkdir -p ${JULIA_PKGDIR} && chown ${NB_USER}:${NB_USER} ${JULIA_PKGDIR}
 ---> Using cache
 ---> cd26b81c85c1
Step 35/46 : USER ${NB_USER}
 ---> Using cache
 ---> 41d6f0581174
Step 36/46 : RUN julia -e 'if (VERSION > v"0.7-") using Pkg; else Pkg.init(); end; Pkg.add("IJulia"); using IJulia;' && mv ${HOME}/.local/share/jupyter/kernels/julia-${JULIA_VERSION%[.-]*}  ${NB_PYTHON_PREFIX}/share/jupyter/kernels/julia-${JULIA_VERSION%[.-]*}
 ---> Using cache
 ---> edbc8909e7b8
Step 37/46 : USER root
 ---> Using cache
 ---> a429a125ea9b
Step 38/46 : COPY src/ ${HOME}
 ---> 3a12b8dbd650
Step 39/46 : RUN chown -R ${NB_USER}:${NB_USER} ${HOME}
 ---> Running in 8d518cf43e87
Removing intermediate container 8d518cf43e87
 ---> 5e2b5b74b9f4
Step 40/46 : USER ${NB_USER}
 ---> Running in 3258d27744e5
Removing intermediate container 3258d27744e5
 ---> 97b7b00a3c70
Step 41/46 : RUN conda env update -n root -f "environment.yml" && conda clean -tipsy && conda list -n root
 ---> Running in d912bbc1f2ca
Solving environment: ...working... done
ca-certificates-2018 | 143 KB    | ########## | 100%
pytz-2018.7          | 226 KB    | ########## | 100%
pyyaml-3.13          | 460 KB    | ########## | 100%
libtiff-4.0.10       | 523 KB    | ########## | 100%
blas-1.1             | 1 KB      | ########## | 100%
packaging-18.0       | 19 KB     | ########## | 100%
openssl-1.0.2p       | 3.1 MB    | ########## | 100%
libuuid-2.32.1       | 24 KB     | ########## | 100%
pcre-8.41            | 243 KB    | ########## | 100%
libxml2-2.9.8        | 1.8 MB    | ########## | 100%
dbus-1.13.0          | 560 KB    | ########## | 100%
kiwisolver-1.0.1     | 924 KB    | ########## | 100%
qt-5.6.2             | 44.3 MB   | ########## | 100%
gst-plugins-base-1.1 | 2.7 MB    | ########## | 100%
pthread-stubs-0.4    | 5 KB      | ########## | 100%
bokeh-1.0.2          | 5.3 MB    | ########## | 100%
icu-58.2             | 22.8 MB   | ########## | 100%
fontconfig-2.13.1    | 320 KB    | ########## | 100%
sip-4.18.1           | 266 KB    | ########## | 100%
pip-18.1             | 1.8 MB    | ########## | 100%
glib-2.56.2          | 4.6 MB    | ########## | 100%
gettext-0.19.8.1     | 3.5 MB    | ########## | 100%
cycler-0.10.0        | 8 KB      | ########## | 100%
xorg-libxau-1.0.8    | 12 KB     | ########## | 100%
expat-2.2.5          | 144 KB    | ########## | 100%
freetype-2.9.1       | 800 KB    | ########## | 100%
xorg-libxdmcp-1.1.2  | 17 KB     | ########## | 100%
gstreamer-1.12.5     | 2.1 MB    | ########## | 100%
libxcb-1.13          | 393 KB    | ########## | 100%
certifi-2018.11.29   | 145 KB    | ########## | 100%
libpng-1.6.36        | 276 KB    | ########## | 100%
numpy-1.15.1         | 9.3 MB    | ########## | 100%
openblas-0.2.20      | 17.0 MB   | ########## | 100%
olefile-0.46         | 31 KB     | ########## | 100%
pillow-5.3.0         | 1018 KB   | ########## | 100%
pyqt-5.6.0           | 5.4 MB    | ########## | 100%
pint-0.8.1           | 99 KB     | ########## | 100%
libiconv-1.15        | 2.0 MB    | ########## | 100%
pyparsing-2.3.0      | 53 KB     | ########## | 100%
matplotlib-2.2.3     | 9.2 MB    | ########## | 100%
appmode-0.4.0        | 13 KB     | ########## | 100%
jpeg-9c              | 229 KB    | ########## | 100%
libgfortran-3.0.0    | 281 KB    | ########## | 100%
Downloading and Extracting Packages
Preparing transaction: ...working... done
Verifying transaction: ...working... done
Executing transaction: ...working... done
Collecting julia (from -r /home/jovyan/condaenv.6unm889p.requirements.txt (line 1))
  Downloading https://files.pythonhosted.org/packages/ed/55/88c2ec067870114801689af0e9e8210107fb448a06ac9143d5ae03b01cb5/julia-0.2.0-py2.py3-none-any.whl (238kB)
Installing collected packages: julia
Successfully installed julia-0.2.0
#
# To activate this environment, use:
# > source activate root
#
# To deactivate an active environment, use:
# > source deactivate
#


Cache location: /srv/conda/pkgs
Will remove the following tarballs:

/srv/conda/pkgs
---------------
olefile-0.46-py_0.tar.bz2                     31 KB
certifi-2018.11.29-py36_1000.tar.bz2         145 KB
gst-plugins-base-1.12.5-hde13a9d_0.tar.bz2     2.7 MB
libxcb-1.13-h470a237_2.tar.bz2               393 KB
libxml2-2.9.8-h422b904_5.tar.bz2             1.8 MB
expat-2.2.5-hfc679d8_2.tar.bz2               144 KB
jpeg-9c-h470a237_1.tar.bz2                   229 KB
gettext-0.19.8.1-h5e8e0c9_1.tar.bz2          3.5 MB
kiwisolver-1.0.1-py36h2d50403_2.tar.bz2      924 KB
pthread-stubs-0.4-h470a237_1.tar.bz2           5 KB
appmode-0.4.0-py36_1001.tar.bz2               13 KB
freetype-2.9.1-h6debe1e_4.tar.bz2            800 KB
pillow-5.3.0-py36hc736899_0.tar.bz2         1018 KB
glib-2.56.2-h464dc38_1.tar.bz2               4.6 MB
qt-5.6.2-hf70d934_9.tar.bz2                 44.3 MB
libtiff-4.0.10-he6b73bb_0.tar.bz2            523 KB
ca-certificates-2018.11.29-ha4d7672_0.tar.bz2     143 KB
matplotlib-2.2.3-py36h8e2386c_0.tar.bz2      9.2 MB
pip-18.1-py36_1000.tar.bz2                   1.8 MB
xorg-libxau-1.0.8-h470a237_6.tar.bz2          12 KB
fontconfig-2.13.1-h65d0f4c_0.tar.bz2         320 KB
packaging-18.0-py_0.tar.bz2                   19 KB
numpy-1.15.1-py36_blas_openblashd3ea46f_0.tar.bz2     9.3 MB
pint-0.8.1-py_1.tar.bz2                       99 KB
libiconv-1.15-h470a237_3.tar.bz2             2.0 MB
pyyaml-3.13-py36h470a237_1.tar.bz2           460 KB
cycler-0.10.0-py_1.tar.bz2                     8 KB
pyqt-5.6.0-py36h8210e8a_7.tar.bz2            5.4 MB
dbus-1.13.0-h3a4f0e9_0.tar.bz2               560 KB
pcre-8.41-hfc679d8_3.tar.bz2                 243 KB
openssl-1.0.2p-h470a237_1.tar.bz2            3.1 MB
libpng-1.6.36-ha92aebf_0.tar.bz2             276 KB
libuuid-2.32.1-h470a237_2.tar.bz2             24 KB
pytz-2018.7-py_0.tar.bz2                     226 KB
sip-4.18.1-py36hfc679d8_0.tar.bz2            266 KB
xorg-libxdmcp-1.1.2-h470a237_7.tar.bz2        17 KB
openblas-0.2.20-8.tar.bz2                   17.0 MB
pyparsing-2.3.0-py_0.tar.bz2                  53 KB
libgfortran-3.0.0-1.tar.bz2                  281 KB
bokeh-1.0.2-py36_1000.tar.bz2                5.3 MB
blas-1.1-openblas.tar.bz2                      1 KB
gstreamer-1.12.5-h5856ed1_0.tar.bz2          2.1 MB
icu-58.2-hfc679d8_0.tar.bz2                 22.8 MB

---------------------------------------------------
Total:                                     142.1 MB

Removed olefile-0.46-py_0.tar.bz2
Removed certifi-2018.11.29-py36_1000.tar.bz2
Removed gst-plugins-base-1.12.5-hde13a9d_0.tar.bz2
Removed libxcb-1.13-h470a237_2.tar.bz2
Removed libxml2-2.9.8-h422b904_5.tar.bz2
Removed expat-2.2.5-hfc679d8_2.tar.bz2
Removed jpeg-9c-h470a237_1.tar.bz2
Removed gettext-0.19.8.1-h5e8e0c9_1.tar.bz2
Removed kiwisolver-1.0.1-py36h2d50403_2.tar.bz2
Removed pthread-stubs-0.4-h470a237_1.tar.bz2
Removed appmode-0.4.0-py36_1001.tar.bz2
Removed freetype-2.9.1-h6debe1e_4.tar.bz2
Removed pillow-5.3.0-py36hc736899_0.tar.bz2
Removed glib-2.56.2-h464dc38_1.tar.bz2
Removed qt-5.6.2-hf70d934_9.tar.bz2
Removed libtiff-4.0.10-he6b73bb_0.tar.bz2
Removed ca-certificates-2018.11.29-ha4d7672_0.tar.bz2
Removed matplotlib-2.2.3-py36h8e2386c_0.tar.bz2
Removed pip-18.1-py36_1000.tar.bz2
Removed xorg-libxau-1.0.8-h470a237_6.tar.bz2
Removed fontconfig-2.13.1-h65d0f4c_0.tar.bz2
Removed packaging-18.0-py_0.tar.bz2
Removed numpy-1.15.1-py36_blas_openblashd3ea46f_0.tar.bz2
Removed pint-0.8.1-py_1.tar.bz2
Removed libiconv-1.15-h470a237_3.tar.bz2
Removed pyyaml-3.13-py36h470a237_1.tar.bz2
Removed cycler-0.10.0-py_1.tar.bz2
Removed pyqt-5.6.0-py36h8210e8a_7.tar.bz2
Removed dbus-1.13.0-h3a4f0e9_0.tar.bz2
Removed pcre-8.41-hfc679d8_3.tar.bz2
Removed openssl-1.0.2p-h470a237_1.tar.bz2
Removed libpng-1.6.36-ha92aebf_0.tar.bz2
Removed libuuid-2.32.1-h470a237_2.tar.bz2
Removed pytz-2018.7-py_0.tar.bz2
Removed sip-4.18.1-py36hfc679d8_0.tar.bz2
Removed xorg-libxdmcp-1.1.2-h470a237_7.tar.bz2
Removed openblas-0.2.20-8.tar.bz2
Removed pyparsing-2.3.0-py_0.tar.bz2
Removed libgfortran-3.0.0-1.tar.bz2
Removed bokeh-1.0.2-py36_1000.tar.bz2
Removed blas-1.1-openblas.tar.bz2
Removed gstreamer-1.12.5-h5856ed1_0.tar.bz2
Removed icu-58.2-hfc679d8_0.tar.bz2
Cache location: /srv/conda/pkgs
Will remove the following packages:
/srv/conda/pkgs
---------------

blas-1.1-openblas                              3 KB
pthread-stubs-0.4-h470a237_1                  11 KB

---------------------------------------------------
Total:                                        14 KB

removing blas-1.1-openblas
removing pthread-stubs-0.4-h470a237_1
source cache (/srv/conda/conda-bld/src_cache)
Size:                                           0 B

git cache (/srv/conda/conda-bld/git_cache)
Size:                                           0 B

hg cache (/srv/conda/conda-bld/hg_cache)
Size:                                           0 B

svn cache (/srv/conda/conda-bld/svn_cache)
Size:                                           0 B

Total:                                          0 B
Removing /srv/conda/conda-bld/src_cache
Removing /srv/conda/conda-bld/git_cache
Removing /srv/conda/conda-bld/hg_cache
Removing /srv/conda/conda-bld/svn_cache
# packages in environment at /srv/conda:
#
# Name                    Version                   Build  Channel
appmode                   0.4.0                 py36_1001    conda-forge
asn1crypto                0.24.0                py36_1003    conda-forge
backcall                  0.1.0                      py_0    conda-forge
blas                      1.1                    openblas    conda-forge
bleach                    2.1.4                      py_1    conda-forge
bokeh                     1.0.2                 py36_1000    conda-forge
bzip2                     1.0.6                h470a237_2    conda-forge
ca-certificates           2018.11.29           ha4d7672_0    conda-forge
certifi                   2018.11.29            py36_1000    conda-forge
cffi                      1.11.5           py36h5e8e0c9_1    conda-forge
chardet                   3.0.4                 py36_1003    conda-forge
conda                     4.5.11                py36_1000    conda-forge
conda-env                 2.6.0                         1    defaults
cryptography              2.3.1            py36hdffb7b8_0    conda-forge
cryptography-vectors      2.3.1                 py36_1000    conda-forge
cycler                    0.10.0                     py_1    conda-forge
dbus                      1.13.0               h3a4f0e9_0    conda-forge
decorator                 4.3.0                      py_0    conda-forge
defusedxml                0.5.0                    py36_0    conda-forge
entrypoints               0.2.3                    py36_2    conda-forge
expat                     2.2.5                hfc679d8_2    conda-forge
fontconfig                2.13.1               h65d0f4c_0    conda-forge
freetype                  2.9.1                h6debe1e_4    conda-forge
gettext                   0.19.8.1             h5e8e0c9_1    conda-forge
glib                      2.56.2               h464dc38_1    conda-forge
gmp                       6.1.2                hfc679d8_0    conda-forge
gst-plugins-base          1.12.5               hde13a9d_0    conda-forge
gstreamer                 1.12.5               h5856ed1_0    conda-forge
html5lib                  1.0.1                      py_0    conda-forge
icu                       58.2                 hfc679d8_0    conda-forge
idna                      2.7                   py36_1002    conda-forge
ipykernel                 4.9.0                    py36_0    conda-forge
ipython                   6.5.0                    py36_0    conda-forge
ipython_genutils          0.2.0                      py_1    conda-forge
ipywidgets                7.2.1                    py36_1    conda-forge
jedi                      0.12.1                   py36_0    conda-forge
jinja2                    2.10                       py_1    conda-forge
jpeg                      9c                   h470a237_1    conda-forge
jsonschema                2.6.0                    py36_2    conda-forge
julia                     0.2.0                     <pip>
jupyter_client            5.2.3                      py_1    conda-forge
jupyter_core              4.4.0                      py_0    conda-forge
jupyterlab                0.34.9                   py36_0    conda-forge
jupyterlab_launcher       0.13.1                     py_2    conda-forge
kiwisolver                1.0.1            py36h2d50403_2    conda-forge
libedit                   3.1.20170329         h6b74fdf_2    defaults
libffi                    3.2.1                hfc679d8_5    conda-forge
libgcc-ng                 7.2.0                hdf63c60_3    conda-forge
libgfortran               3.0.0                         1    conda-forge
libiconv                  1.15                 h470a237_3    conda-forge
libpng                    1.6.36               ha92aebf_0    conda-forge
libsodium                 1.0.16               h470a237_1    conda-forge
libstdcxx-ng              7.2.0                hdf63c60_3    conda-forge
libtiff                   4.0.10               he6b73bb_0    conda-forge
libuuid                   2.32.1               h470a237_2    conda-forge
libxcb                    1.13                 h470a237_2    conda-forge
libxml2                   2.9.8                h422b904_5    conda-forge
markupsafe                1.0              py36h470a237_1    conda-forge
matplotlib                2.2.3            py36h8e2386c_0    conda-forge
mistune                   0.8.3            py36h470a237_2    conda-forge
nbconvert                 5.4.0                         1    conda-forge
nbformat                  4.4.0                      py_1    conda-forge
ncurses                   6.1                  hfc679d8_1    conda-forge
notebook                  5.6.0                    py36_1    conda-forge
nteract-on-jupyter        1.9.6                     <pip>
numpy                     1.15.1          py36_blas_openblashd3ea46f_0    conda-forge
olefile                   0.46                       py_0    conda-forge
openblas                  0.2.20                        8    conda-forge
openssl                   1.0.2p               h470a237_1    conda-forge
packaging                 18.0                       py_0    conda-forge
pandoc                    1.19.2                        0    conda-forge
pandocfilters             1.4.2                      py_1    conda-forge
parso                     0.3.1                      py_0    conda-forge
pcre                      8.41                 hfc679d8_3    conda-forge
pexpect                   4.6.0                    py36_0    conda-forge
pickleshare               0.7.4                    py36_0    conda-forge
pillow                    5.3.0            py36hc736899_0    conda-forge
pint                      0.8.1                      py_1    conda-forge
pip                       18.1                  py36_1000    conda-forge
prometheus_client         0.3.1                      py_1    conda-forge
prompt_toolkit            1.0.15                     py_1    conda-forge
pthread-stubs             0.4                  h470a237_1    conda-forge
ptyprocess                0.6.0                    py36_0    conda-forge
pycosat                   0.6.3            py36h470a237_1    conda-forge
pycparser                 2.19                       py_0    conda-forge
pygments                  2.2.0                      py_1    conda-forge
pyopenssl                 18.0.0                py36_1000    conda-forge
pyparsing                 2.3.0                      py_0    conda-forge
pyqt                      5.6.0            py36h8210e8a_7    conda-forge
pysocks                   1.6.8                 py36_1002    conda-forge
python                    3.6.6                h5001a0f_0    conda-forge
python-dateutil           2.7.3                      py_0    conda-forge
pytz                      2018.7                     py_0    conda-forge
pyyaml                    3.13             py36h470a237_1    conda-forge
pyzmq                     17.1.2           py36hae99301_0    conda-forge
qt                        5.6.2                hf70d934_9    conda-forge
readline                  7.0                  haf1bffa_1    conda-forge
requests                  2.20.1                py36_1000    conda-forge
ruamel_yaml               0.15.71          py36h470a237_0    conda-forge
send2trash                1.5.0                      py_0    conda-forge
setuptools                40.2.0                   py36_0    conda-forge
simplegeneric             0.8.1                      py_1    conda-forge
sip                       4.18.1           py36hfc679d8_0    conda-forge
six                       1.11.0                   py36_1    conda-forge
sqlite                    3.24.0               h2f33b56_1    conda-forge
terminado                 0.8.1                    py36_1    conda-forge
testpath                  0.3.1                    py36_1    conda-forge
tk                        8.6.8                         0    conda-forge
tornado                   4.5.3                    py36_0    conda-forge
traitlets                 4.3.2                    py36_0    conda-forge
urllib3                   1.23                  py36_1001    conda-forge
wcwidth                   0.1.7                      py_1    conda-forge
webencodings              0.5.1                      py_1    conda-forge
wheel                     0.31.1                   py36_1    conda-forge
widgetsnbextension        3.2.1                    py36_1    conda-forge
xorg-libxau               1.0.8                h470a237_6    conda-forge
xorg-libxdmcp             1.1.2                h470a237_7    conda-forge
xz                        5.2.4                h470a237_1    conda-forge
yaml                      0.1.7                had09818_2    defaults
zeromq                    4.2.5                hfc679d8_5    conda-forge
zlib                      1.2.11               h470a237_3    conda-forge
Removing intermediate container d912bbc1f2ca
 ---> 65607fc01971
Step 42/46 : RUN julia /tmp/install-repo-dependencies.jl "REQUIRE"
 ---> Running in 0820959d1867
INFO: Cloning cache of AxisAlgorithms from https://github.com/timholy/AxisAlgorithms.jl.git
INFO: Cloning cache of BinDeps from https://github.com/JuliaPackaging/BinDeps.jl.git
INFO: Cloning cache of Calculus from https://github.com/JuliaMath/Calculus.jl.git
INFO: Cloning cache of CategoricalArrays from https://github.com/JuliaData/CategoricalArrays.jl.git
INFO: Cloning cache of CodecZlib from https://github.com/bicycle1885/CodecZlib.jl.git
INFO: Cloning cache of ColorTypes from https://github.com/JuliaGraphics/ColorTypes.jl.git
INFO: Cloning cache of Colors from https://github.com/JuliaGraphics/Colors.jl.git
INFO: Cloning cache of CommonSubexpressions from https://github.com/rdeits/CommonSubexpressions.jl.git
INFO: Cloning cache of Compose from https://github.com/GiovineItalia/Compose.jl.git
INFO: Cloning cache of Contour from https://github.com/JuliaGeometry/Contour.jl.git
INFO: Cloning cache of CoupledFields from https://github.com/Mattriks/CoupledFields.jl.git
INFO: Cloning cache of DataArrays from https://github.com/JuliaStats/DataArrays.jl.git
INFO: Cloning cache of DataFrames from https://github.com/JuliaData/DataFrames.jl.git
INFO: Cloning cache of DataStreams from https://github.com/JuliaData/DataStreams.jl.git
INFO: Cloning cache of DataStructures from https://github.com/JuliaCollections/DataStructures.jl.git
INFO: Cloning cache of DiffEqDiffTools from https://github.com/JuliaDiffEq/DiffEqDiffTools.jl.git
INFO: Cloning cache of DiffResults from https://github.com/JuliaDiff/DiffResults.jl.git
INFO: Cloning cache of DiffRules from https://github.com/JuliaDiff/DiffRules.jl.git
INFO: Cloning cache of Distances from https://github.com/JuliaStats/Distances.jl.git
INFO: Cloning cache of Distributions from https://github.com/JuliaStats/Distributions.jl.git
INFO: Cloning cache of DocStringExtensions from https://github.com/JuliaDocs/DocStringExtensions.jl.git
INFO: Cloning cache of FixedPointNumbers from https://github.com/JuliaMath/FixedPointNumbers.jl.git
INFO: Cloning cache of ForwardDiff from https://github.com/JuliaDiff/ForwardDiff.jl.git
INFO: Cloning cache of GR from https://github.com/jheinen/GR.jl.git
INFO: Cloning cache of Gadfly from https://github.com/GiovineItalia/Gadfly.jl.git
INFO: Cloning cache of Hexagons from https://github.com/GiovineItalia/Hexagons.jl.git
INFO: Cloning cache of IndirectArrays from https://github.com/JuliaArrays/IndirectArrays.jl.git
INFO: Cloning cache of Interpolations from https://github.com/JuliaMath/Interpolations.jl.git
INFO: Cloning cache of IterTools from https://github.com/JuliaCollections/IterTools.jl.git
INFO: Cloning cache of Juno from https://github.com/JunoLab/Juno.jl.git
INFO: Cloning cache of KernelDensity from https://github.com/JuliaStats/KernelDensity.jl.git
INFO: Cloning cache of LaTeXStrings from https://github.com/stevengj/LaTeXStrings.jl.git
INFO: Cloning cache of LineSearches from https://github.com/JuliaNLSolvers/LineSearches.jl.git
INFO: Cloning cache of Loess from https://github.com/JuliaStats/Loess.jl.git
INFO: Cloning cache of MacroTools from https://github.com/MikeInnes/MacroTools.jl.git
INFO: Cloning cache of Measures from https://github.com/JuliaGraphics/Measures.jl.git
INFO: Cloning cache of Media from https://github.com/JunoLab/Media.jl.git
INFO: Cloning cache of Missings from https://github.com/JuliaData/Missings.jl.git
INFO: Cloning cache of NLSolversBase from https://github.com/JuliaNLSolvers/NLSolversBase.jl.git
INFO: Cloning cache of NaNMath from https://github.com/mlubin/NaNMath.jl.git
INFO: Cloning cache of NamedTuples from https://github.com/JuliaData/NamedTuples.jl.git
INFO: Cloning cache of OffsetArrays from https://github.com/JuliaArrays/OffsetArrays.jl.git
INFO: Cloning cache of Optim from https://github.com/JuliaNLSolvers/Optim.jl.git
INFO: Cloning cache of PDMats from https://github.com/JuliaStats/PDMats.jl.git
INFO: Cloning cache of Parameters from https://github.com/mauro3/Parameters.jl.git
INFO: Cloning cache of PlotThemes from https://github.com/JuliaPlots/PlotThemes.jl.git
INFO: Cloning cache of PlotUtils from https://github.com/JuliaPlots/PlotUtils.jl.git
INFO: Cloning cache of Plots from https://github.com/JuliaPlots/Plots.jl.git
INFO: Cloning cache of PositiveFactorizations from https://github.com/timholy/PositiveFactorizations.jl.git
INFO: Cloning cache of PyCall from https://github.com/JuliaPy/PyCall.jl.git
INFO: Cloning cache of PyPlot from https://github.com/JuliaPy/PyPlot.jl.git
INFO: Cloning cache of QuadGK from https://github.com/JuliaMath/QuadGK.jl.git
INFO: Cloning cache of Ratios from https://github.com/timholy/Ratios.jl.git
INFO: Cloning cache of RecipesBase from https://github.com/JuliaPlots/RecipesBase.jl.git
INFO: Cloning cache of Reexport from https://github.com/simonster/Reexport.jl.git
INFO: Cloning cache of Requires from https://github.com/MikeInnes/Requires.jl.git
INFO: Cloning cache of Rmath from https://github.com/JuliaStats/Rmath.jl.git
INFO: Cloning cache of ShowItLikeYouBuildIt from https://github.com/JuliaArrays/ShowItLikeYouBuildIt.jl.git
INFO: Cloning cache of Showoff from https://github.com/JuliaGraphics/Showoff.jl.git
INFO: Cloning cache of SortingAlgorithms from https://github.com/JuliaCollections/SortingAlgorithms.jl.git
INFO: Cloning cache of SpecialFunctions from https://github.com/JuliaMath/SpecialFunctions.jl.git
INFO: Cloning cache of StaticArrays from https://github.com/JuliaArrays/StaticArrays.jl.git
INFO: Cloning cache of StatsBase from https://github.com/JuliaStats/StatsBase.jl.git
INFO: Cloning cache of StatsFuns from https://github.com/JuliaStats/StatsFuns.jl.git
INFO: Cloning cache of TranscodingStreams from https://github.com/bicycle1885/TranscodingStreams.jl.git
INFO: Cloning cache of URIParser from https://github.com/JuliaWeb/URIParser.jl.git
INFO: Cloning cache of Unitful from https://github.com/ajkeller34/Unitful.jl.git
INFO: Cloning cache of WeakRefStrings from https://github.com/JuliaData/WeakRefStrings.jl.git
INFO: Cloning cache of WoodburyMatrices from https://github.com/timholy/WoodburyMatrices.jl.git
INFO: Installing AxisAlgorithms v0.3.0
INFO: Installing BinDeps v0.8.10
INFO: Installing Calculus v0.4.1
INFO: Installing CategoricalArrays v0.3.13
INFO: Installing CodecZlib v0.4.4
INFO: Installing ColorTypes v0.6.7
INFO: Installing Colors v0.8.2
INFO: Installing CommonSubexpressions v0.1.0
INFO: Installing Compose v0.6.1
INFO: Installing Contour v0.4.0
INFO: Installing CoupledFields v0.1.0
INFO: Installing DataArrays v0.7.0
INFO: Installing DataFrames v0.11.7
INFO: Installing DataStreams v0.3.8
INFO: Installing DataStructures v0.8.4
INFO: Installing DiffEqDiffTools v0.4.1
INFO: Installing DiffResults v0.0.3
INFO: Installing DiffRules v0.0.7
INFO: Installing Distances v0.6.0
INFO: Installing Distributions v0.15.0
INFO: Installing DocStringExtensions v0.4.6
INFO: Installing FixedPointNumbers v0.4.6
INFO: Installing ForwardDiff v0.7.5
INFO: Installing GR v0.36.0
INFO: Installing Gadfly v0.8.0
INFO: Installing Hexagons v0.1.0
INFO: Installing IndirectArrays v0.4.2
INFO: Installing Interpolations v0.8.0
INFO: Installing IterTools v0.2.1
INFO: Installing Juno v0.4.1
INFO: Installing KernelDensity v0.4.1
INFO: Installing LaTeXStrings v1.0.3
INFO: Installing LineSearches v6.0.2
INFO: Installing Loess v0.3.0
INFO: Installing MacroTools v0.4.4
INFO: Installing Measures v0.2.0
INFO: Installing Media v0.3.0
INFO: Installing Missings v0.2.10
INFO: Installing NLSolversBase v6.1.1
INFO: Installing NaNMath v0.3.2
INFO: Installing NamedTuples v4.0.2
INFO: Installing OffsetArrays v0.6.0
INFO: Installing Optim v0.15.3
INFO: Installing PDMats v0.8.0
INFO: Installing Parameters v0.9.2
INFO: Installing PlotThemes v0.2.0
INFO: Installing PlotUtils v0.4.4
INFO: Installing Plots v0.17.4
INFO: Installing PositiveFactorizations v0.1.0
INFO: Installing PyCall v1.18.5
INFO: Installing PyPlot v2.6.3
INFO: Installing QuadGK v0.3.0
INFO: Installing Ratios v0.3.0
INFO: Installing RecipesBase v0.3.1
INFO: Installing Reexport v0.1.0
INFO: Installing Requires v0.4.4
INFO: Installing Rmath v0.4.0
INFO: Installing ShowItLikeYouBuildIt v0.2.0
INFO: Installing Showoff v0.2.1
INFO: Installing SortingAlgorithms v0.2.1
INFO: Installing SpecialFunctions v0.6.0
INFO: Installing StaticArrays v0.7.2
INFO: Installing StatsBase v0.23.1
INFO: Installing StatsFuns v0.6.1
INFO: Installing TranscodingStreams v0.5.4
INFO: Installing URIParser v0.3.1
INFO: Installing Unitful v0.8.0
INFO: Installing WeakRefStrings v0.4.7
INFO: Installing WoodburyMatrices v0.3.0
INFO: Building CodecZlib
Info: Downloading https://github.com/bicycle1885/ZlibBuilder/releases/download/v1.0.2/Zlib.v1.2.11.x86_64-linux-gnu.tar.gz to /srv/julia/pkg/v0.6/CodecZlib/deps/usr/downloads/Zlib.v1.2.11.x86_64-linux-gnu.tar.gz...
[05:01:03] ######################################################################## 100.0%
INFO: Building SpecialFunctions
INFO: Building Rmath
Info: Downloading https://github.com/staticfloat/RmathBuilder/releases/download/v0.2.0-1/libRmath.x86_64-linux-gnu.tar.gz to /srv/julia/pkg/v0.6/Rmath/deps/usr/downloads/libRmath.x86_64-linux-gnu.tar.gz...
[05:01:11] ######################################################################## 100.0%
INFO: Building GR
INFO: Downloading pre-compiled GR 0.36.0 Ubuntu binary
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 59.8M  100 59.8M    0     0   9.8M      0  0:00:06  0:00:06 --:--:-- 13.1M
INFO: Building Plots
INFO: Cannot find deps/plotly-latest.min.js... downloading latest version.
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 2805k  100 2805k    0     0  12.5M      0 --:--:-- --:--:-- --:--:-- 12.5M
INFO: Building Conda
INFO: Building PyCall
Info: PyCall is using python3 (Python 3.6.6) at /srv/conda/bin/python3, libpython = /srv/conda/lib/libpython3.6m.so.1.0
Info: /srv/julia/pkg/v0.6/PyCall/deps/deps.jl has been updated
Info: /srv/julia/pkg/v0.6/PyCall/deps/PYTHON has been updated
Warning: No working GUI backend found for matplotlib
WARNING: Error requiring Juno from Plots:
ArgumentError: Module Hiccup not found in current path.
Run `Pkg.add("Hiccup")` to install the Hiccup package.
Stacktrace:
 [1] _require(::Symbol) at ./loading.jl:435
 [2] require(::Symbol) at ./loading.jl:405
 [3] err(::Plots.##703#710, ::Module, ::String) at /srv/julia/pkg/v0.6/Requires/src/require.jl:44
 [4] withpath(::Plots.##702#709, ::String) at /srv/julia/pkg/v0.6/Requires/src/require.jl:34
 [5] (::Plots.##701#708)() at /srv/julia/pkg/v0.6/Requires/src/require.jl:56
 [6] _collect(::Array{Function,1}, ::Base.Generator{Array{Function,1},Requires.##3#4}, ::Base.EltypeUnknown, ::Base.HasShape) at ./array.jl:483
 [7] loadmod(::Symbol) at /srv/julia/pkg/v0.6/Requires/src/require.jl:22
 [8] require(::Symbol) at ./loading.jl:408
 [9] _include_from_serialized(::String) at ./loading.jl:157
 [10] _require_from_serialized(::Int64, ::Symbol, ::String, ::Bool) at ./loading.jl:200
 [11] _require(::Symbol) at ./loading.jl:498
 [12] require(::Symbol) at ./loading.jl:405
 [13] eval(::Module, ::Any) at ./boot.jl:235
 [14] macro expansion at /tmp/install-repo-dependencies.jl:34 [inlined]
 [15] anonymous at ./<missing>:?
 [16] include_from_node1(::String) at ./loading.jl:576
 [17] include(::String) at ./sysimg.jl:14
 [18] process_options(::Base.JLOptions) at ./client.jl:305
 [19] _start() at ./client.jl:371
Removing intermediate container 0820959d1867
 ---> 7caea38921e5
Step 43/46 : USER ${NB_USER}
 ---> Running in 79bb37c2033d
Removing intermediate container 79bb37c2033d
 ---> 2f557a6712ee
Step 44/46 : RUN chmod +x postBuild
 ---> Running in e6b3ab7fe7c6
Removing intermediate container e6b3ab7fe7c6
 ---> 4e825f23ed55
Step 45/46 : RUN ./postBuild
 ---> Running in 8d18b8a97336
./postBuild: 1: ./postBuild: Syntax error: "(" unexpected
Removing intermediate container 8d18b8a97336
The command '/bin/sh -c ./postBuild' returned a non-zero code: 2
