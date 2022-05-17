# Cell_rdg.py
## What is this script for?
The Cell_rdg script contains the 'Cell' class and the 'MRG' class (which inherits from Cell). We use it to create MRG axon NEURON models

## Dependencies
- **find_node_coordinates**, and **find_node_coordinatesQ** from **functions.find_node_coordinates import** 
## Classes
### Cell (class)
- The cell class is used to instantiate a generic cell object. It must be provided with the path to the directory containing the cell's [NEURON model file](https://neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/mechanisms/nmodl.html) (.hoc) as well as the name and extension of the NEURON model file.

#### Parameters:
- **CELL_DIR**: Path to directory containing the model file
- **CELL_FILE_NAME**: Name of Hoc model file (usually 'NewMRGaxon_for_Python.hoc')
	
#### Class Methods:
##### _ _ Init _ _
-  **Parameters**:
- **Summary**: Initializes Cell object
- **Step-by-step**:
	- Save passed parameters
	- Check if given CELL_DIR & CELL_FILE_NAME. If False, raise TypeError
	- set the environment variable  [nrn.NRN_NMODL_PATH](https://www.frontiersin.org/articles/10.3389/neuro.11.001.2009/full) equal to CELL_DIR
	- [Import the mechanisms](https://neuron.yale.edu/neuron/static/py_doc/programming/neuronpython.html?highlight=load_mechanisms#neuron.load_mechanisms) stored in CELL_DIR 
	- Construct the cell via the [[#_construct_cell |_contruct_cell()]] class method
	- load the extracellular mechanisms via [[#_xtra|_xtra()]] class method
	- create anaction potential counter using the  [[#_ap_counters|_ap_counters()]] class method

##### _construct_cell
- "raise 'Dummy Axon'"
- Empty method overridden by child class (ex. [[#MRG (class) | MRG]])

##### _ap_counters
-  **Parameters**: Self
- **Summary**: Creates an action potential counter, which is especially useful for threshold calculation
- **Step-by-step**:
	- Create instance of [h.APCount](https://neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/mechanisms/mech.html?highlight=apcounter#APCount)
	- Set the voltage threshold for AP detection in mV
	- Create [h.vector](https://neuron.yale.edu/neuron/static/py_doc/programming/math/vector.html?highlight=vector) to append to the times of threshold crossing in ms
	- Attach times vector to APCount instance via [.record()](https://neuron.yale.edu/neuron/static/py_doc/programming/math/vector.html?highlight=vector) method

##### root_section
-  **Parameters**: Self
- **Summary**: Return the root [section](https://www.neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/topology/geometry.html) of the current cell
- **Step-by-step**:
	- Calls [h.SectionRef().root](https://neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/topology/secref.html?highlight=sectionref%20root#SectionRef.root)

##### center_3Dcoords
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### get_im
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### build_tree
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### display
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### draw
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### move
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### rotate
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### retrieve_coordinates
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### record
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### plot
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### store
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### _xtra
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### set_tstop
-  **Parameters**: Self, tstop
- **Summary**:
- **Step-by-step**:

##### set_variable
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### get_variable
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

### MRG (class)
- The MRG class is a child class of the [[#Cell class|Cell]] superclass, and it is used to implement the [McIntyre, Richardson, Grill model of mammalian nerve fibers](https://journals.physiology.org/doi/full/10.1152/jn.00353.2001?rfr_dat=cr_pub++0pubmed&url_ver=Z39.88-2003&rfr_id=ori%3Arid%3Acrossref.org) in NEURON.

#### Parameters
- **axon_trajectory**:
- **fiberD**:
- **CELL_DIR**: see [[#Parameters|CELL_DIR]]
- **CELL_FILE_NAME**: see [[#Parameters|CELL_FILE_NAME]]
#### Class Methods
##### __ __ Init __ __
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### get_secs
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### _construct_cell
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

##### _my_ap_counters
-  **Parameters**: Self
- **Summary**:
- **Step-by-step**:

## Code suggestions
- get rid of variable setter and getter in Cell class, instead implement with @property decorator
