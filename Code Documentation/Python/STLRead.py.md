# STLRead.py
## What is this script for?


## Dependencies
- Numpy

## Functions 
### read_stl
-  **Parameters**
	- *filename:* Description of parameter
- **Description**
	- Read a .stl file and return the points that define the face boundaries, the face normals, and the face centers of the file.

- **Step-by-Step**
	- Define python lists for each of the outputs (points that define a face: 'P', normal of the face: 'N', and center of the face: 'Pc')
	- **For each line in the the file:**
		- **If the line starts with 'vertex':**
			- Parse the line and place the vertex coordinates in a list
			- Append the vertex list to the 'P list'
		- **If the line starts with 'facet normal':**
		- **If the line starts with 'outer':**
		- **If the line starts with 'endloop':**

### sampleFunction
-  **Parameters**
	- *param_name_italicized:* Description of parameter
- **Description**
	- Description of function's purpose

- **Step-by-Step**
	- 

## Tags
#incomplete 

## Suggestions for improvement
- There is also a ReadSTL.py file that seems to be a duplicate, and doesn't seem to be used *yet*. Considered deleting that file for the sake of cleanliness.

## Code I don't understand
- ```Here, copy paste any code portions that you are unsure what it does``` 
	- Here, include the line number in the file to make it easy to find later
	- Feel free to also list any thoughts that you think may be relevant later when reviewing  the confusing code with the rest of the group

