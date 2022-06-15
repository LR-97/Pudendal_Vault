# TrajectoryFunctions.py
## What is this script for?
This is a template that can be copied and pasted to fill out documentation for the various scripts we use in the pudendal project. Under this heading, provide a general description of the purpose of the script and note key knowledge critical to properly using the script.

## Dependencies
- [[Bezier|Bezier]] from [[Bezier]]
- [[InOutTest|InOut]] from [[InOutTest]]
- [[InOutTest|InOutPar]] from [[InOutTest]]

## Functions
### FindTrajectories
-  **Parameters**
	- *Source:* 
	- *Target:*
	- *R:*
	- *StepSize:*
	- *Basis:*
	- *Pc:* List of facet centroids in an stl file
	- *Pn:* List of normal vectors of facets in an stl file
	- *Pu:* List of vertices in an stl file
- **Description**
	- Description of function's purpose

- **Step-by-Step**
	- List the steps the method is taking to achieve its goal in plain english
	- try to provide the big picture as if explaining to someone who might be unfamiliar with the programming language
	- only state packages being used if they are niche (such as NEURON) but not if they are common (for example, NumPy). 
	- Additionally, link to relevant documentation when possible. For example: [NEURON model file](https://neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/mechanisms/nmodl.html)  

### SmoothTrajectories
-  **Parameters**
	- *PointsArray:* Numpy array containing points describing a trajectory
- **Description**
	- Description of function's purpose

- **Step-by-Step**
	- Define an array, *PP*, with 3 number that dictate how much the trajectory will be upsampled/smoothed in each of 3 rounds of upsampling/smoothing.
	- Make a copy of *PointsArray* named *Points*
	- Set a variable *N* equal to the first value in *PP*
	- Define the *t* array as a linear interpolation from 0 to 1 in 3*N points
	- In segments of N points, smooth the trajectory using the [[Bezier#Bezier]] function. 
	- Append the smooth segments to an array, *Q*
	-  After smoothing all segments, set *Points* equal to *Q*
	- Set *N* equal to the 2nd value in *PP*
	- Recalculate *t* using the new *N* value
	- Repeat the smoothing steps (2nd time)
	- After smoothing all segments, again, set *Points* equal to *Q*
	- Set *N* equal to the 3rd value in *PP*
	- Recalculate *t* using the new *N* value
	- Repeat the smoothing steps (3rd time)
	- Return *Q*

### FindTrajectoriesMulti
-  **Parameters**
	- *param_name_italicized:* Description of parameter
- **Description**
	- Description of function's purpose

- **Step-by-Step**
	- List the steps the method is taking to achieve its goal in plain english
	- try to provide the big picture as if explaining to someone who might be unfamiliar with the programming language
	- only state packages being used if they are niche (such as NEURON) but not if they are common (for example, NumPy). 
	- Additionally, link to relevant documentation when possible. For example: [NEURON model file](https://neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/mechanisms/nmodl.html)  

### FindGuides
-  **Parameters**
	- *param_name_italicized:* Description of parameter
- **Description**
	- Description of function's purpose

- **Step-by-Step**
	- List the steps the method is taking to achieve its goal in plain english
	- try to provide the big picture as if explaining to someone who might be unfamiliar with the programming language
	- only state packages being used if they are niche (such as NEURON) but not if they are common (for example, NumPy). 
	- Additionally, link to relevant documentation when possible. For example: [NEURON model file](https://neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/mechanisms/nmodl.html)  

## Tags
#incomplete #axonTrajectories 

## Suggestions for improvement
- ~~The variable name 'Path' for the input variable to smooth trajectory doesn't make sense in this context. It suggests that it is a string pointing to some, but what gets passed is actually a variable of type numpy array. It should be renamed.~~ Renamed to PointsArray
- Code for [[TrajectoryFunctions#SmoothTrajectories]] is very repetitive. Placing the repeated code in a nested function would increase readability very much.
- The [[TrajectoryFunctions#SmoothTrajectories]] function has a for-loop that goes to a break block by design, the logic could probably be cleaned up to increase readability

## Code I don't understand
- ```Here, copy paste any code portions that you are unsure what it does``` 
	- Here, include the line number in the file to make it easy to find later
	- Feel free to also list any thoughts that you think may be relevant later when reviewing  the confusing code with the rest of the group

