# Domino Analytics Distribution 20210126

## Repo
quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210126

## Description
* Ubuntu 18.04
* Mini-conda 4.8.3 
* Python 3.8
* R 4.0.3
* Jupyter, Jupyterlab, VSCode, Rstudio

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
Additional images with CUDA installed are available.
| Dockerfile name  | Image tag |
| ------------- | ------------- |
| Dockerfile.cuda11  | quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210127_CUDA11.0_full  |
| Dockerfile.slim.cuda10_1  |quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210126_CUDA10.1   |
| Dockerfile.slim.cuda10_2 |quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210126_CUDA10.2|
| Dockerfile.slim.cuda11 |quay.io/domino/base:Ubuntu18_DAD_Py3.8_R4.0-20210126_CUDA11.0|
