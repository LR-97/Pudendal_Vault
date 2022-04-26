# CommandThresholdCalculation.py
## What is this script for?
The 'CommandThresholdCalculation' script is the [[python scripts|python script]] we use to calculate the threshold voltage of the axons of our model. The script is called via the command line interface (CLI). It is given as inputs the [[subject id]],  the [[stimulation configuration]], and the [[branch]] the fiber terminates at. It uses this information to retrive the [[trajectories]] of the axons terminating at the specified branch and the [[voltages]] along the trajectories of these axons. It then builds a neuron model for each fiber and determines the threshold using a [[bisection algorithm]]. For each axon, the output is a .txt file listing an upper bound and lower bound estimate of the threshold. The threshold can be taken to be the midpoint between the two bounds.

*Note:* When running CommandThresholdCalculation.py, the current working directory should be the 'Python' folder of the 'Pudendal' folder on the 'E:' drive

## Dependencies
- [[Cell_rdg#MRG class|MRG]] from [[Cell_rdg|classes.Cell_rdg]] 
- [[rec_dict]] from [[rec_dict|functions.rec_dict]]
- [[Voltages]] from [[functions.Voltages]] 

## Functions
### Model
-  **Parameters**
	- *Traj:* 
- **Description**
	- The "Model" function takes as input an axons [[trajectory]] and return an MRG NEURON model ([[Cell_rdg#MRG class|MRG Object]]) that follows the input trajectory. Additionally, it sets simulation parameters and creates a [[rec_dict|recording dictionary]] that records membrane voltage of each 'node' compartment of the axon model throughout the duration of the simulation.

- **Step-by-Step**
	- Set simulation parameters:
		- Toggle off the variable time-step integration method (Cvode). See [h.CVode.active()](https://www.neuron.yale.edu/neuron/static/py_doc/simctrl/cvode.html#CVode.active)
		- Set the integration interval [h.dt](https://www.neuron.yale.edu/neuron/static/py_doc/simctrl/programmatic.html?highlight=dt#dt) (in kHz) using h.steps_per_ms. 
		- Set the temperature of the simulation using [h.celsius](https://www.neuron.yale.edu/neuron/static/py_doc/simctrl/programmatic.html?highlight=celsius#celsius)
		- Set the initial voltage of the model compartments  (currently -80mV) using h.v_init
	- Set the fiber diameter in micrometers (currently fixed at 7.3um)
	- Create the axon model using the imported [[Cell_rdg]] module
	- Create the axon's recording dictionary by looping through the compartments of the axon using the [[Cell_rdg#get_secs|'gets_secs' method of the MRG class]], checking if the compartment is a node (using [sec.name()](https://www.neuron.yale.edu/neuron/static/py_doc/modelspec/programmatic/topology.html?highlight=name#Section.name)), and if it is a node, using the imported [[rec_dict]] function.
	- Pass the dictionary to the MRG object using the [[Cell_rdg#record|'record']] class method
	- Return the MRG object created

### UpdateConfig
- **Parameters**
	- *MyCell*: The current axon, of type [[Cell_rdg#MRG class|MRG object]] 
	-  *Name*: Name of the curren cell, of form branch_root_id (ex. G_S2_10)
- **Description**
	- Given a cell and the cell name, UpdateConfig loads the k-values along the fiber trajectory and assigns them to the transfer impedance attribute [[rx_xtra]] of their respective NEURON section. 

- **Step-by-Step**
	- load to memory the voltages (k-values) file for the current electrode configuration and fiber name
	- extract the voltages/k-values from the last column in the file. 
		- _Note:_ values in the file are not listed in spatially sequential order. They are ordered in the same order the [[Cell_rdg#get_secs|get_secs()]] method iterates through MRG sections
	- Iterate through the MRG sections using [[Cell_rdg#get_secs|get_secs()]] and assign 
		- Set the rx_xtra attribute of the current section equal to its respective k-value
			- _Note_: The k-values get scaled by 1e-6. [[Why?]]
	- Return MyCell and the voltage values ndarray.

### UpdateStim
- **Parameters**
- **Description**
- **Step-by-step**

### RunModel
- **Parameters**
- **Description**
- **Step-by-step**

### Target
- **Parameters**
- **Description**
- **Step-by-step**

### Trial
- **Parameters**
- **Description**
- **Step-by-step**

### Threshold
- **Parameters**
- **Description**
- **Step-by-step**

## Main Code Section

## Suggestions for improvement
- Instead of saving the upper and lower bound to a .txt file, save only the midpoint value.
- Modifiy [[CommandThresholdCalculation#Model| Model(traj)]] to also take as a parameter the desired fiber diameter
- Give UpdateConfig a more descriptive name
- In UpdateConfig, get rid of the iSec index, instead use an enumerate() loop
- UpdataConfig doesnt have to return anything, I think.
- Encapsulate main code section inf a main() function and use an "if name == main" type statement.

## Code I dont understand
- sys.path.insert(0, "/Applications/NEURON-7.7/nrn/x86_64/bin")
	- line 22
	- What is the path?
- sys.path.insert(0, "/Applications/NEURON-7.7/nrn/lib/python")
	- line 23
	- What is the path?
- Using both h.steps_per_ms and h.dt=1/h.steps_per_ms
	- lines 34 & 35
	- I believe its so that h.dt is an exact binary variable (confirm with someone) 
	- If so, why is this important?
