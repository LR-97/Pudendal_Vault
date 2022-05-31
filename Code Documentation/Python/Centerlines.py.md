# Centerlines.py
## What is this script for?
This script creates centerlines for the different portions of the pudendal nerve (roots-through-trunk centerlines, and branches centerlines). It utilizes the .txt files created by [[ExportData.py]] and derived from  [[Pudendal Protocol#Axon Trajectories| previously made paraview selections]]. It also requires the VMTK package, see the pudendal protocol for more details. The script exports .vtk and .txt files describing the centerlines.

*Note:* Remember to change the Subject variable to the appropriate participant ID, and the 'Side' variable to the correct side based on electrode position

## Dependencies
- [pypes](http://www.vmtk.org/documentation/pypes.html) from [vmtk](http://www.vmtk.org/documentation/)
- [vmtkcenterlines](http://www.vmtk.org/vmtkscripts/vmtkcenterlines.html) from [vmtk](http://www.vmtk.org/documentation/)
- [vmtkcenterlinestonumpy](http://www.vmtk.org/vmtkscripts/vmtkcenterlinestonumpy.html) from [vmtk](http://www.vmtk.org/documentation/)
- [vmtkscripts](http://www.vmtk.org/tutorials/ScriptsBasic.html) from [vmtk](http://www.vmtk.org/documentation/)

## Functionality 
### Compute centroids of selections (lines 6-29)
- **For each of the [[Pudendal Protocol#Axon Trajectories| previously made paraview selections]] ('G0', 'G1', 'P0', 'P1', 'R0', 'R1', 'M0', 'S2', 'S3', and 'S4'):**
	- Load the respective selection's text file, and parse for the coordinates of the points in the selection
	- Average the x, y, and z coordinates to compute the centroid of the selection 
	- Format the centroid coordinates as a 2D numpy float array
	- Store the centroid array in a python dictionary called 'Anchors' where the key is the name of the selection
- Define the 'Paths' python list with the names ('G0G1', 'R0R1', 'P0P1', 'M0S2', 'M0S3', 'M0S4') of the centerlines we need to create from the paraview selections.

### Instantiate a VMTK Surface Reader (lines 33- 35)
- Create an instance of [[Centerlines.py#Dependencies|vmtkSurfaceReader]]
- Set the SurfaceReader's InputFileName property to be the filepath of the pudendal nerve .stl file 
- Call the SurfaceReader's Execute() method

### Create centerlines (lines 37-67)
- **For each path in the 'Paths' list:**
	-  Split the path from 'Paths' into a 'source' and 'target' string (ex. source = G0 and target = G1)
	- **Compute the centerline (38-47): **
		- Create an instance of a [[Centerlines.py#Dependencies|vmtkCenterlines]] object
		- Assign the the Centerlines' surface to the be the same as the SurfaceReader's 'surface' attribute
		- Indicate that the centerline's seed points will come from a points list by setting the centerlines object's 'SeedSelectorName' property to be 'pointlist'
		- Set the centerlines object's 'SourcePoints' property to be the centroid of the current source selection by accessing the 'Anchors' dictionary
		- Set the centerlines object's 'TargetPoints' property to be the centroid of the current target selection by accessing the 'Anchors' dictionary
		- Call the centerlines object's 'Execute()' method
	- **Save the centerline as a .vtk file (48-51):**
		- Create an instance of a [[Centerlines.py#Dependencies|vmtkSurfaceWriter]] object
		- Set the surface writer's 'OutputFileName' property with the appropriate path
		- Set the surface writer's 'Surface' property to be the centerlines object's 'Centerlines' property
		- Call the surface writer's 'Execute()' method to create the output vtk file
	- **Convert centerline to numpy-compatible format (53-59):**
		- Instantiate another surface reader to read the centerline vmtk path we just created
		- Set the surface reader's 'InputFileName' property to be the path of the vtk file just created
		- Call the new surface reader's 'Execute()' method
		- Create an instance of a [[Centerlines.py#Dependencies|vmtkCenterlinesToNumpy]] object
		- Set the 'Centerlines' attribute of the CenterlinesToNumpy object to be equal to the 'Surface' attribute of the new surface reader
		- Call the CenterlinesToNumpy object's 'Execute()' method
		- Fetch the numpy-formatted centerline data (stored as a python dictionary) from the CenterlinesToNumpy object by calling the 'ArrayDict' attribute
	- **Save the centerline as a .txt file (61-67):**
		- Concatenate the centerline point coordinates and their respective maximum inscribed sphere radius into a single numpy array 
		- Save the numpy array as a .txt file

## Output (use if the script outputs a file)
- .vtk files for the centerline of each portion of the the nerve
- .txt files describing the coordinates and maximum inscribed radius for the centerline of each portion of the nerve

## Tags
#complete #paraview #axonTrajectories 

## Suggestions for improvement
- The nested for-loop in lines 14-28  throws exceptions by design. This is bad practice since it makes it harder to understand what is going on. Changing the names variable to include all the valid filenames would fix this and make the code more concise.

## Code I don't understand


