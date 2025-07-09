<img src="https://github.com/CEINMS-RT/ceinmsrt-core-cpp/blob/main/logo-ceinms-rt-white-v.png" width="50%" alt="CEINMS-RT logo">

Here, you can find small explanation of all the included folders and files: 

NOTE: TO CHECK THE OUTPUT YOU MUST CAN REPROCESSED THE DATA USING THE FOLLOWING COMMAND:

path\to\bin\Win\Debug\CEINMS.exe -s path\to\lumbarModel_calibrated.xml -e path\to\\executionRT.xml -p path\to\Sample_data\squat5kg -r path\to\outputDirectory
Then, plot Torque.sto and compare to reference id.sto files. You will see the the model accurately predicts torque for the lifting phases (areas for which it was calibrated).
Areas for which the model was not calibrated experience torque underestimation (parts where the participant was standing).


Configuration files --> this folder contains all the necessary files to run the back model

- executionEMG.xml --> file specifying the maximum EMG values (typically found during Maximum Voluntary Contraction, MVC, recordings. These values are used to normalize the recorded EMGs. The values present
in this file are specific for the specific individual.

- executionIK.xml --> Some important parameters related to inverse kinematics are specified in this file:
	* numberOfThread --> number of threads used to compute inverse kinematics
	* maxError --> maximum error allowed for markers during the inverse kinematics optimization. 
	* OsimFile --> OpenSim model for which we want to perform inverse kinematics. 
	* LabFile --> file specifying lab-related aspects such as force plate rotations. Here, we can also specify external forces applied to the model such as hand forces. 
	* Fc --> cut-off frequency for the low pass filter used to filter inverse kinematics results (joint angles)
	* externalLoadsXml --> file giving information about the external forces applied to the model. 
	* ikTaskFilename --> file indicating the markers used to inverse kinematics (and their optimization weights). It is important that the markers (and the order in which they are listed) is exactly the same as in the OpenSim model and in Qualisys.

- executionRT.xml --> This file is given as argument (in the terminal) when using CEINMS. It specifies plugins (such as EMG, Xsens or RTOSIM) and configuration files (such as executionEMG.xml or executionIK.xml)
Additionally, in this file, we should indicate the identifier for the spline coefficient file. This is done under NameOfSubject label.

- ID_loadDefinition.xml --> see 'externalLoadsXml' above. 

- InverseKinematics.xml --> see 'ikTaskFilename' above. 

- lab_highWeight.xml --> see 'LabFile' above. The presented lumbar model was typically used for studies involving box-lifting tasks. In this file, it is possible to specify the following:
	* ID --> identified for the external force (e.g. r_hand)
	* weigth --> the weight of the lifted object
	* heightThreshold --> the is the Y-position (vertical) of a marker placed on the lifted box. As soon as the Y-position of the marker (specified under "markerForThreshold") was above the threshold
	the force was applied to the model. Otherwise, the box was at a resting position (not being lifted by the participant).
	* applyAtMarker --> in box-lifting experiments the forces are typically applied to the hand. In this case, the force was applied to the model at the position indicated by L2K or R2K (left or right 2nd knucle markers).

Geometry --> this folder contains all the geometry files required to use the back model.

CEINMS models --> this model contains 2 lumbar muscle models. A base uncalibrated model and a calibrated model.

OpenSim model --> folder containing 2 lumbar OpenSim models. A base unscaled model and a scaled model

Spline coefficients --> folder containing the spline coefficients used to compute muscle-tendon lenghts and moments arms for the lumbar model muscle-tendon units. The coefficients are for the specific participant of the present dataset.

Sample data --> folder containing the output files from CEINMS-RT. Specifically, we include inverse kinematic output, inverse dynamics and EMG-based lumbosacral moments, muscle forces and lumbosacral compression forces. 
Data is included for 4 different box-lifting recordings including 2 lifting techniques (squat and stoop) and 2 weights (5 and 15 kg). 

