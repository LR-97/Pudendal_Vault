# rec_dict.py
## What is this script for?
This script contains the  rec_dict function which is used define a python dictionary of variables to be recorded during a NEURON simulation. It outputs a dictionary in the form:
- self.recording_dict = {sec.variable : h.sec(location)._ref_variable}

## Parameters:
- **recording_dict**: the name of the dictionary to append
- **sec** : the neuron section object
- **location** : the location within the section (0 <= location <= 1)
- **variable**: independent or state variable to be recorded (e.g. vm, i_membrane)

## Suggestions for improvement
- Rewrite in such a way that the eval() function is not used.