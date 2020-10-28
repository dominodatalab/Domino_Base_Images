# MATLAB R2019b Domino Base Image 2020 10/14

## Image tag

To be set in the compute environment as the Base Image (under the Custom Image field):
```
quay.io/domino/matlab:R2019b-complete-20201014
```

## Description

This image is based on the Domino Analytics Distribution,
image tag `quay.io/domino/base:Ubuntu18_DAD_Py3.6_R3.6_20190916`,
listed in this repo under `Domino_Analytics_Distribution/2019_q3_py3.6_r3.6`.
See the Dockerfile for that image for details about what is included.
The MATLAB workspace has been added, and will run in Domino with the below notebook configuration and proper license configuration within the compute environment.

## Notebook Properties

Pluggable properties for MATLAB workspace to be set in the compute environment:

```
matlab:
    title: "MATLAB"
    iconUrl: "https://raw.githubusercontent.com/dominodatalab/workspace-configs/develop/workspace-logos/matlab.png"
    start: [ "/var/opt/workspaces/matlab/start.sh" ]
    httpProxy:
        port: 8888
        requireSubdomain: false
```

Optionally, any pluggable properties available to the parent image (the Domino Analytics Distribution above) can also be used.

## Release Notes

The following are notable changes in this image as compared to the previous ``quay.io/domino/matlab:r2019b-20200521`` image.
* This image has a more complete set of toolboxes (see below).
* Parallel Server functionality and MDCS batch feature are added.
* Workspaces will now report the Domino username to the license server.
* Updated ``xpra`` version may improve the UI experience.
* Issues with ``lmutil`` license manager utility are fixed.


## MATLAB Toolboxes

The following Toolboxes have been installed in this image, and can be used in a Domino session if you have the proper licenses for them.

```
MATLAB                                                Version 9.7         (R2019b)
Simulink                                              Version 10.0        (R2019b)
5G Toolbox                                            Version 1.2         (R2019b)
AUTOSAR Blockset                                      Version 2.1         (R2019b)
Aerospace Blockset                                    Version 4.2         (R2019b)
Aerospace Toolbox                                     Version 3.2         (R2019b)
Antenna Toolbox                                       Version 4.1         (R2019b)
Audio Toolbox                                         Version 2.1         (R2019b)
Automated Driving Toolbox                             Version 3.0         (R2019b)
Bioinformatics Toolbox                                Version 4.13        (R2019b)
Communications Toolbox                                Version 7.2         (R2019b)
Computer Vision Toolbox                               Version 9.1         (R2019b)
Control System Toolbox                                Version 10.7        (R2019b)
Curve Fitting Toolbox                                 Version 3.5.10      (R2019b)
DSP System Toolbox                                    Version 9.9         (R2019b)
Database Toolbox                                      Version 9.2         (R2019b)
Datafeed Toolbox                                      Version 5.9         (R2019b)
Deep Learning Toolbox                                 Version 13.0        (R2019b)
Econometrics Toolbox                                  Version 5.3         (R2019b)
Embedded Coder                                        Version 7.3         (R2019b)
Filter Design HDL Coder                               Version 3.1.6       (R2019b)
Financial Instruments Toolbox                         Version 2.10        (R2019b)
Financial Toolbox                                     Version 5.14        (R2019b)
Fixed-Point Designer                                  Version 6.4         (R2019b)
Fuzzy Logic Toolbox                                   Version 2.6         (R2019b)
GPU Coder                                             Version 1.4         (R2019b)
Global Optimization Toolbox                           Version 4.2         (R2019b)
HDL Coder                                             Version 3.15        (R2019b)
HDL Verifier                                          Version 6.0         (R2019b)
Image Acquisition Toolbox                             Version 6.1         (R2019b)
Image Processing Toolbox                              Version 11.0        (R2019b)
Instrument Control Toolbox                            Version 4.1         (R2019b)
LTE HDL Toolbox                                       Version 1.4         (R2019b)
LTE Toolbox                                           Version 3.2         (R2019b)
MATLAB Coder                                          Version 4.3         (R2019b)
MATLAB Compiler                                       Version 7.1         (R2019b)
MATLAB Compiler SDK                                   Version 6.7         (R2019b)
MATLAB Report Generator                               Version 5.7         (R2019b)
Mapping Toolbox                                       Version 4.9         (R2019b)
Mixed-Signal Blockset                                 Version 1.1         (R2019b)
Model Predictive Control Toolbox                      Version 6.3.1       (R2019b)
Navigation Toolbox                                    Version 1.0         (R2019b)
Optimization Toolbox                                  Version 8.4         (R2019b)
Parallel Computing Toolbox                            Version 7.1         (R2019b)
Partial Differential Equation Toolbox                 Version 3.3         (R2019b)
Phased Array System Toolbox                           Version 4.2         (R2019b)
Powertrain Blockset                                   Version 1.6         (R2019b)
Predictive Maintenance Toolbox                        Version 2.1         (R2019b)
RF Blockset                                           Version 7.3         (R2019b)
RF Toolbox                                            Version 3.7         (R2019b)
ROS Toolbox                                           Version 1.0         (R2019b)
Reinforcement Learning Toolbox                        Version 1.1         (R2019b)
Risk Management Toolbox                               Version 1.6         (R2019b)
Robotics System Toolbox                               Version 3.0         (R2019b)
Robust Control Toolbox                                Version 6.7         (R2019b)
Sensor Fusion and Tracking Toolbox                    Version 1.2         (R2019b)
SerDes Toolbox                                        Version 1.1         (R2019b)
Signal Processing Toolbox                             Version 8.3         (R2019b)
SimBiology                                            Version 5.9         (R2019b)
SimEvents                                             Version 5.7         (R2019b)
Simscape                                              Version 4.7         (R2019b)
Simscape Driveline                                    Version 3.0         (R2019b)
Simscape Electrical                                   Version 7.2         (R2019b)
Simscape Fluids                                       Version 2.7         (R2019b)
Simscape Multibody                                    Version 7.0         (R2019b)
Simulink 3D Animation                                 Version 8.3         (R2019b)
Simulink Check                                        Version 4.4         (R2019b)
Simulink Code Inspector                               Version 3.5         (R2019b)
Simulink Coder                                        Version 9.2         (R2019b)
Simulink Control Design                               Version 5.4         (R2019b)
Simulink Coverage                                     Version 4.4         (R2019b)
Simulink Design Optimization                          Version 3.7         (R2019b)
Simulink Design Verifier                              Version 4.2         (R2019b)
Simulink PLC Coder                                    Version 3.1         (R2019b)
Simulink Report Generator                             Version 5.7         (R2019b)
Simulink Requirements                                 Version 1.4         (R2019b)
Simulink Test                                         Version 3.1         (R2019b)
SoC Blockset                                          Version 1.1         (R2019b)
Stateflow                                             Version 10.1        (R2019b)
Statistics and Machine Learning Toolbox               Version 11.6        (R2019b)
Symbolic Math Toolbox                                 Version 8.4         (R2019b)
System Composer                                       Version 1.1         (R2019b)
System Identification Toolbox                         Version 9.11        (R2019b)
Text Analytics Toolbox                                Version 1.4         (R2019b)
Trading Toolbox                                       Version 3.6         (R2019b)
Vehicle Dynamics Blockset                             Version 1.3         (R2019b)
Vehicle Network Toolbox                               Version 4.3         (R2019b)
Vision HDL Toolbox                                    Version 2.0         (R2019b)
WLAN Toolbox                                          Version 2.2         (R2019b)
Wavelet Toolbox                                       Version 5.3         (R2019b)
```
