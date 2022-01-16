# Regularized-Greedy-Forest-in-R

The details of the codeset and plots are included in the attached Microsoft Word Document (.docx) file in this repository. 
You need to view the file in "Read Mode" to see the contents properly after downloading the same.

RGF Package - A Brief Introduction
===================================

The RGF package is a wrapper of the Regularized Greedy Forest (RGF) python package, which also includes a Multi-core implementation (FastRGF). A Singularity image file is available in case that someone intends to run RGF on Ubuntu Linux (locally or in a cloud instance) with all package requirements pre-installed. This allows the user to utilize the RGF package without having to spend time on the installation process.

System Requirements
===================

    Python (>= 3.6)


All modules should be installed in the default python configuration (the configuration that the R-session displays as default), otherwise errors will occur during the RGF package installation (reticulate::py_discover_config() might be useful here).

    Debian/Ubuntu/Fedora
    =====================
    First install / upgrade the dependencies,

    sudo pip install --upgrade pip setuptools

    sudo pip install -U numpy

    sudo pip install --upgrade scipy

    sudo pip install -U scikit-learn


    Mac OS X
    ============
    Upgrade python to version 3 using,

    brew upgrade python


    Then install the dependencies for RGF and FastRGF

    sudo pip3 install --upgrade setuptools

    sudo pip3 install -U numpy

    sudo pip3 install --upgrade scipy

    sudo pip3 install -U scikit-learn


    The FastRGF module requires a gcc >= 8.0. To install gcc-8 (or the most recent gcc) with brew follow the next steps,

# before running the following commands make sure that the most recent Apple command line tools for Xcode are installed

    brew update

    brew upgrade

    brew info gcc

    brew install gcc

    brew cleanup

After the newest gcc version is installed the user should navigate to /usr/local/bin and if a gcc file exists (symbolic link) then the user should delete it. Then the user should run the following command,

    sudo ln -s /usr/local/bin/gcc-8 /usr/local/bin/gcc


The user should then verify that the gcc has been updated using

    gcc -v

    which gcc


After the new gcc is installed the user should continue with the installation of rgf_python,

    git clone https://github.com/RGF-team/rgf.git

    cd /rgf/RGF/build

    export CXX=/usr/local/bin/g++-8 && export CC=/usr/local/bin/gcc-8

    cmake /rgf/RGF /rgf/FastRGF

    make

    sudo make install

    cd /rgf/python-package

    sudo python3 setup.py install


After a successful rgf-python installation the user should open an R session and give the following reticulate command to change to the relevant (brew-python) directory (otherwise the RGF package won't work properly),

    reticulate::use_python('/usr/local/bin/python3')

and then,

    reticulate::py_discover_config()


To validate that a user is in the python version where RGF or FastRGF are installed. Then,

    install.packages(RGF)


    library(RGF)


to load the R package. It is possible that the following warning in the R session appears if FastRGF is not installed,

      UserWarning: Cannot find FastRGF executable files. FastRGF estimators will be unavailable for usage.
      warnings.warn("Cannot find FastRGF executable files. FastRGF estimators will be unavailable for usage.")
  
Windows OS

    NOTE : CURRENTLY THE PACKAGE ON WINDOWS CAN BE USED ONLY FROM THE COMMAND LINE (cmd)

    First download of get-pip.py for windows

    Update the Environment variables ( Control Panel >> System and Security >> System >> Advanced system settings >> Environment variables >> System variables >> Path >> Edit ) by adding ( for instance in case of python 3 ),

    C:\Python36;C:\Python36\Scripts


    Install the Build Tools for Visual Studio

    Open the Command prompt (console) and install the rgf_python dependencies,

    pip3 install --upgrade setuptools

    pip3 install -U numpy

    pip3 install --upgrade scipy

    pip3 install -U scikit-learn


    Then download git for windows,

    https://git-scm.com/download/win


    and run the downloaded .exe file. Then do,

    git clone https://github.com/RGF-team/rgf.git


    FastRGF requires a gcc version > 5.0 . To find out the gcc version, open a command prompt (console) and type,

    gcc --version


Installation / Upgrade of MinGW
===============================
Perform the following steps to upgrade the MinGW (so that simple RGF functions work – but not FastRGF)

Normally MinGW is installed in the C:\ directory. So, first delete the folder C:\MinGW (if it already exists), and then remove the environment variable from (Control Panel >> System and Security >> System >> Advanced system settings >> Environment variables >> System variables >> Path >> Edit) which usually is C:\MinGW\bin. Then download the most recent version of MinGW, and especially the mingw-get-setup.exe which is an automated GUI installer assistant. After the new version is installed successfully, update the environment variable by adding C:\MinGW\bin in (Control Panel >> System and Security >> System >> Advanced system settings >> Environment variables >> System variables >> Path >> Edit). Then open a new command prompt (console) and type,

        gcc --version


to find out if the new version of MinGW is installed properly.

A word of caution, If Rtools is already installed then make sure that it does not point to an older version of gcc. Just observe the Path field of the environment variables (accessible as explained previously).Perform the following steps only in case that a FastRGF installation is desired and gcc version is < 5.0

FastRGF works only with MinGW-w64 because only this version provides POSIX threads. It can be downloaded from the project's official SourceForge page. After a successful download and installation the user should also update the environment variables field in (Control Panel >> System and Security >> System >> Advanced system settings >> Environment variables >> System variables >> Path >> Edit) by adding the following path (assuming the software is installed in C:\Program Files (x86) folder),

    C:\Program Files (x86)\mingw-w64\i686-7.2.0-posix-dwarf-rt_v5-rev1\mingw32\bin


Installation of cmake
=====================
First download cmake for Windows, win64-x64 Installer. Once the file is downloaded run the .exe file and during installation make sure to add CMake to the system PATH for all users.

Before the installation of rgf I might have to remove Rtools environment variables, such as C:\Rtools\bin (accessible as explained previously), otherwise errors might occur.

Installation of RGF, FastRGF and rgf_python [ assuming the installation takes place in the c:/ directory ]

Open a console with administrator privileges (right click on cmd and run as administrator), then

# download the most recent version of rgf-python from the GitHub repository 
#--------------------------------------------------------------------------

    git clone http://github.com/RGF-team/rgf.git



# then navigate to 
#-----------------

    cd /rgf/RGF/

    mkdir bin

    cd c:/


# then download the latest "rgf.exe" from https://github.com/RGF-team/rgf/releases and place the "rgf.exe" inside the previously created "bin" folder ( /rgf/RGF/bin )



# installation of RGF
#--------------------

    cd /rgf/RGF/build

    mingw32-make

    cd c:/



# installation of FastRGF
#------------------------

    cd /rgf/FastRGF/

    mkdir build

    cd build


# BEFORE PROCEEDING WITH cmake MAKE SURE THAT THE "Rtools" folder IS NOT IN THE SAME DIRECTORY (IF THAT IS THE CASE THEN REMOVE IT TEMPORARILY, i.e. copy-paste the "Rtools" folder somewhere else)


    cmake .. -G "MinGW Makefiles"

    mingw32-make

    mingw32-make install

    cd c:/


# IF APPLICABLE, PASTE THE "Rtools" FOLDER IN THE INITIAL LOCATION / DIRECTORY


# installation of rgf-python
#---------------------------

    cd rgf/python-package

    python setup.py install


Then open a command prompt (console) and type,

    python 


To launch Python and then type

    import rgf

    exit()


To observe if rgf is installed properly. Then continue with the installation of the RGF package,

        install.packages(RGF)


On windows the user can take advantage of the RGF package currently only from within the command prompt (console). First, find the full path of the installation location of R (possible if someone right-clicks in the R short-cut (probably on Desktop) and navigates to properties >> shortcut >> target). In case, for instance, that R is located in C:\Program Files\R\R-3.4.0\bin\x64\R, then, by opening a command prompt (console) and giving,

    cd C:\Program Files\R\R-3.4.0\bin\x64\

    R

    library(RGF)


one can proceed with the usage of the RGF package.

Installation of the RGF package

To install the package from CRAN use,

        install.packages('RGF')

