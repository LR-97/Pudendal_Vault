# Electrode.m
## What is this script for?
This matlab script creates a comsol model of a participant's electrode. It requires two .xml files describing the electrode's centerline and the centroids of the electrode contacts. For more details, see [[Pudendal Protocol#Electrode reconstruction|here]].

## Dependencies
- [Comsol with Matlab](https://doc.comsol.com/5.4/doc/com.comsol.help.llmatlab/LiveLinkForMATLABUsersGuide.pdf)

## Functionality 
### Filepath Generation
- The subject ID is provided by the user (update 'Subj_ID')
- The root directory is obtained from the current working directory
- Using the Root and Subj_ID variables create the following paths: 'Path_Model', 'Path_Centerline', 'Path_Contacts', 'Path_Export', 'Path_Save', and 'Path_SelC'
- Verify that the centerline and contacts xml files exist

### Centerline Preprocessing
- Load the data in centerline.xml
- isolate the centerline x, y, and z coordinates to their own vectors



## Suggestions for improvement
- Change the subj_ID variable to be a prompt, in order to prevent the user forgetting update the subj_ID string
	- Line 4

## Code I don't understand
- ```Here, copy paste any code portions that you are unsure what it does``` 
	- Here, include the line number in the file to make it easy to find later
	- Feel free to also list any thoughts that you think may be relevant later when reviewing  the confusing code with the rest of the group

