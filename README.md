# SFND-Term1-P4-Radar-Target-Generation-and-Detection
Project 4 of Udacity Sensor Fusion Nanodegree  
Project Layout  
<img src="images/Project_Layout.png" width="1359" height="772" />
Radar System Requirements  
<img src="images/Radar_System_Requirements.png" width="829" height="226" />

## Overview  
In this project, you will implemented a CFAR processing script to measure the distance and velocity of the target and display the target in a simulated environment. You will be using the MATLAB to performat the sensor target simulation. Then you will evaluate the performance of CFAR processing by displaying the output figures.  This project consists of four parts:  

* First, you will configure the FMCW waveform based on the system requirements.
* Then, you will define the range and velocity of target and simulate its displacement. In the same simulation loop, you will proces sthe transmit and receive signal to determine the beat signal
* Next, you will perform range of FFT on the received signal to determine the range.
* Finally, we will performa the CFAR processing on the output of second FFT to display the target

## Prerequisites/Dependencies  
Matlab Download
To complete the project, you will need to download MATLAB on your computer, if you haven't already. To get started, you can follow these steps:

1. If you do not already have a MathWorks account, create one [here](https://www.mathworks.com/mwaccount/register). Be sure to verify your email (check your Junk/Spam folders) before moving on to step 2.
2. Download the installer here.
3. Run the installer – it will guide you through the steps for your OS.

## (TODO)Project Description  
.
├── images
│   ├── Project_Layout.png
│   └── Radar_System_Requirements.png
├── LICENSE
├── README.md
├── results
│   ├── 1st_FFT_Result.jpg
│   ├── 2D_CFAR_Range_Doppler_Map_Result.jpg
│   └── 2D_FFT_Range_Doppler_Result.jpg
└── src
    └── radar_target_generation_and_detection.m

## Run the project  
* Clone this repository  
```
git clone https://github.com/jinchaolu/SFND-Term1-P4-Radar-Target-Generation-and-Detection.git
```
* Start your MATLAB
* Navigate to the `SFND-Term1-P4-Radar-Target-Generation-and-Detection/src` folder  
* Open the `radar_target_generation_and_detection.m`  
* Click `Run` button or press `F5` on the keyboard to run the script

## Tips  
N/A  

## Code Style  
N/A  

## Project Rubric  
### 1. FMCW Waveform Design  
#### 1.1 Using the given system requirements, design a FMCW waveform. Find its Bandwidth (B), chirp time (Tchirp) and slope of the chirp.  
The FMCW waveform is designed here [radar_target_generation_and_detection.m (Line 33-35)](./src/radar_target_generation_and_detection.m#L33-L35).  

### 2. Simulation Loop  
#### 2.1 Simulate Target movement and calculate the beat or mixed signal for every timestamp.  
Target movement simulation is implemented here [radar_target_generation_and_detection.m (Line 71)](./src/radar_target_generation_and_detection.m#L71).  

The beat or mixed signal calculation for every timestamp is implemented here [radar_target_generation_and_detection.m (Line 66-88)](./src/radar_target_generation_and_detection.m#L66-L88).  

### 3. Range FFT (1st FFT)  
#### 3.1 Implement the Range FFT on the Beat or Mixed Signal and plot the result.  
The Range FFT on the Beat or Mixed Signal is implemented here [radar_target_generation_and_detection.m (Line 93-110)](./src/radar_target_generation_and_detection.m#L93-L110).  

The result plot is implemented here [radar_target_generation_and_detection.m (Line 112-121)](./src/radar_target_generation_and_detection.m#L112-L121).  

### 4. 2D CFAR  
#### 4.1 Implement the 2D CFAR process on the output of 2D FFT operation, i.e the Range Doppler Map.  
The 2D CFAR process on the output of 2D FFT operation is implemented here [radar_target_generation_and_detection.m (Line 131-245)](./src/radar_target_generation_and_detection.m#L131-L245).  

#### 4.2 Create a CFAR README File  
Done. You are reading it.  

* Implementation steps for the 2D CFAR process.  
1. Determine the number of Training cells for each dimension Tr and Td. Similarly, pick the number of guard cells Gr and Gd.  
2. Slide the Cell Under Test (CUT) across the complete cell matrix  
3. Select the grid that includes the training, guard and test cells. Grid Size = (2Tr+2Gr+1)(2Td+2Gd+1).  
4. The total number of cells in the guard region and cell under test. (2Gr+1)(2Gd+1).  
5. This gives the Training Cells : (2Tr+2Gr+1)(2Td+2Gd+1) - (2Gr+1)(2Gd+1)  
6. Measure and average the noise across all the training cells. This gives the threshold  
7. Add the offset (if in signal strength in dB) to the threshold to keep the false alarm to the minimum.  
8. Determine the signal level at the Cell Under Test.  
9. If the CUT signal level is greater than the Threshold, assign a value of 1, else equate it to zero.  
10. Since the cell under test are not located at the edges, due to the training cells occupying the edges, we suppress the edges to zero. Any cell value that is neither 1 nor a 0, assign it a zero.  

* Selection of Training, Guard cells and offset.  
The number of training cells is defined here [radar_target_generation_and_detection.m (Line 158-161)](./src/radar_target_generation_and_detection.m#L158-L161).  
The number of guard cells is defined here [radar_target_generation_and_detection.m (Line 163-167)](./src/radar_target_generation_and_detection.m#L163-L167).  
The offset is defined here [radar_target_generation_and_detection.m (Line 169-171)](./src/radar_target_generation_and_detection.m#L169-L171).  

* Steps taken to suppress the non-thresholded cells at the edges.  
Non-thresholded cells are suppressed here [radar_target_generation_and_detection.m (Line 203-205)](./src/radar_target_generation_and_detection.m#L203-L205).  
