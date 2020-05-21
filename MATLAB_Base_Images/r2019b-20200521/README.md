# MATLAB Domino Base Image 2020 05/21

## Image tag

To be set in the compute environment as the Base Image (under the Custom Image field):
```
quay.io/domino/matlab:r2019b-20200521
```

## Description

This image is based the Domino Analytics Distribution,
image tag `quay.io/domino/base:Ubuntu18_DAD_Py3.6_R3.6_20190916`,
listed in this repo under `Domino_Analytics_Distribution/2019_q3_py3.6_r3.6`.
See the Dockerfile for that image for details about what is included.
The MATLAB workspace has been added to that, and will run in Domino with the below notebook configuration and proper license configuration within the compute environment.

## Notebook Properties

Pluggable properties for MATLAB workspace to be set in the compute environment.
Optionally, any pluggable properties available to the parent environment (listed above) can also be used.

```
matlab:
    title: "MATLAB"
    iconUrl: "https://raw.githubusercontent.com/dominodatalab/workspace-configs/develop/workspace-logos/matlab.png"
    start: [ "/var/opt/workspaces/matlab/start.sh" ]
    httpProxy:
        port: 8888
        requireSubdomain: false
```
