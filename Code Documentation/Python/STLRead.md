# STLRead.py
## What is this script for?
The STLRead.py script is used to parse an .stl file for all the information needed to recreate the geometry. Stl files describe 3d surface geometry as a list of triangular facets defined by the facet's normal vector and its vertices. The script return a unique (no repeated entries) list of the geometry's vertices, a list of the centroids of facets, and a list of the unit normal vectors of facets.

*Note:* STL files must use the ASCII encoding, not binary.

## Dependencies
- Numpy

## Functions 
### read_stl
-  **Parameters**
	- *filename:* filepath of .stl file
- **Description**
	- Read a .stl file and return the points that define the face boundaries, the face normals, and the face centers of the file.
- **Outputs**
	- *PU*: List of all the unique vertices in the file
	- *PC*: List of all the centroids of the triangular facets of the file
	- *N*: List of unit normal vectors of all the triangular facets

- **Step-by-Step**
	- Define python lists for each of the outputs (points that define a face: 'P', normal of the face: 'N', and center of the face: 'Pc')
	- **For each line in the the file:**
		- **If the line starts with 'vertex':**
			The 'Vertex' keyword precedes the coordinates of triangle facets
			- Parse the line and place the vertex coordinates in a list
			- Append the vertex list to the 'P' list
			- Add the x, y, z coordinates to their respective variables (Xc, Yc, Zc) tracking the sum of the coordinates of a facet. Later used for calculating the centroid of the facet
		- **If the line starts with 'facet normal':**
			The 'facet normal' keyword indicates the start of a fact declaration, and it is followed by the coordinates describing the unit normal vector of the facet
			- Parse the line and place the unit normal vector coordinates in a list
			- Append the normal vector list to the 'N' list
		- **If the line starts with 'outer':**
			The 'Outer' keyword signals the start of the enumeration of a facet's vertices
			- Initialize the Xc, Yc, and Zc variables used to calculate the facet centroid
		- **If the line starts with 'endloop':**
			The 'endloop' keyword signals the end of a facet description
			- Calculate the centroid of the triangle by dividing Xc, Yc, and Zc by three (essentially taking the mean of the vertices' coordinates)
			- Append the centroid to the 'Pc' list
	- Convert 'P', 'PC', and 'N' from python lists to numpy arrays
	- Apply the '.unique' numpy method to 'P' so that only unique entries in 'P' are kept, and store this as 'PU'
	- Return 'PU', 'PC', and 'N'

## Tags
#complete #axonTrajectories 

## Suggestions for improvement
- There is also a ReadSTL.py file that seems to be a duplicate, and doesn't seem to be used *yet*. Considered deleting that file for the sake of cleanliness.

## Code I don't understand


