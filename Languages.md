## German ##

There already exists HeeksCAD/de/HeeksCAD.po

You must compile this into HeeksCAD.mo

> For Linux, get the gettext package, then in terminal go to HeeksCAD/de folder and type "msgfmt -o HeeksCAD.mo HeeksCAD.po"

> After you have done "sudo make install" for HeeksCAD, you must copy the HeeksCAD.mo file to /usr/local/share/heekscad/de   ( I type "sudo nautilus" to open a folder browser with permission to copy to this folder ).

Now when you type HeeksCAD, if your computer is in German mode, you will see HeeksCAD with translations. This is only working at the moment, if you start HeeksCAD from the Directory "/usr/local/share/heekscad/de"