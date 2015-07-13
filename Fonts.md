# Introduction #

HeeksCAD supports the use of two vector font file-formats.  These are the CXF format fonts delivered with the QCAD product as well as the Hershey fonts.  Due to licensing reasons, these font files are not delivered along with the HeeksCAD product.  If they are loaded onto the computer, however, the HeeksCAD product is capable of making use of them.

On Ubuntu Linux, the CXF-format fonts may be delivered within the qcad-data product. Something similar to 'sudo apt-get install qcad-data' should suffice.

Both the CXF and Hershey fonts are vector fonts so that the text which uses them may be converted into Sketch objects via the 'Make a Sketch' menu option (beneath the right mouse click).

The HeeksCAD product also uses one of the OpenGL font files by default.  This OpenGL font is a raster font and cannot, therefore, be converted into Sketch objects.

## Using True Type fonts in Heeks ##

Ribbonsoft have a utility that converts True Type font files into CXF format.  It's called 'ttf2cxf'.  CXF is the format used by Ribbonsoft's QCAD product for its font files.  The CXF format is also supported by HeeksCAD.  The idea is to use the utility to convert a TrueType font into CXF format.  Manually copy the resultant CXF font file into one of the directories configured in the 'font options->font paths' option and refer to the font's name when placing text.

The utility can be found here:
[ftp://ribbonsoft.com/archives/ttf2cxf/ttf2cxf-0.0.0.1-src.tar.gz](ftp://ribbonsoft.com/archives/ttf2cxf/ttf2cxf-0.0.0.1-src.tar.gz)

## Properties ##

The 'Options' panel for HeeksCAD includes a section for Font Options.  This section includes properties for;

### Active Font ###

When a text object is created, this is the font that will be used by default.  The default value here is the OpenGL (raster) font.

### Font Paths ###

This is a semi-colon separated list of directories that hold supported font files.  At the moment it looks for files whose name end in either '.CXF' or '.JHF'.  By default this value is set to /usr/share/qcad/fonts as this is where the qcad-data product puts the fonts by default.  If the Hershey fonts have been downloaded, add the path to their directory in this parameter.  All CXF and Hershey fonts available in the directories specified will be read into memory as HeeksCAD starts up.

### Word and Character Space ###

These two parameters express the word and character spacing values in terms of a percentage of the maximum character width for the current font.