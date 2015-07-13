# Easy Installation with RPMS #

openSUSE-Education official project provides rpms for the following products:

HeeksCAD
HeeksCNC
HeeksArt
libarea
libactp

that means, you DO NOT NEED to compile by your own HeeksCAD nor that plugins, just add the following repo to your list, the search and install the packages you like most:

**openSUSE 11.1**:

http://download.opensuse.org/repositories/Education/openSUSE_11.1

**openSUSE 11.0**:

http://download.opensuse.org/repositories/Education/openSUSE_11.0

You can use YaST or zypper, in that case write the following commands to the shell

```
sudo zypper ar -f http://download.opensuse.org/repositories/Education/openSUSE_11.1 openSUSE-Education
sudo zypper in HeeksCAD
#if you want to install all of them then type
sudo zypper in HeeksCAD HeeksCNC HeeksArt
```

# Compiling #

In order to compile bye your own HeeksCAD you need to type the following commands on your shell

**attention** : OpenCASCADE is available on Education repository (the same as before) or in Packman repository: http://packman.links2linux.org/package/OpenCASCADE

```
sudo zypper in OpenCASCADE-devel wxGTK-devel gtkglext-devel subversion
svn checkout http://heekscad.googlecode.com/svn/trunk/ HeeksCAD
cd HeeksCAD
cmake .
sudo make install
```