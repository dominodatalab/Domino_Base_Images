# MATLAB R2019b Domino Base Image 2020 05/21

## Image tag

To be set in the compute environment as the Base Image (under the Custom Image field):
```
quay.io/domino/matlab:r2019b-20200521
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

## MATLAB Toolboxes

The following Toolboxes have been installed in this image, and can be used in a Domino session if you have the proper licenses for them.

```
MATLAB                                                Version 9.7         (R2019b)
Simulink                                              Version 10.0        (R2019b)
Computer Vision Toolbox                               Version 9.1         (R2019b)
Curve Fitting Toolbox                                 Version 3.5.10      (R2019b)
Deep Learning Toolbox                                 Version 13.0        (R2019b)
Global Optimization Toolbox                           Version 4.2         (R2019b)
Image Processing Toolbox                              Version 11.0        (R2019b)
MATLAB Compiler                                       Version 7.1         (R2019b)
MATLAB Compiler SDK                                   Version 6.7         (R2019b)
Optimization Toolbox                                  Version 8.4         (R2019b)
Parallel Computing Toolbox                            Version 7.1         (R2019b)
Predictive Maintenance Toolbox                        Version 2.1         (R2019b)
Signal Processing Toolbox                             Version 8.3         (R2019b)
Statistics and Machine Learning Toolbox               Version 11.6        (R2019b)
Symbolic Math Toolbox                                 Version 8.4         (R2019b)
System Identification Toolbox                         Version 9.11        (R2019b)
Text Analytics Toolbox                                Version 1.4         (R2019b)
```

