# How to build HeeksCAD 1.0 #

How to build HeeksCAD 1.0 for Windows

I used a 64bit SONY VPCCB running Windows 7

download and install TortoiseSVN software from here http://tortoisesvn.net/
make a new folder on your computer somewhere, called HeeksCAD1.0
I made this folder "C:\Dev\HeeksCAD1.0"
right click on the HeeksCAD1.0 folder and do "TortoiseSVN"->"SVN Checkout..."
The "URL of repository":
http://heekscad.googlecode.com/svn//branches/v1_0/
The Checkout directory something like:
C:\Dev\HeeksCAD1.0
Press OK.
It should checkout all the HeeksCAD 1.0 source code


Get Microsoft Visual C++ 2008 Express Edition ( it's free, but about 1GB ) or use full version.

Download and install the Open CASCADE installation. I am currently using 6.5.2. http://www.opencascade.org/getocc/download/loadocc/ ( OpenCASCADE652.exe )

Download and install the wxWidgets installation. I am using 2.8.12. http://sourceforge.net/projects/wxwindows/files/2.8.12/wxMSW-2.8.12-Setup.exe/download

Set an environment variable called WXWIN to be
C:\wxWidgets-2.8.12
or whereever wxWidgets installed to. ( to set an environment variable go to Control Panel -> System and Security -> System -> Advanced system settings -> press "Environment Variables" button -> in "user variable" add new ).
( you must restart Visual Studio for it to know the new environment variable )

Edit C:\wxWidgets-2.8.12\include\wx\msw\setup.h changing "#define wxUSE\_GLCANVAS 0" to "#define wxUSE\_GLCANVAS 1" and changing "#define wxUSE\_ODBC 0" to "#define wxUSE\_ODBC 1"

Open C:\wxWidgets-2.8.12\build\msw\wx\_dll.dsw ( let VC2008 convert the projects ). Change the configuration to "DLL Unicode Release".
Press "Build Solution"

Copy 4 of the dlls that get made from C:\wxWidgets-2.8.12\lib\vc\_dll to HeeksCAD1.0 ( the folder you checked out this project to ).

They are: wxbase28u\_vc\_custom.dll wxmsw28u\_aui\_vc\_custom.dll wxmsw28u\_core\_vc\_custom.dll wxmsw28u\_gl\_vc\_custom.dll

Make an environment variable called
CASROOT
with value of
C:\OpenCASCADE6.5.2\ros

Get libarea source code:
> make "C:\Dev\libarea"
> SVN Checkout in the same way but with libarea instead of HeeksCAD


> add an environment variable to your computer

> called
> LIBAREA\_PATH
> with value as where your libarea code is, for example for me it is
> C:\Dev\libarea



copy all the dlls from C:\OpenCASCADE6.5.2\ros\win32\vc8\bin to C:\Dev\HeeksCAD1.0
copy all the dlls from C:\OpenCASCADE6.5.2\3rdparty\win32\tbb\bin to C:\Dev\HeeksCAD1.0
copy the dlls from C:\OpenCASCADE6.5.2\3rdparty\win32\freeimage\bin to C:\Dev\HeeksCAD1.0

Open "C:\Dev\HeeksCAD1.0\src\HeeksCAD VC2008.sln" with Visual Studio 2008.
Change configuration to "Unicode Release"

Press "Build Solution"

If it builds OK, press "Start without Debugging"