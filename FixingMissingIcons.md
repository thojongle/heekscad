A lot of us have been frustrated in an attempt to get icons to show up next to menu items in HeeksCAD/linux. Recent Ubuntu builds seem to have menu icons shut off and they need to be turned back on like this in a terminal:

gconftool-2 --type boolean --set /desktop/gnome/interface/menus\_have\_icons true

This was the web page that had the answere:

http://www.python-forum.org/pythonforum/viewtopic.php?f=4&t=16870&p=86344