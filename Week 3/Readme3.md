# Agenda for the fianl week: 2D detailing, equation based modelling(Optional but sexy af) and URDF export(The single most important part for robotics)

## 2D detailing: More relevant to static structures than dynamic ones
task -> [Video](https://drive.google.com/file/d/1We5Dfq0iGke2VxEqmmHYZOrWeleuKLqr/view) | [parts](https://drive.google.com/file/d/15ghnpdZrhDU1fAEQsWs3cG6FXM8hV-C_/view) 



[3D sketching](https://drive.google.com/file/d/1sQVgvV8ebp2VFXXjdR0Srl-PehuFyT7C/view)
<p align="center">
 <img  width="900" height="600" src="https://github.com/Robotics-Club-IIT-BHU/HDS-SummperCamp21/blob/main/media/2D-DETAILING-1024x534.jpg">
 <p align="center">
 <i></i><br> 
</p>

# URDF Exporter for SW

[Official Documentation](https://wiki.ros.org/sw_urdf_exporter/Tutorials/Export%20an%20Assembly) 
[Tutorial](https://www.youtube.com/watch?v=OSL-zqw4cXs) and [Next Tutorial](https://www.youtube.com/watch?v=IS3JIV45rh0)





[PDF](https://www.youtube.com/watch?v=Y-Y5jClGnbM) 


## IMPORTANT STEPS TO FOLLOW

Author - Tejas Rane.
##############################
- The steps and procedures mentioned in this document were executed in SolidWorks 2018 Professional Edition (SP5) with the sw2urdf plug-in. The author does not guarantee correct results with any other version of SolidWorks.
- The steps and procedures mentioned in this document are best suited for robots with "revolute" joints (rotational joints with constrained motion; min and max value of rotation). The author does not guarantee correct results with assemblies having any other types of joints.
- Go through the plug-in webpage properly before attempting to export to URDF. (http://wiki.ros.org/sw_urdf_exporter)
- The observations and solutions mentioned in the "Post Processing" section are only based on experience. The mentioned solutions may not work in all scenarios.
##############################

Pre-requisites-

1. Make all the sub assembly files that will form the final assembly. The only mates in the final assembly should be for defining the joints.
Eg- in case of revolute joints, the only mates in the final assembly should be axis (concentric) and surface (coincident).

2. The sub assembly files should be made with all the reference points for adding the Coordinate Systems. These changes can be made later as well, while actually assigning the Coordinate Systems. 

3. While making the sub assemblies, make sure that the parts are all aligned with respect to the origin of the assembly. This ensures that the STLs and meshes are exported properly. 

4. While making the final assembly, if some of the parts/sub assemblies are going to be repeated, make them independent part files.
Eg- instead of having 4 leg files from the same sub assembly (Leg<1>, Leg<2>, Leg<3>, Leg<4>), create independent sub assemblies as Leg_FL, Leg_FR, Leg_BL, Leg_BR. This can be easily done while making the final assembly. After inserting the component, right click and select "Make Independent" and save the component with a relevant name. This method is prefered over making individual component files, as changes made to the parent file, are reflected directly in all the child files made independent.

5. While making the final assembly, make sure that the Origin of the "base_link" coincides with the Origin of the assembly, which will eventually be the global origin for the URDF. Hence while making the "base_link", make it such that its Origin is in the desired place.

6. Make sure that the mass of the entire assembly, and that of the individual components is correct according to the actual system. If not, override the mass properties and define the desired mass values. 

##############################

While making the URDF-

1. Insert a Coordinate System at the Origin, and name it "Global_Origin" or "Robot_Origin".

2. Define all the other reference geometries (Axes and Coordinate Systems for all the joints). Give relevant names to the defined geometries which will be easily understood later on.

3. Make sure that the Coordinate Systems for the joints lie on the corresponding Axes. 

4. All Coordinate Systems should follow the same convention throughout the assembly. The universal convention is using the Right Hand Rule, with the X-Axis pointing along the forward direction of the robot, and the Z-Axis pointing vertically upwards.

5. The Coordinate System for a revolute joint should lie on the child link. Therefore when the joint rotates, the Coordinate System rotates with it. 

6. After all the Axes and Coordinate Systems are defined properly, open the plug-in by going to File->Export as URDF.

7. Define the parent-child sturcture properly, with relevant names for all the links and joints. 

8. Define all the Reference Coordinate Systems, Reference Axes, Joint Types, and the Global Origin Coordinate System manually. DO NOT leave any field on "Automatically Generate" or "Automatically Detect".

9. After the entire structure is porperly defined and verified, click on "Preview and Export".

10. In the "Configure Joint Properties" dialogue box, click on every joint and make sure that the parent link, child link, joint name, joint type, Coordinate System, Axis, and axis direction are correct. 
In case of revolute joints, defining the Lower Limit, Upper Limit, Effort and Velocity is a must. If not defined, the default values selected are 0, which means that the joint will not move.
Go through every joint to make sure none of the required values are taken as 0 by mistake.
After verifying for all joints, click on "Next".

11. In the "Configure Link Properties" dialogue box, the Mass and Moment of Inertia matirx of each link is often generated wrong. 
Here, the values for the Mass, and for the Moment of Inertia matrix (Ixx, Ixy, Ixz, Iyy, Iyz, Izz) must be entered manually, if the generated values are not as desired. All these values can be found in the mass properties for each component.
Go through every link to make sure none of the required values are taken as 0 by mistake.
After verifying for all links, click on "Export URDF and Meshes".

12. This will generate the entire URDF package in the selected folder.

##############################

Post Processing (Gazebo)- 

Before spawning the URDF in Gazebo, make sure that the path of the URDF file is defined correctly in the launch file. Add any other arguments (paused, debug, verbose, etc.) as well, if required.

After spawning-

1. If the entire model explodes into the sub assemblies, the Axes and Coordinate Systems are not defined properly.

2. If the entire model explodes, and the sub assemblies also explode into their respective components, there is a bug in the SolidWorks version used. Try to use only the versions which are mentioned on the plug-in webpage. 

3. If the entire model implodes to Origin after making contact with the surface (collision), the joint type defined is wrong (not as desired).

##############################

Following the above mentioned steps should give you correctly exported URDF in most of the cases. The author does not promise results in all cases and scenarios.



# URDF from fusion

## In our experience so far, fusion is more robust for URDF exporting and SW is a more makeshift 'jugaad'.


[A really lomba tutorial](https://www.youtube.com/watch?v=o7w7yv-Nros)

[Github for the plugin](https://github.com/syuntoku14/fusion2urdf)


# (Optional) Equation Modelling
[Link](https://youtu.be/VaU1U86rHSw) and [Link](https://youtu.be/wAjXADdo66k)
