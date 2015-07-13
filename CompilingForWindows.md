# How to build HeeksCAD for Windows #

I used a 64bit SONY VPCCB running Windows 7

download and install TortoiseSVN software from here http://tortoisesvn.net/
make a new folder on your computer somewhere, called HeeksCAD.
I made these folders "C:\Dev\HeeksCAD"
right click on the HeeksCAD folder and do "TortoiseSVN"->"SVN Checkout..."
The "URL of repository":
http://heekscad.googlecode.com/svn/trunk/
The Checkout directory something like:
C:\Dev\HeeksCAD
Press OK.
It should checkout all the HeeksCAD source code

Get Microsoft Visual Studio 2013 Express Desktop version.

Download and install the Open CASCADE installation. I am currently using 6.5.2. http://www.opencascade.org/getocc/download/loadocc/ ( OpenCASCADE652.exe )

Download and install the wxWidgets 3.0 installation;
the zip file from here https://www.wxwidgets.org/downloads/
and extract it to C:\wxWidgets-3.0.0

Set an environment variable called WXWIN30 to be
C:\wxWidgets-3.0.0  ( to set an environment variable go to Control Panel -> System and Security -> System -> Advanced system settings -> press "Environment Variables" button -> in "user variable" add new ).
( you must restart Visual Studio for it to know the new environment variable )

Open C:\wxWidgets-3.0.0\build\msw\wx\_dll.dsw ( let Visual Studio convert the projects ). Change the configuration to "DLL Release".
Press "Build Solution"

Copy 4 of the dlls that get made from C:\wxWidgets-3.0.0\lib\vc\_dll to HeeksCAD ( the folder you checked out this project to ).

They are: wxbase30u\_vc\_custom.dll wxmsw30u\_aui\_vc\_custom.dll wxmsw30u\_core\_vc\_custom.dll wxmsw30u\_gl\_vc\_custom.dll

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



copy all the dlls from C:\OpenCASCADE6.5.2\ros\win32\vc8\bin to C:\Dev\HeeksCAD
copy all the dlls from C:\OpenCASCADE6.5.2\3rdparty\win32\tbb\bin to C:\Dev\HeeksCAD
copy the dlls from C:\OpenCASCADE6.5.2\3rdparty\win32\freeimage\bin to C:\Dev\HeeksCAD

Open "C:\Dev\HeeksCAD\src\HeeksCAD VC2013.sln"
Change configuration to "Unicode Release"

Press "Build Solution"

If it builds OK, there will be a HeeksCAD.exe at "C:\Dev\HeeksCAD"