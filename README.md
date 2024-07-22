# 3D Printing with .xyz Data
## Introduction:
This document will go over the main steps needed to turn a point-cloud .xyz file of a real-world surface into a 3D-printable .stl file. The programs I used were MeshLab and Solidworks. MeshLab is free and open-source, while Solidworks is not. However, most of the steps taken in Solidworks should be easily replicated in other CAD programs. 
[Free MeshLab Download](https://www.meshlab.net/)
## Process Overview:
### In MeshLab:
1. Import .xyz file
2. Reduce size of file (amount of vertices)
3. Re-orient vertices
4. Create mesh
5. Edit mesh
6. Move origin
7. Export as .stl
### In Solidworks:
1. Import .stl file
2. Create mesh body
3. Create base
4. Trim edges
5. Export as .stl

You can then open this .stl in any slicing program and print!
