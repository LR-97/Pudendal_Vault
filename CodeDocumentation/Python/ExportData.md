# ExportData.py
## What is this script for?
This script saves the selections made during the first steps of [[PudendalProtocol#Axon Trajectories|axon trajectory generation]] as a list of points in a .txt file. It uses the Paraview api and must be executed in the Paraview's python shell.

*Note:* Remember to change the Subject variable to the appropriate participant ID, and the 'Side' variable to the correct side based on electrode position
## Dependencies
- Must be executed in Paraview's python shell

## Functionality 
### Save point cloud selections as .txt file
- Set the 'Subject' variable
- For each of the point cloud selections ('G0', 'G1', 'P0', 'P1', 'R0', 'R1', 'M0', 'S2', 'S3', and 'S4):
	- Find the selection using the [FindSource](https://kitware.github.io/paraview-docs/latest/python/paraview.simple.html?highlight=findsource#paraview.simple.FindSource) paraview function
	- Make the selection the active object using the [SetActiveSource](https://kitware.github.io/paraview-docs/latest/python/paraview.simple.html?highlight=setactivesource#paraview.simple.SetActiveSource) Paraview function
	- Save the points in the selection in a .txt file in *Trajectories/Right (or Left)/Anchors* using the Paraview function [SaveData](https://kitware.github.io/paraview-docs/latest/python/paraview.simple.html?highlight=savedata#paraview.simple.SaveData)

## Output
- Text file with 1 header line. Each subsequent line has the an incremental index, and the 3 spatial coordinate, all comma separated.

## Tags
#complete, #Paraview, #axonTrajectories

## Suggestions for improvement
- Make the 'subject' variable a command line argument

## Code I don't understand
- N/A


