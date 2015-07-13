# Requirements #

This tutorial assumes you already have installed:
  * python
  * wxWidgets (2.8 or 3.0)
  * OpenCASCADE or OCE (OpenCASCADE Community Edition)
  * OpenCAMLib (OCL)


# Fetch #

```
svn checkout http://libarea.googlecode.com/svn/trunk/ libarea
svn checkout http://heekscad.googlecode.com/svn/trunk/ heekscad
svn checkout http://heekscnc.googlecode.com/svn/trunk/ heekscnc
```

# Build and install #
## libarea ##
```
cd libarea
mkdir build
cd build
cmake ..
make
sudo make install
cd ../..
```
## HeeksCAD ##
```
cd heekscad
mkdir build
cd build
cmake ..
make
sudo make install
cd ../..
```
## HeeksCNC ##
```
cd heekscnc
mkdir build
cd build
cmake ..
make
sudo make install
cd ../..
```