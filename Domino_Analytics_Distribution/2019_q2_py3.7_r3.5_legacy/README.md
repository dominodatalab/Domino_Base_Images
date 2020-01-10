# Domino Analytics Distribution 2019 Q2 py3.7_R3.5


## Repo
dominodatalab/base:DAD_py3.7_r3.5_2019q2_legacy

Also available under the tags: 
dominodatalab/base:Ubuntu18_DAD_Py3.7_R3.5-20190501
quay.io/domino/base:Ubuntu18_DAD_Py3.7_R3.5-20190501



## Description
Ubuntu 18.04
Anaconda Python 3.7
R 3.5.3
Jupyter Lab 0.35.4 ,Jupyter 1.0 ,Rstudio 1.2, VSCode
Keras 2.2.4 and Tensorflow-gpu 1.13.1
CUDA 10.0.130 with Nvidia driver 410.104


## Notebook Properities

Pluggable properties values to be set in the compute environment
```
jupyterlab:
    title: "JupyterLab (Beta)"
    iconUrl: "https://raw.githubusercontent.com/dominodatalab/workspace-configs/develop/workspace-logos/jupyterlab.svg?sanitize=true"
    start: [  /var/opt/workspaces/Jupyterlab/start.sh ]
    httpProxy:
        internalPath: "/{{#if pathToOpen}}/lab/tree/{{pathToOpen}}{{/if}}"
        port: 8888
        rewrite: false
rstudio:
  title: "RStudio"
  iconUrl: "https://raw.github.com/dominodatalab/workspace-configs/develop/workspace-logos//Rstudio.svg?sanitize=true"
  start: [ "/var/opt/workspaces/rstudio/start" ]
  httpProxy:
    port: 8888
vscode:
 title: "vscode"
 iconUrl: "https://raw.github.com/dominodatalab/workspace-configs/develop/workspace-logos/vscode.svg?sanitize=true"
 start: [ "/var/opt/workspaces/vscode/start" ]
 httpProxy:
    port: 8888
jupyter:
  title: "Jupyter (Python, R, Julia)"
  iconUrl: "https://raw.github.com/dominodatalab/workspace-configs/develop/workspace-logos/Jupyter.svg?sanitize=true"
  start: [ "/var/opt/workspaces/jupyter/start" ]
  httpProxy:
    port: 8888
    rewrite: false
    internalPath: "/{{#if pathToOpen}}tree/{{pathToOpen}}{{/if}}"
  supportedFileExtensions: [ ".ipynb" ]
```
