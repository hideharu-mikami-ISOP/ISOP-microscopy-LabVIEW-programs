# ISOP-microscopy-LabVIEW-programs
LabVIEW programs for ISOP microscopy image acquisition, volumetric image reconstruction, and a part of analysis

Instructions for LabVIEW Files
List of LabVIEW Shortcuts
1.	ISOP camera console
2.	ISOP creation of simulated low-speed images
3.	ISOP galvo calibration
4.	ISOP image calibration and reconstruction
5.	ISOP microscope control console
6.	ISOP PSF analysis-1
7.	ISOP PSF analysis-2
8.	ISOP recording of real-time waveforms for dynamic calibration
9.	ISOP regression curve generation for dynamic calibration
10.	ISOP PSF numerical simulation
________________________________________
Prerequisites
1.	Prepare workstations with Windows OS (image acquisition was validated on Windows 10).
2.	Set up a local network to allow workstation communication via TCP/IP or UDP.
3.	Install LabVIEW (64-bit, 2024 Q3 or later) on the control machine. The Vision Development Module, NI-DAQmx, and NI-VISA are required.
4.	Prepare and connect the experimental setup properly (see Methods, Extended Data Fig. 1, Supplementary Fig. 6, and Supplementary Table 1).
5.	Install drivers for the AWG, cameras, function generators, and USB oscilloscope. When each VI is opened for the first time, verify that the required VIs and DLLs related to the drivers are properly referenced.
________________________________________
Image Acquisition Workflow

Step 1

•	Launch ISOP microscope control console.

•	Launch ISOP galvo calibration.

•	Adjust G1 and G2 waveforms by changing parameters on Launch ISOP microscope control console.

•	Outcome: finalized G1 calibration and coarse G2 calibration.

Step 2

•	Launch ISOP camera console on two machines in calibration mode. Select Master/Slave before launching. If using a single machine, launch Master only and enable “One PC.”

•	Perform manual adjustments:

o	Stop G1, monitor fluorescence images of beads, and manually adjust G2 and OL3 xyz position.

o	Adjust Y-offset of the camera ROI.

o	Adjust Y scanning range (AOD bandwidth).

o	Align relative positions of the two color channels.

•	Acquire calibration images of 10-µm fluorescent beads.

•	For dynamic calibration:

o	Launch ISOP recording of real-time waveforms for dynamic calibration in advance to record synchronized waveforms and images.

o	Enable the “calib” button during image acquisition.

•	Outcome: finalized G2 calibration, AWG adjustment, and camera calibration.

Step 3

•	Use ISOP image calibration and reconstruction to perform image calibration (slice extraction parameters).

•	For dynamic calibration:

o	Enable “calib using picoscope.”

o	Use ISOP regression curve generation for dynamic calibration to obtain and save regression curves.

•	Outcome: finalized slice extraction parameters for subsequent image reconstruction.

Step 4

•	Relaunch ISOP camera console in monitoring mode.

•	Adjust overlay alignment between bright-field and fluorescence images.

•	Adjust relative position between bright-field tracking image and fluorescence image.

•	Mount the experimental sample, monitor a central frame of the volume, adjust z-position, and adjust excitation laser power if needed.

•	Switch to recording mode (REC) to acquire experimental volumetric data with time stamps.

•	On a separate machine, acquire and save bright-field tracking images, tracking positions, and time stamps.

•	For dynamic calibration: launch ISOP recording of real-time waveforms for dynamic calibration in advance.

•	Outcome: finalized alignment of monitoring/tracking images and storage of raw imaging data.

Step 5

•	Open acquired image frames with ISOP image calibration and reconstruction.

•	Reconstruct 3D images and adjust:

o	Relative positions of two color channels.

o	Slice extraction parameters.

o	Color scale (if saving videos).

•	Continue experimental imaging with adjusted parameters.

•	After experiments, save adjustment parameters and reconstruction data.

•	Outcome: finalized 3D fluorescence image data for analysis.

________________________________________
Generating Simulated Low-Speed Images

•	Prepare volumetric image data (*.3DU16).

•	Use ISOP creation of simulated low-speed images to generate and save simulated image files (*.3DU16).

________________________________________
PSF Data Analysis

1.	Load volumetric image data (*.3DU16) of 200-nm fluorescent beads using ISOP PSF analysis-1. Manually select individual bead images and save.
2.	Preview the saved data using ISOP PSF analysis-2.
   
________________________________________
Numerical Simulation of PSF

•	Use ISOP PSF numerical simulation with specified parameters (NA, immersion medium, wavelength, etc.).

________________________________________
Format of *.3DU16 Files (binary format for reconstructed volumetric image data)

•	1D array (3 elements, double): voxel size in z, y, x [µm].

•	1D array (5 elements, 32-bit signed int): number of volumes, number of channels, voxels in x, y, z.

•	4D array of voxel counts at t = 0 (16-bit unsigned int): [channel, z, y, x].

•	4D arrays at subsequent time points (t = 1 … n): same index order.

Array format: (num elements of 1st dim, 32-bit unsigned int) (num elements of 2nd dim, 32-bit unsigned int) … (num elements of nth dim, 32-bit unsigned int) (element 000) (element 001) … (element m1m2…mn).

