# MATLAB R2020a Domino Base Image 2020 10/14

## Image tag

To be set in the compute environment as the Base Image (under the Custom Image field):
```
quay.io/domino/matlab:R2020a-complete-20201014
```

## Description

This image is based on the Domino Analytics Distribution,
image tag `quay.io/domino/base:Ubuntu18_DAD_Py3.6_R3.6_20190916`,
listed in this repo under `Domino_Analytics_Distribution/2019_q3_py3.6_r3.6`.
See the Dockerfile for that image for details about what is included.
The MATLAB workspace has been added to that, and will run in Domino with the below notebook configuration and proper license configuration within the compute environment.

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

The following are notable changes in this image as compared to the previous ``quay.io/domino/matlab:r2020a-20200521`` image.
* A more complete set of toolboxes is now installed (see below).
* Parallel Server functionality and MDCS batch feature are added.
* Workspaces will now report the Domino username to the license server.
* Updated ``xpra`` version may improve the UI experience.
* An issue with the MATLAB installation path has been fixed; some suggested Domino workflows rely on the installation path including the MATLAB version, i.e. a folder named ``R2020a``, but in the previous image the folder instead was named ``R2020a_Update_2``.
* Known issue: ``lmutil`` license manager is not installed in the R2020a image; if you wish to use ``lmutil`` to troubleshoot license server issues, please use the R2019b image.




## MATLAB Toolboxes

The following Toolboxes have been installed in this image, and can be used in a Domino session if you have the proper licenses for them.

```
MATLAB                                                Version 9.8         (R2020a)
Simulink                                              Version 10.1        (R2020a)
5G Toolbox                                            Version 2.0         (R2020a)
AUTOSAR Blockset                                      Version 2.2         (R2020a)
Aerospace Blockset                                    Version 4.3         (R2020a)
Aerospace Toolbox                                     Version 3.3         (R2020a)
Antenna Toolbox                                       Version 4.2         (R2020a)
Audio Toolbox                                         Version 2.2         (R2020a)
Automated Driving Toolbox                             Version 3.1         (R2020a)
Bioinformatics Toolbox                                Version 4.14        (R2020a)
Communications Toolbox                                Version 7.3         (R2020a)
Computer Vision Toolbox                               Version 9.2         (R2020a)
Control System Toolbox                                Version 10.8        (R2020a)
Curve Fitting Toolbox                                 Version 3.5.11      (R2020a)
DSP System Toolbox                                    Version 9.10        (R2020a)
Database Toolbox                                      Version 9.2.1       (R2020a)
Datafeed Toolbox                                      Version 5.9.1       (R2020a)
Deep Learning Toolbox                                 Version 14.0        (R2020a)
Econometrics Toolbox                                  Version 5.4         (R2020a)
Embedded Coder                                        Version 7.4         (R2020a)
Filter Design HDL Coder                               Version 3.1.7       (R2020a)
Financial Instruments Toolbox                         Version 3.0         (R2020a)
Financial Toolbox                                     Version 5.15        (R2020a)
Fixed-Point Designer                                  Version 7.0         (R2020a)
Fuzzy Logic Toolbox                                   Version 2.7         (R2020a)
GPU Coder                                             Version 1.5         (R2020a)
Global Optimization Toolbox                           Version 4.3         (R2020a)
HDL Coder                                             Version 3.16        (R2020a)
HDL Verifier                                          Version 6.1         (R2020a)
Image Acquisition Toolbox                             Version 6.2         (R2020a)
Image Processing Toolbox                              Version 11.1        (R2020a)
Instrument Control Toolbox                            Version 4.2         (R2020a)
LTE Toolbox                                           Version 3.3         (R2020a)
MATLAB Coder                                          Version 5.0         (R2020a)
MATLAB Compiler                                       Version 8.0         (R2020a)
MATLAB Compiler SDK                                   Version 6.8         (R2020a)
MATLAB Report Generator                               Version 5.8         (R2020a)
Mapping Toolbox                                       Version 4.10        (R2020a)
Mixed-Signal Blockset                                 Version 1.2         (R2020a)
Model Predictive Control Toolbox                      Version 6.4         (R2020a)
Motor Control Blockset                                Version 1.0         (R2020a)
Navigation Toolbox                                    Version 1.1         (R2020a)
Optimization Toolbox                                  Version 8.5         (R2020a)
Parallel Computing Toolbox                            Version 7.2         (R2020a)
Partial Differential Equation Toolbox                 Version 3.4         (R2020a)
Phased Array System Toolbox                           Version 4.3         (R2020a)
Powertrain Blockset                                   Version 1.7         (R2020a)
Predictive Maintenance Toolbox                        Version 2.2         (R2020a)
RF Blockset                                           Version 7.4         (R2020a)
RF Toolbox                                            Version 3.8         (R2020a)
ROS Toolbox                                           Version 1.1         (R2020a)
Reinforcement Learning Toolbox                        Version 1.2         (R2020a)
Risk Management Toolbox                               Version 1.7         (R2020a)
Robotics System Toolbox                               Version 3.1         (R2020a)
Robust Control Toolbox                                Version 6.8         (R2020a)
Sensor Fusion and Tracking Toolbox                    Version 1.3         (R2020a)
SerDes Toolbox                                        Version 1.2         (R2020a)
Signal Processing Toolbox                             Version 8.4         (R2020a)
SimBiology                                            Version 5.10        (R2020a)
SimEvents                                             Version 5.8         (R2020a)
Simscape                                              Version 4.8         (R2020a)
Simscape Driveline                                    Version 3.1         (R2020a)
Simscape Electrical                                   Version 7.3         (R2020a)
Simscape Fluids                                       Version 3.0         (R2020a)
Simscape Multibody                                    Version 7.1         (R2020a)
Simulink 3D Animation                                 Version 9.0         (R2020a)
Simulink Check                                        Version 4.5         (R2020a)
Simulink Code Inspector                               Version 3.6         (R2020a)
Simulink Coder                                        Version 9.3         (R2020a)
Simulink Compiler                                     Version 1.0         (R2020a)
Simulink Control Design                               Version 5.5         (R2020a)
Simulink Coverage                                     Version 5.0         (R2020a)
Simulink Design Optimization                          Version 3.8         (R2020a)
Simulink Design Verifier                              Version 4.3         (R2020a)
Simulink PLC Coder                                    Version 3.2         (R2020a)
Simulink Report Generator                             Version 5.8         (R2020a)
Simulink Requirements                                 Version 1.5         (R2020a)
Simulink Test                                         Version 3.2         (R2020a)
SoC Blockset                                          Version 1.2         (R2020a)
Stateflow                                             Version 10.2        (R2020a)
Statistics and Machine Learning Toolbox               Version 11.7        (R2020a)
Symbolic Math Toolbox                                 Version 8.5         (R2020a)
System Composer                                       Version 1.2         (R2020a)
System Identification Toolbox                         Version 9.12        (R2020a)
Text Analytics Toolbox                                Version 1.5         (R2020a)
Trading Toolbox                                       Version 3.6.1       (R2020a)
Vehicle Dynamics Blockset                             Version 1.4         (R2020a)
Vehicle Network Toolbox                               Version 4.4         (R2020a)
Vision HDL Toolbox                                    Version 2.1         (R2020a)
WLAN Toolbox                                          Version 3.0         (R2020a)
Wavelet Toolbox                                       Version 5.4         (R2020a)
Wireless HDL Toolbox                                  Version 2.0         (R2020a)
```
