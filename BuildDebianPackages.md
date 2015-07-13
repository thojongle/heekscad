# Requirement: libarea #
HeeksCAD requires libarea, this section will explain how to build and install libarea using the Debian way.

## Install build dependencies ##
```
sudo apt-get install subversion build-essential debhelper cmake libboost-python-dev
```

## Fetch sources ##
```
svn checkout http://libarea.googlecode.com/svn/trunk/ libarea
cd libarea
```

## Build packages ##

```
dpkg-buildpackage -b -us -uc
```

This will produces 3 packages: libarea0, libarea-dev and python-area.

## Install packages ##
```
cd ..
sudo dpkg -i libarea*.deb python-area*.deb
```

# HeeksCAD #
When libarea is correctly installed, we can build HeeksCAD packages the same way.

## Install build dependencies ##
On system released before 2013 (ie. Ubuntu 10.04 LTS, 12.04 LTS):
```
sudo apt-get install libopencascade-visualization-dev libwxgtk2.8-dev libgtkglext1-dev python-dev
```

On more recent system:
```
sudo apt-get install liboce-visualization-dev libwxgtk2.8-dev libgtkglext1-dev python-dev
```

## Fetch sources ##

```
svn checkout http://heekscad.googlecode.com/svn/trunk/ heekscad
cd heekscad
```

## Build packages ##

```
dpkg-buildpackage -b -us -uc
```

This will produces 4 packages: heekscad, heekscad-dev, libheekstinyxml0 and libheekstinyxml-dev

## Install run-time dependencies ##
If you want a fully translated version:
```
sudo apt-get install wx2.8-i18n
```

## Install packages ##
```
cd ..
sudo dpkg -i *heeks*.deb
```

# Optionnal: HeeksCNC #
If you want to use HeeksCNC, CAM plugin, have a look to:
https://code.google.com/p/heekscnc/wiki/DebianPackagesBuild