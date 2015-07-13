# Prerequisites #

You definitely have to install XCode developer tools (which come optional from the OS X install DVD or available from the Apple web site) . And there are some other necessary things. OpenCASCADE needs a X11 Tcl and HeeksCAD needs a X11 wxWidgets like wxGTK and Python. All three can easily be installed from [Fink](http://fink.sf.net).

Actually, the only version of wxwidgets known to work is wxgtk (wxgtk2.8 from fink) -the native mac version wxMac is known to NOT work-the mac libraries seem to share the same Handle name with OCC in the code. You also need gtkglext for opengl support.

To install Fink for OS X 10.6 you need to do a source install from http://www.finkproject.org/download/srcdist.php, though it is relatively easy.
Previous versions (OS X 10.5) can use the links at http://www.finkproject.org/download/index.php?phpLang=en

Install wxgtk,gtkglext:

```
"fink install wxgtk2.8"
"fink install wxgtk2.8-shlibs"
"fink install gtkglext1"
```
fink will ask to install a ton of dependencies- answer 'yes'

# OpenCASCADE #

Download and unpack [OpenCASCADE](http://www.opencascade.org/getocc/download/loadocc/).

You need to patch the DRAWEXE Makefile

```
--- adm/make/DRAWEXE/Makefile.am.orig 2008-09-06 14:15:14.000000000 +0200
+++ adm/make/DRAWEXE/Makefile.am 2008-09-06 14:33:58.000000000 +0200
@@ -22,4 +22,4 @@
../TKMath/libTKMath.la \
../TKG3d/libTKG3d.la \
../TKernel/libTKernel.la \
- $(STLPort_LIB) $(CSF_TclLibs_LIB) $(CSF_TclTkLibs_LIB) $(CSF_gdi32_LIB) $(CSF_advapi32_LIB) $(CSF_user32_LIB) $(CSF_SOCKETLibs_LIB) $(CSF_FPELibs_LIB) $(CSF_ThreadLibs_LIB) $(CSF_kernel32_LIB) 
+ $(STLPort_LIB) $(CSF_TclLibs_LIB) $(CSF_TclTkLibs_LIB) $(CSF_gdi32_LIB) $(CSF_advapi32_LIB) $(CSF_user32_LIB) $(CSF_SOCKETLibs_LIB) $(CSF_FPELibs_LIB) $(CSF_ThreadLibs_LIB) $(CSF_kernel32_LIB) $(CSF_XwLibs_LIB) 
```

The configure script and the ltmain.sh are too old. The latter was provided by fink and the former was solved by running the whole GNU auto magic:

```
export CASROOT=/WhereeverYouPut/OpenCASCADE6.3.0/ros
cd ${CASROOT}
aclocal
automake
autoconf
cp /sw/share/libtool/ltmain.sh make/
export TCLHOME=/sw
#configure does not honor --with-gl-include
export CPPFLAGS=-I/usr/X11R6/include
flags="--with-gl-include=/usr/X11R6/include --with-gl-library=/usr/X11R6/lib"
flags="$flags --with-xmu-include=/usr/X11R6/include/X11"
flags="$flags --with-xmu-library=/usr/X11R6/lib"
flags="$flags --with-tcl=${TCLHOME}/lib"
flags="$flags --with-tk=${TCLHOME}/lib "
flags="$flags --with-java-include=/System/Library/Frameworks/JavaVM.framework/Versions/A/Headers/ "
flags="$flags --disable-debug --enable-production"
flags="$flags --enable-wrappers=yes"
flags="$flags --enable-wok=yes"
flags="$flags --enable-draw=yes"
./configure --prefix=${CASROOT}/mac $flags
make
make install
```

# HeeksCAD #

Copy buildenv\_mac.example to buildenv\_mac. Change the variables to your needs. You might just change the OpenCASCADE installation path.

```
source buildenv_mac
cd src
make
```