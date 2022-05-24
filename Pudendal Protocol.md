# Pudendal Protocol
## Table of Contents
```toc
```

## Before you begin

1. Duplicate the “New Subject” folder in the “Subjects” folder and change its name to the name of the new subject (e.g. 1010).

**Critical: **Change “subject = _YourNewSubject” _ _before_ running any of the codes. This is the only line in all the codes that you need to change unless you are prompted by the code to correct some potential issues.  

**Note: **The codes look for specific files in specific folders. The existence of all these files and folders and checked in the beginning of most codes and you will receive error messages if the necessary files are not where they are expected to be. Hence, it is important to keep the organization of files and folders as intended.

**Note: **The “New Subject” folder includes all the empty subfolders that are necessary to run simulation and do the analysis. These subfolders will be populated with necessary files along the process.


## Segmentation

2. Use Mimics to start a new segmentation project for the MRI and save the project in:

_/Subjects/YourNewSubject/Segmentations_

**Note:** You can do the segmentation on any computer and then move the files where the analysis will be performed.

3. Segment the MRI images! 

**Note:** You can use MRI images to segment bones but I suggest to use CT images for that purpose. However, you **have to **segment pelvis using MRI images because we use it for coregistration. 

4. Use Mimics to start a new segmentation project for the CT and save the project in:

_/Subjects/YourNewSubject/Segmentations_

**Note: **You can do the segmentation on any computer and then move the files where the analysis will be performed.

5. Segment the CT images!

We segment all the bone structures (pelvis, sacrum, femurs), and foregin metal objects (electrodes and implants) using the CT images. 


## Co-registration

6. Make 3D objects for all the parts you have segmented using CT images. 

You can use the “Part” in the “Segmentation” tab to create parts or click on the cube shape in the bottom of the mask panel. Use the **high** quality preset in the Calculate Part window ([Figure 1](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.72h5mzr4w53e)). 

**Critical:** Make sure to use the boolean operation (segmentation tab) to unite the masks for the left and right side of the pelvis in case you segment them separately (as I do). This is necessary in the co-registration step (step 9).

**Note: **You do not need to perform any smoothing or other post-processing on the parts at this point. Yet, all the parts except for the electrodes should already look good if you have done a good job segmenting ([Figure 1](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.72h5mzr4w53e)). 

![](https://lh3.googleusercontent.com/uYZCS3LuwAb9SlUp-p4zPUsZ2gfaezcHFJIPwm2FpHM9APL4QnqjpjdbNWMcmiMzRBQDWPcTGEpNCN1tLXDpmwpK5tk1YJ8l5Jkk5qoyYhvLOeiEa19FXd1UM8cr4MFBGTXAv5MQ)


###### Figure 1

7. Copy all the 3D objects from the CT project to the MRI segmentation project. You can do this by simply selecting them in the Objects panel ([Figure 2](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.6hqkahncheup)), right clicking on them and then choosing “copy”. Then you go to the MRI project and press Ctrl+V to paste (for Windows OS).

![](https://lh4.googleusercontent.com/KO5qaC330PFsrQKlIVu3Bgm7zkI38rKYnmFCY8t_w18CCTJSONr3jyueEr45kaYCRK5N2ki7znv0v7Hnnr_3uNDY_rw3BIvNeS3QRt7Lk6ECc0hob7jhT6atHPLAuysmU3AEHX-3)


###### Figure 2

**Note: **I recommend adding CT to the beginning of all the copied objects to know their source. 

**Note: **You can potentially have a single project for segmentation and have two sets of images (MRI and CT) or more. And switch between the image types and do segmentation. However, I prefer to keep two separate projects of MRI and CT. 

**Note: **The objects that you are moving from the CT project are: pelvis, sacrum, femurs, contact0 (closest contact to the tip), contact1, contact2, contact3, the electrode wire, and potential metallic foreign objects (e.g. hip implants). I suggest using these names for the objects especially for the contacts. You can potentially segment and create an object for the IPG.

**Note: **I use Dynamic Grow Region to segment the contacts. 

8. Use the MRI segmentation to create a 3D part for the pelvis.

**Note: **If you are not sure how to do this step, check step 6 and its note and follow the same procedure (no smoothing and high quality preset to calculate parts).

9. Use the pelvis from CT and the pelvis from MRI to co-register the electrode and other parts (sacrum and femurs and potential implants).

Use Inertia Axis Algin from Algin tab. Select the MRI pelvis for the Fixed Part. Select the CT pelvis for the Moving Part. Select other CT objects as Move Along objects. Finally, click Align ([Figure 3](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.4bn6pq3ot02u)). 

![](https://lh5.googleusercontent.com/KpSe7-Dk-h1Y_ty3Sc5R28BrO_32G-EZGHPh0u6vsPoyckNmQ3vlyTyo6iZfKT-ZFxNrlpbdQr6Fw34QM-tdVnd7YpqNPEkNkasMZMNfKT2P_hfllDfj8VV2bEyhMD1sumhuhDzW)


###### Figure 3

## Nerve reconstruction -- Simvascular
10. From Mimics, export the subjects MRI as dicom files with the pudendal nerve mask included
	*TODO: Describe how to *
1. Open simvascular and create a project

## Electrode reconstruction
10. Use 3-matic to create a new project and save it in:

_/Subjects/YourNewSubject/Segmentations_

11. Copy the co-registered contacts and wire (step 9) and paste them in the new 3-matic project. 


12. From the Design tab, then Create Analytical Primitive, select Create Point. For Method, use Fit center of gravity. For Fitting entity, go through each contact and click Apply ([Figure 4](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.dh2vm99doqwl)). This process creates a point at the center of gravity of each contact.

**Note: **I suggest hiding the 3D objects for each contact after you create the points for each contact. To do so, right click on each contact in the Object Tree and then select Hide.

![](https://lh6.googleusercontent.com/K0oZ0oGHsyITUmSv6SXrcNq-gAYzcRCoZ7wGzYlyws757naMCRHfZPCgmihfzHGiOlo3bZxeCzTW8FaFVmchQdgCNDtn9RCpBEAalxZxNk62Lp0Xl3dxJIg-A6b8FYZuGsfZRlKp)


###### Figure 4

13. From the Curve tab, select Create Center Line. For entity, select Wire. Use 0.5 for Segment length and detail. Click Apply ([Figure 5](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.sf0xilqj233i)). This process creates a centerline of the wire. 

**Critical: **It is possible that the centerline consists of more than one curve (mostly the case if the segmented wire is long). You can expand the centerline in the object tree to check if there are more than one curve. In such cases, use Connect Curves from the Curve tab to connect the curves so that you end up with a single curve in the end. It is also possible to get small loops that need to be deleted. All in all, make sure that the centerline is a single curve that makes sense to you based on the 3D structure of the wire. 

![](https://lh5.googleusercontent.com/nPcFEHH8TI4-R2RlCQJiRCIVFyO2area9K5X8sbAaJ-vUFBaOjgrHk1SpyIk-CzGzJDpC8jDF4BRL1IhCtXzIHOglwK5aWYlr2N4h5OMdwsIMV8kDwbbh1zSKS67NeSDGLUKsRyN)


###### Figure 5

14. Expand the Wire in the Object Tree and create a new part from the Centerline ([Figure 6](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.j3nojt94ngqv)).

**Note: **You may now hide the 3D wire for easy navigation and visualization.

![](https://lh5.googleusercontent.com/hi0nIbMMX2rhPbAp67TpQmiZpl54tDfBBopA5ok7sd66Km4abQXJ6sDJ2wOYH50aqZ-kMseiwxHuwuA_xr4ZVpqv7EEegvQXB8MCsH7Fqk187EmBRDkK8ssHxLbgif-_Xe32B6NA)


###### Figure 6

15. Use Extend Curve from the Curve tab to connect the end of the center line to the center of gravity of Contact3 ([Figure 7](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.s0wbch7ajjtc)). 

![](https://lh5.googleusercontent.com/jFszcppTr2UUiPwWAHQIwPulclufZ10xH6unP3mpcIlFW4ftAnkkbxoJs0YmAxlOYpk7BdZo3r3td05zG_G2W_EMb0BD8OcZXR4zeM1WU3X7AaLATxBWGSFNbL6QuXzpf_iPP7VS)


###### Figure 7

16. Smooth the curve from step 15. Use Smoothing factor of 0.25, and number of iterations as 5 ([Figure 8](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.fm92nba0su62)).

**Note: **Reduced smoothing factor if the smoothed curve looks jagged. You should not face such issues if you use the suggested values. 

![](https://lh3.googleusercontent.com/_XlkR5niJsRGlED4BUfJnh8lQ8nQ9c6YQ2zBt4iqdTFMVXuKb1vzALrcZ0Jds2qeqEvu7TNbQAmKpaxbTCbzgtVSvKDXiGtehl4x2orWCCgu3hbl29ugPkwNqRpuO_VPBbY5jkZ0)


###### Figure 8

17. Similar to step 15, extend the curve by connecting it to the other contacts. 


18. Enlarge the curve from step 17 from Contact0 side. For Method, use Tangent to the last segment. Set Length of free curve 0.0 for Begin point and 3.0 for End point ([Figure 9](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.oc91omafji40)). This extension will be used in _Electrode.m _to create the tip of the electrode. 

**Critical: **Make sure that the curve is enlarged from Contact0. If not, you need to change the values of Begin point and End point. 

**Note: **Contact0 is the contact closest to the tip and Contact3 is the contact furthest from the tip. 

\-![](https://lh3.googleusercontent.com/n3BvSmVK48a1BaKg3fbNDGcyqJQv4Ue14gAApPhQDHh2IdBY6im0Yacp8mMEUKu-a5SqikF0fO-gq0rVelYb6-yXhbegH3fZ0HMJN7U-Hy_Qp2aN3QbzWj9to6ABhsta4FnZxB_t)


###### Figure 9

19. Smooth the final curve once more by setting Smoothing factor of as 0.2, and number of iterations as 1.


20. Save the project (I name it Electrode). 


21. Export the final curve as an **xml** file and make sure to export the file in the **Segmentation** folder and name the file **Centerline** ([Figure 10](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.jz8nswimtciw)).

![](https://lh6.googleusercontent.com/dHDDM-SD7MBZnpCjk2PvApr9_y0fG_VyzTNAa7iI7rnS2H8r4H6kk4ck1GD2u_Pf7iR_YhRNzsSw3dqPW5O5Gri1mRuq1RZZaqhOKR_wKdc_9x8YmGBZFOQ56dqyJ6YucEUOS1-m)


###### Figure 10

22. Export all the center points of contacts in a single as an .**xml **file and make sure to export the file in the **Segmentation** folder and name the file **Contacts.**

**Critical: **The order of contacts in the exported file is important and has to be contact0, contact1, contact2, and contact3.

23.  Navigate to the Python folder and run _[[Read_XML.py]] _ after changing the Subject variable to the current subject in the script. 

This code reads the xml file and extracts the required information to construct the electrode. 

24. Open COMSOL with MATLAB.


25. Navigate to the MATLAB folder and run  _[[Electrode.m]] _ after changing the Subject variable in the script to the current subject. This code creates the electrode geometry and the contacts. 

**Note: **The result is saved at  _/Subjects/YourNewSubject/FEM/Electrode.mph _ and you should open it to make sure it looks good ([Figure 11](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.bqaxpbg87txc))

![](https://lh6.googleusercontent.com/5RuCPoTOIgltEj3qNZCOK2XB0ECRpTHCumuxgnpjKwyO2AgIU2bQwrYqhwp-J0NN9QOQIHwgDmPNGZuW23W9wcrz7FDGTMxkFZc0bftqwv_OHq3See7znXPSaDP2xb-splo0_E9Q)


###### Figure 11

**Troubleshooting: **You might receive an error after running _Electrode.m _that says:

'Something is wrong. You may want to flip the order of points in the python code.'

In that case, go to _Read_XML.py _ and comment/uncomment the line that says 

Points=np.flip(Points,axis=0)

This issue arises because of what I have explained in the critical part of step 18.


## 3D parts

26. Open the co-registered MRI project in Mimics.


27. Build 3D parts for all the segmented parts (follow the same procedure as step 6). 


28. Smooth (located in 3D Tools tab) all the large parts (pelvis, bladder, large muscles etc.) using 100 iterations and smoothing factor of 0.25. Also, no need to turn on “compensate shrinkage”. 

**Note: ** You may have to smooth the exterior (body) more aggressively (repeating step 28 and even step 29) to avoid issues during constructing the geometry in COMSOL. 

29. Wrap (located in 3D Tools tab) all the small parts (nerves and veins) using 1mm for the smallest details and 0.5 for closing gaps. Also, have Dilate results turned on. 


30. Smooth the wrapped objects using the same setting as step 28 but have “compensate shrinkage” turned **on**.


31. Use 3-matic to create a new project and save it in:

_/Subjects/YourNewSubject/Segmentations_

32. Copy all the 3D objects from Mimics and paste them in the new 3-matic project (see step 7 and [Figure 2](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.6hqkahncheup)). 


33. Remove Spikes (Fix tab) for all the parts using Spike size as 1.0, smallest detail as 1 and Preserve surface structure on.


34. Run Fix Wizard (Fix tab) for all the parts to make sure there are not any issues with any of the parts. 


35. Improve Mesh (Fix tab) for all the small parts (e.g nerves) by setting maximum geometrical error as 0.05 and maximal edge length as 0.5. Shape quality set to high.


36. Improve Mesh (Fix tab) for all the large parts (e.g pelvis) by setting maximum geometrical error as 0.05 and maximal edge length as 2.5. Shape quality set to high.


37. Export all the files as STL and ASCII to _/Subjects/YourNewSubject/STLs_

**Critical: **Make sure you are following the [name convention](https://docs.google.com/document/u/0/d/1MkUwdI0cnqnPp6CfRu0ZwqJ3u2gOTcVO9DkWAD-tnXw/edit) provided. You may call the masks whatever you want during segmenting and other steps. However, the final names need to be specific so that the codes can find them. The codes do **not **stop if they cannot find a part because some might not actually exist (most patients do not have implants or male patients do not have uterus), but you will be prompted by my codes that some parts were not found to make sure something that needed to exist is not missing. 


## Meshing and material assignment

38. Open COMSOL with MATLAB.


39. Navigate to MATLAB folder and run _[[Geometry.m]] _ after changing the Subject to the current subject. This code creates the geometry for the model. 

**Note: **The result is saved at _/Subjects/YourNewSubject/FEM/Geometry.mph _and you should open it to make sure it looks good ([Figure 12](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.t8s4cjti5ycz))

![](https://lh3.googleusercontent.com/3o92fGrDN7cHvsMzteiyME5QtgDXmDXA-nJEpl9v8w6wg61HSDXoV3cJMYtTqoG1nMtflgv7JsP_KLkaavzeGlacDj6xzMJMMMRa_Ro3FdjVwYl7XvfPQPkkNwV70Fe_ts0AQMdR)


###### Figure 12

**Troubleshooting: **You may have to smooth the body more if COMSOL fails to create the geometry. Also check if electrode & nerve geometry overlap.

40. Navigate to MATLAB folder and run _[[Mesh.m]] _ after changing the Subject to the current subject. This code creates the mesh and the files necessary for material assignment. The code refines the mesh multiple times and the final mesh and its corresponding conductivity will be used. 

**Note: ** The meshes are saved at _/Subjects/YourNewSubject/FEM/Meshes_

**Note: ** The conductivities are saved at** **_/Subjects/YourNewSubject/FEM/Sigmas_

**Note: ** There are visualization files for conductivity values located in_/Subjects/YourNewSubject/FEM/Sigmas _with .vtu extension that can be opened by Paraview.

**Note: ** The meshing and material assignment is a time consuming process and can take about an hour. 

**Troubleshooting: ** You may have to change mesh resolution for the nerve (or other parts) if COMSOL fails to create the mesh.** **However, if the initial mesh is generated without any issues, the refinement process will carry out with no problem. Check _Mesh.m _to find where you can modify the mesh resolution.


## FEM solution

41.  Open COMSOL with MATLAB.


42. Navigate to MATLAB folder and run  _[[PreSolution.m]] _ after changing the Subject to the current subject. This code creates the model that will be run to generate the voltage distributions.


43. Navigate to MATLAB folder and run  _[[Run.m]] _ after changing the Subject to the current subject. This code runs the model for all the monopolar and bipolar configurations and saves the files in  

_/Subjects/YourNewSubject/FEM/Solutions_

**Note: **There are visualization files for voltages located in _/Subjects/YourNewSubject/FEM/Solutions _with .vtu extension that can be opened by Paraview.

**Note: **This is a time consuming process and solving each electrode configuration can take 15-30 minutes. You may remove some of the configuration that you do not need by modifying  _Run.m _ code.


## Axon Trajectories

44. Open the STL file of the nerve you exported in step 37 in Paraview.


45. Press “g” on the keyboard and drag a box around the tip of the perineal branch ([Figure 13](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.bzts9ynxjqjd)).

**Critical: **We do this step to find coordinates of the center of the branch. Therefore, it is important to make sure the selection in step 45 only includes the points of the deserted branch and not other parts of the nerve as this method of (pressing “g”) selects through the stl file. You may have to rotate the nerve to get a good view that allows you to make a selection such as the one shown in [Figure 13](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.bzts9ynxjqjd)**.  **


###### Figure 13

46. Right click on the Nerve in the Pipeline Browser. Go to Add Filter. Go to Alphabetical and select Extract Selection ([Figure 14](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.mofiprphg09e)).

![](https://lh4.googleusercontent.com/Wox7LZX1yYf1IKG0FNd3_JUQ6RBYprg-w60SyHVJlwLqmNN2VGDTAC6y6hunfqBJsYpV0cCEqze7Y9UdgTZBH8MJZlKgc1hO5DIa09Gm9b1pwU2lmC7J2BeW4B54bj3W-N0zBrx0)


###### Figure 14

47. Rename the selection to “P0” in the pipeline. 


48. Create a selection for the perineal branch right before it joins the other branches and name it P1 (step 43- 47) as shown in [Figure 15](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.skw2bpyfcdgp).

![](https://lh3.googleusercontent.com/tWBpaCS2-5HdKDy7ugxIIbqVjaY1b2t2X9NfJWw6YZeGmPsllG9VgOAqsLn9-l9muLLiUDieQJBN5Vtd19l5_APnf_-6cIE23eeerH59vQUQN1S5Ft6bzNQwnKqWkPO9Z8FyWOlS)


###### Figure 15

49. Repeat these steps for the rectal and gential branches and create R0, R1, G0 and G1 selections. 


50. Repeat these steps for S2, S3, S4 for branches and name them S2, S3 and S4.


51. Create a selection for the main branch and call it M0 (refer to [Figure 16](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.qys2wlttabnl) for an example of where all these selections are).


###### Figure 16

52. Navigate to the Python folder and open  _[[ExportData.py]]_ code. Change the subject name to the current subject name and save. Also change the path according to which nerve (left or right) is of interest.


53. Go to View and open a Python Shell. Then go to Run Script and open _ExportData.py _code that we modified in step 52 ([Figure 17](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.sbxfrugxy5v4)). This python code runs in paraview and creates the center point of the selections we created in the previous steps.

![](https://lh6.googleusercontent.com/tdOKDSVK-sa5WWvE33t65vUMF_4x8-c49FNwahyxD4mKEju6SOGdaG5_eLUS4H-Yr18PFbb-6IgBe7_1h72_riF6Hz-cQcGA04amR4KjO0yZ9KscM4ZfyfEB6iK6d62cl4nt1rd4)


###### Figure 17

54. Navigate to the Python folder and run _Centerlines.py_ code after changing the subject to the current subject. Also change Path2 and surfaceReader.InputFileName based on whether it is the left or right nerve. This code creates centerlines that connect the center of points we defined in the previous steps. 

**Critical: **This code requires the [vmtk](http://www.vmtk.org/) package, which is not a standard Python package. I recommend following their installation [guide ](http://www.vmtk.org/download/)and installing the package in a new environment.This package uses an older version of numpy and that is one of the reasons why I recommend installing it in a separate environment.

**Note: **The results of running this code is saved at:

_\\Subjects\\YourNewSubject\\Trajectories\\Left\\Centerlines_

Or 

_\\Subjects\\YourNewSubject\\Trajectories\\Right\\Centerlines_

Depending on which nerve (left or right) you are working with. The centerline coordinates are saved at the .txt files but they are also saved as .vtk files that you can open in Paraview for visual inspection ([Figure 18](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.rzpnw04zkb5))

![](https://lh5.googleusercontent.com/ZPcjhBwAkch9tfmKwV6kAZIyHFCHmbzV83SRUuSOpF3z-EpAiuPMSD9JfXh_40DWEg1mChBJ3sgMrJSo7Ou4gy7nuxf0GJIHALbvER-i5I6u89DN-fXev7MwSsVLq0YFNUhKi-Ry)


###### Figure 18

55. Navigate to the Python folder and open _GuideCreator.py_ and change the subject to the current subject. There are other parameters that you need to change in this code before running it. 
56. You have to decide where to put the guides in the main branch for the perineal, rectal and genital axons. The guides are points that the trajectories have to pass through them. Technically, you can have only to guide points (seed and targets). However, if we want to force trajectories to populate a specific side part of the nerve (e.g. lateral), then having guides is necessary. 

There are several ways of doing this and you can learn more about them by looking at the _FindGuides _function. 

Right now, we are assuming that the perineal axons are populated in the middle of the nerve [(Figure 19)](https://docs.google.com/document/d/1dW4wiqABN6PR1X6uNr-PSv6VEQMVTfmk5EJmJhHy1Fg/edit##heading=h.j60j4yg8yb3). So, you don’t need to pass any extra argument to _FindGuides _function.

However, the rectal branch is assumed to be towards the lateral side and the genital branch is assumed to be towards the medial side. Therefore, you need to provide extra arguments for the _FindGuides _to populate the guides accordingly. 

The easiest way would be by passing Direction=\[i_hat,j_hat,k_hat] to the _FindGuides _function, where i_hat,j_hat,k_hat are unit vectors that point toward the medial and lateral sides. You can use Mimics or Paraview to figure out these vectors. However most of the time Direction=\[-1,0,0] points toward the medial side and Direction=\[+1,0,0] points towards the lateral side for a left nerve (it would be opposite for the right nerve). However it is **critical **to check these and update the code.

**Note: **The results of running this code is saved at:

_\\Subjects\\1005\\Trajectories\\Left\\Guides_

Or 

_\\Subjects\\1005\\Trajectories\\Right\\Guides_

Depending on which nerve (left or right) you are working with.

  


![](https://lh4.googleusercontent.com/CsUovaCbNTY04a1Uf72JUERb6xWk4CHz3BBa27GoH-_7FRLnq8oIrBBlYBU1cHb6Evj550C06ec8lCmL7LsQ7uAsoahZ2tsFoKipC4Owz_wH608yTMBiERDnnSqHw4yfzPYsCsnF)


###### Figure 19

57. Navigate to the Python folder and run _LoopMultiCenter.py_ code after changing the subject to the current subject. This code creates the axon trajectories for all the branches.

**Note: **This can be a time consuming process especially if you increase NPaths, which is the number of trajectories.

**Note: **The code might fail to populate the nerve if you add too many axons. Check the comments in the code for more information.

**Note: **The results of running this code is saved at:

_\\Subjects\\YourNewSubject\\Trajectories\\Left\\Paths_

Or 

_\\Subjects\\YourNewSubject\\Trajectories\\Right\\Paths_

Depending on which nerve (left or right) you are working with.


## NEURON Simulations

58. Navigate to the Python folder and run _ExportCoordinates.py_ code after changing the subject to the current subject. This code exports all the compartment coordinates for the axon trajectories we created in step 57.

**Critical: **Make sure that you have functioning neuron installation because _ExportCoordinates.py requires _NEURON

**Critical: **Make sure to change the Diameter variable in the code if you want to export the coordinates for axons of a specific diameter. 

**Note: **The results of running this code is saved at:

_\\Subjects\\YourNewSubject\\Trajectories\\Left\\Comps_

Or 

_\\Subjects\\YourNewSubject\\Trajectories\\Right\\Comps_

Depending on which nerve (left or right) you are working with.

59. Open COMSOL with MATLAB.


60. Navigate to the MATLAB folder and run _ExportV.m _after changing the subject to the current subject and changing ‘Path2’ & ‘Path3’ to match the appropriate nerve (left or right). This code opens the COMSOL solutions we found in step 43. Then it uses the compartment locations in step 58 and calculates the voltages at them.

**Note:** The results are saved at

_\\Subjects\\YourNewSubject\\Trajectories\\Left\\Voltages_

Or 

_\\Subjects\\YourNewSubject\\Trajectories\\Right\\Voltages_

Depending on which nerve (left or right) you are working with.

**Note: **This code also saves voltages as .vtu files for visualization in Paraview. The results are saved at _/Subjects/YourNewSubject/FEM/Solutions_

**Note: **Change the solutions you want to export voltages for if you did not solve for all configurations in Step 58.

**Note: **This code also calculates the integral of currents at each contact (used to calculate impedance and convert current threshold to voltage thresholds) as in a file called _Integrals.txt _where the voltages are exported. The same file also includes the contact area so that you can make sure the electrode construction is decent. 

**Note: **This is a time consuming process.** **

61. Navigate to the Python folder and run _CommandThresholdCalculation.py_ after setting the subject and configuration and the branches you want to check. 

**Critical: **This code requires a functional NEURON installation.

**Note: **Make sure that the diameter is the same as what you used to export the compartments coordinates. Otherwise, you will receive an error. 

**Note: **You will have to modify the pulse at some point!


## Batch NEURON simulations

It is better to do threshold calculations on the Great Lakes cluster. To that end:

1. Upload the voltages folder and Paths folder to your directory on the Great Lakes cluster. 


2. Upload the NEURON folder to your directory.


3. Use _HPC_Threshold.py _to calculate the thresholds.

**Note: **You can use _Slurm_Writer.py _to write slurm commands to run the code. However, make sure to make proper adjustments when you use this code. Otherwise, you will be sending emails to me when you run your codes!!! And will try to save your files to my directory!
