# Domino Analytics Distribution 20210503

## Repo
quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210709_noCUDA

## Description
* Ubuntu 18.04
* Mini-conda 4.8.3 
* Python 3.8
* R 4.0.5
* Jupyter, Jupyterlab, VSCode, Rstudio

## Change Log
* July 9th, 2021
  * Remove bintray from list of apt sources as it was retired on July 4th
* May 3rd, 2021
  * R 4.0.2 => 4.0.5
  * Miniconda 4.7.12.1 => py38_4.8.3
  * Python 3.6 => 3.8
  * Use updated workspace configs
    * Stop pinning JupyterLab version < 3.0.0
    * Bump RStudio version to 1.4, add required chowns
  * Security Fixes:
    * Comment out openssh server 
    * Upgrade git client version
    * Remove scala kernel (almond)
  * Install git lfs
  * Add Goofys binaries to support EDV's
  * Add SSHFS binaries to support EDV's
  * Add future as R package

## Notebook Properities

Pluggable properties values to be set in the compute environment
```
jupyter:
  title: "Jupyter (Python, R, Julia)"
  iconUrl: "/assets/images/workspace-logos/Jupyter.svg"
  start: [ "/var/opt/workspaces/jupyter/start" ]
  httpProxy:
    port: 8888
    rewrite: false
    internalPath: "/{{ownerUsername}}/{{projectName}}/{{sessionPathComponent}}/{{runId}}/{{#if pathToOpen}}tree/{{pathToOpen}}{{/if}}"
    requireSubdomain: false
  supportedFileExtensions: [ ".ipynb" ]
jupyterlab:
  title: "JupyterLab"
  iconUrl: "/assets/images/workspace-logos/jupyterlab.svg"
  start: [  /var/opt/workspaces/Jupyterlab/start.sh ]
  httpProxy:
    internalPath: "/{{ownerUsername}}/{{projectName}}/{{sessionPathComponent}}/{{runId}}/{{#if pathToOpen}}tree/{{pathToOpen}}{{/if}}"
    port: 8888
    rewrite: false
    requireSubdomain: false
vscode:
 title: "vscode"
 iconUrl: "/assets/images/workspace-logos/vscode.svg"
 start: [ "/var/opt/workspaces/vscode/start" ]
 httpProxy:
    port: 8888
    requireSubdomain: false
rstudio:
  title: "RStudio"
  iconUrl: "/assets/images/workspace-logos/Rstudio.svg"
  start: [ "/var/opt/workspaces/rstudio/start" ]
  httpProxy:
    port: 8888
    requireSubdomain: false
```

## Additional Images
Additional images with CUDA or spark installed are also available.
| Dockerfile name  | Image tag |
| ------------- | ------------- |
| Dockerfile.slim.cuda10.1 | quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210709_CUDA10.1 |
| Dockerfile.slim.cuda11 | quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210709_CUDA11 |
| Dockerfile.cuda11 | quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210709_CUDA11_full |
| Dockerfile.spark | quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210709_Spark3.1
