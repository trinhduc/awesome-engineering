# KiCAD PCB Tips & Trick

## Export Board 3D to STL from KiCAD 3D

![Kicad 3D](images/kicad-3d.png)

- From KiCAD PcbNew, select File -> Export -> VRML file
- Download and install [meshlab](http://meshlab.sourceforge.net/)
- From Meshlab, select File -> Import Mesh -> Select file *WRL was exported 
- From Meshlab, select File -> Export Mesh As -> Select *STL file

**GitHub can host and render 3D files with the .stl extension**

Sample: https://github.com/skalnik/secret-bear-clip/blob/master/stl/clip.stl

## Using BOM Tool, get price list from Digitkey, Mouser ...

https://kicost.readthedocs.io/en/latest/