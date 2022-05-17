# Read_XML.py
## What is this script for?
The main function of this script is to read parse XML files for point coordinates and save these in a '.txt' file. Specifically, this script takes two XML files, 'Centerline.xml' and 'Contacts.xml', which describe the centerline of the electrode lead and the electrode contact centroids, respectively. It then parses the files for x, y, z coordinates which it saves in the files 'ExtractCenterline.txt' and 'ExtractContacts.txt' files. These text files are then used during the [[Pudendal Protocol#Electrode reconstruction|electrode reconstruction]].

*Note:* The variable *Path0*, which stores the path to the 'Subjects' folder is hard coded, and must be changed if the script is gonna be ran on another computer.

## Dependencies
- None

## Functionality 
### Parse *Centerline.xml*
- Store the subject ID passed by the function caller via the CLI
- Open the 'Centerline.xml' file using the [io](https://docs.python.org/3/library/io.html) python module
- Isolate the coordinates portion of the file and split the point coordinates by taking advantage of the '< Point >' xml tag
- For each point parsed:
	- store the coordinates in a python list with this format: [x, y, z]
	- Append the list of coordinates to a list-of-lists called 'Points'
-Save the 'Points' list as a text file using the *[np.savetxt()](https://numpy.org/doc/stable/reference/generated/numpy.savetxt.html)* function

### Parse *Contacts.xml*
- Open the 'Contacts.xml' file using the [io](https://docs.python.org/3/library/io.html) python module
- Isolate the coordinates portion of the file and split the point coordinates by taking advantage of the '< Point >' xml tag
- For each point parsed:
	- store the coordinates in a python list with this format: [x, y, z]
	- Append the list of coordinates to a list-of-lists called 'Points'
-Save the 'Points' list as a text file using the *[np.savetxt()](https://numpy.org/doc/stable/reference/generated/numpy.savetxt.html)* function

## Suggestions for improvement
- Consider encapsulating code in functions and creating a _ _ Main _ _() method
- Check if it is possible to export as .txt or .csv from 3matic, so that this script is not needed.

