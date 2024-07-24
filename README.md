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

## In MeshLab:
### 1. Import .xyz file

**Files > Import Mesh**

![Import](/docs/assets/meshlabimport.png)

### 2. Reducing file size

This step will use a function in MeshLab that merges vertices within a set distance of eachother to reduce the total amount of vertices.

**Filters > Cleaning and Repairing > Merge Close Vertices**

![Merge1](/docs/assets/meshlabmerge.png)

This will open a menu:

![Merge2](/docs/assets/meshlabmerge2.png)

Starting with a file size of about 4,000,000 vertices, setting the “perc on” value to 10 reduced the file to about 250,000 vertices. This was just about as much as Solidworks could handle for me later on, but it might be different for you. Try a value for “perc on” and hit apply to see results. The number of vertices in the file are displayed on the bottom of your screen (shown below). Close the menu when finished.

![Merge3](/docs/assets/meshlabmerge3.png)

### 3: Re-orient vertices

Now we will rotate our points to better match the x, y, and z axis. This will make it easier to create a square end product.

**Filters > Normals, Curvatures and Orientation > Transform: Rotate**

![Rotate1](/docs/assets/meshlabrotate.png)

This will open a menu:

![Rotate2](/docs/assets/meshlabrotate2.png)

Select the rotation axis, **make sure to select “barycenter” as the “Center of rotation”**, and change the rotation angle. Start with a small value. Hit apply to rotate the vertices. Each time you hit apply, the vertices will rotate according to the specified rotation angle. This lets you fine-tune their orientation. Close the menu when satisfied with your orientation.

### 4: Create mesh

In this step we will create a mesh from our vertices. First we have to compute normals for point sets.

**Filters > Normals, Curvatures and Orientation > Compute normals for point sets**

![Create1](/docs/assets/meshlabcreate.png)

This will open a menu:

![Create2](/docs/assets/meshlabcreate2.png)

The default settings work. Hit apply and close the menu. Next we will create the actual mesh.

**Filters > Remeshing, Simplification and Reconstruction > Surface Reconstruction: Screened Poisson**

![Create3](/docs/assets/meshlabcreate3.png)

This will open a menu:

![Create4](/docs/assets/meshlabcreate4.png)

The default settings work. Hit apply and close the menu. This will create a new mesh layer in gray (shown below). The original vertices are highlighted yellow.

![Create5](/docs/assets/meshlabcreate5.png)

### 5: Edit mesh

You’ll notice that the new mesh is larger than needed. In this step we will trim it down to fit our actual data points. Click the button indicated below. Hover over it with the mouse and it should display “Select Faces in a rectangular region”.

![Trim1](/docs/assets/meshlabtrim.png)

The following red info box will pop up on the upper left part of your screen:

![Trim2](/docs/assets/meshlabtrim2.png)

Click and drag with the mouse to highlight your desired region of the mesh, then use the “I” (invert all) key to select everything outside your desired region. Anything you would like to remove should be highlighted red. Now select the “Select Faces in a rectangular region” button again and the red info box should disappear. Then click the last button on the top taskbar (shown below) to delete all selected vertices and faces. 

![Trim3](/docs/assets/meshlabtrim3.png)

Then, we will repair all non-manifold edges. These can cause issues later in the process when importing a final 3D object into slicing programs.

**Filters > Cleaning and Repairing > Repair non Manifold Edges**

![Trim4](/docs/assets/meshlabtrim4.png)

This will open a menu:

![Trim5](/docs/assets/meshlabtrim5.png)

The default “Remove Faces” option works. Hit apply and close the menu.

### 6: Move origin

Because my original data was in UTM coordinates, the actual origin of the mesh (0, 0, 0) was super far away. This causes issues when importing the mesh into any CAD software. As soon as I’d try to even rotate the mesh, it would fly off into the distance. To solve this problem, we will move the origin of the mesh to its centroid. 

**Filters > Normals, Curvatures and Orientation > Transform: Translate, Center, set Origin**

![Origin1](/docs/assets/meshlaborigin.png)

This will open a menu:

![Origin2](/docs/assets/meshlaborigin2.png)

Click the drop-down arrow and change the “transformation” option to “Center on Scene BBox”. Then hit apply and close the menu. Your mesh might disappear! Don’t worry, it is still there.

### 7: Export as .stl

First, make sure the “Poisson mesh” layer is highlighted on the right upper part of your screen.

![Export1](/docs/assets/meshlabexport.png)

Now we can export our mesh as an .stl file.

**File > Export Mesh As**

![Export2](/docs/assets/meshlabexport2.png)

## In Solidworks:
