# Electrode.m
## What is this script for?
This matlab script creates a comsol model of a participant's electrode. It requires two .xml files describing the electrode's centerline and the centroids of the electrode contacts. For more details, see [[PudendalProtocol#Electrode reconstruction|here]].

## Dependencies
- [Comsol with Matlab](https://doc.comsol.com/5.4/doc/com.comsol.help.llmatlab/LiveLinkForMATLABUsersGuide.pdf)

## Functionality 
### Filepath Generation (3-23)
- The subject ID is provided by the user (update 'Subj_ID')
- The root directory is obtained from the current working directory
- Using the Root and Subj_ID variables create the following paths: 'Path_Model', 'Path_Centerline', 'Path_Contacts', 'Path_Export', 'Path_Save', and 'Path_SelC'
- Verify that the centerline and contacts xml files exist

### Centerline Preprocessing (24-30)
- Load the data in centerline.xml
- isolate the centerline x, y, and z coordinates to their own vectors

### Model Creation (31-40)
- Create a new model object in the comsol server
- Create a 3D geometry with units of mm

### Centerline Creation (41-44)
- Create an interpolation curve named 'ic1' using the centerline xml file as the source
- Useful links: [Interpolation curve documentation](https://doc.comsol.com/5.5/doc/com.comsol.help.comsol/comsol_ref_geometry.14.038.html), [Interpolation curve API documentation](https://doc.comsol.com/5.4/doc/com.comsol.help.comsol/comsol_api_geom.39.090.html)

### Create Plane normal to electrode tip (45-51)
- Create a comsol [work plane](https://doc.comsol.com/5.5/doc/com.comsol.help.comsol/comsol_api_geom.39.134.html) 'wp1' defined by the normal vector 'N0' spanning from the tip of the electrode centerline (point 'P0') to the next centerline point
	- *Note:* This step assumes that the first point in the centerline xml file is the distal tip of the electrode. If that's not the case this would create issues.
- Useful links: [Work plane documentation](https://doc.comsol.com/5.5/doc/com.comsol.help.comsol/comsol_ref_geometry.14.088.html), [Work plane API documentation](https://doc.comsol.com/5.5/doc/com.comsol.help.comsol/comsol_api_geom.39.134.html)

### Sweep wire cross-section along centerline (52-66)
- On the normal plane 'wp1', draw a circle of diameter equal to the electrode diameter (1.27mm)
- Create a sweep geometry object that extrudes the circle on 'wp1' (the elctrode cross-section) along the interpolation curve 'ic1' (the electrode centerline).
- Useful links: [Sweep documentation](https://doc.comsol.com/5.5/doc/com.comsol.help.comsol/comsol_ref_geometry.14.085.html), [Sweep API documentation](https://doc.comsol.com/5.5/doc/com.comsol.help.comsol/comsol_api_geom.39.129.html)

### (67-77)
- Initialize the boolean variable Plane and Partition as true and false, respectively
- Get *dx, dy, dz* by calculating the difference between adjecent elements of the centerline x, y, z coordinate vectors using [diff](https://www.mathworks.com/help/matlab/ref/diff.html)
- Calculate the numerical gradient of the centerline x, y, z coordinate vectors using [gradient](https://www.mathworks.com/help/matlab/ref/gradient.html?s_tid=doc_ta)
- Use dx, dy, dz to compute the derivative, *ds* of a parametric version of the centerline
- Sum the elements of ds to calculate the arc length of the centerline

## Tags
#incomplete 

## Suggestions for improvement
- Change the subj_ID variable to be a prompt, in order to prevent the user forgetting update the subj_ID string
	- Line 4

## Code I don't understand
- ```geom1.feature('wp1').set('unite',true)``` 
	- line 55
	- I think this unites any 2D geometries on the workplane to make it easier to apply 3d operations (like sweep) on the 2d geometries?

