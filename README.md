# ROS 2.0 installation guide for Windows

Note from the author: yes Windows, be prepared for the fun

## Supported compilers

At this moment, compilation has been tested on Windows 8 and is supported 
when using Visual Studio 2013. Patches for other versions are welcome.

### Note on enabling 64bits compilation

MSVC will compile for 32bits if no other configuration is passed when enable it
(running vcarsall.bat) or when running cmake. 64bits compilation can be enabled
passing amd64 parameter to vcvarsall.bat (vcvarsall.bat amd64). Looks like some
versions of MSVC Express edition don't have this 64 bits support.

## Install dependencies

 - [Visual Studio 2013](http://www.microsoft.com/en-us/download/details.aspx?id=34673).
    - Use wexpressfull.exe and follow installer.

 - [Python 3.4.1](https://www.python.org/ftp/python/3.4.1/python-3.4.1.amd64.msi)
    - Add `;C:\Python34;C:\Python34\Scripts;C:\Python34\Lib\site-packages` to PATH in enviroment variables.
    - 3.4 brings pip so no extra installation needed
 - [Cmake 3.0.1](http://www.cmake.org/files/v3.0/cmake-3.0.1-win32-x86.exe)
 - [Git 1.9.4](https://github.com/msysgit/msysgit/releases/download/Git-1.9.4-preview20140815/Git-1.9.4-preview20140815.exe)
    - Use git from the windows command prompt + checkout windows style , commit unix style.

## Create a python virtual enviroment
 
    cd %HOMEPATH%
    mkdir ws_ros && cd ws_ros
    python -m venv ros2
    ros2\Scripts\activate.bat

## Install the libraries inside the virtual enviroment

    pip install empy
    pip install vcstools
    pip install trollius

## Install ament

We need to tell python (compiled using VS2010) to use VS2013 and run the varsall.bat

    SET VS100COMNTOOLS=%VS120COMNTOOLS%
    C:\Program Files(x86)\Visual Studio 12\VC\vcvarsall.bat

    git clone https://github.com/osrf/osrf_pycommon
    cd osrf_pycommon
    python setup.py install 

    git clone https://github.com/ament/ament_package
    cd ament_package
    python setup.py install

ament should be working at this point
