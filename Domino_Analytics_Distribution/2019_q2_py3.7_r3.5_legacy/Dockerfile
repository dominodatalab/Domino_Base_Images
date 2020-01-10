FROM ubuntu:18.04
USER root

#### Utilities required by Domino ####
ENV DEBIAN_FRONTEND noninteractive


#create a Ubuntu User
RUN \
  groupadd -g 12574 ubuntu && \
  useradd -u 12574 -g 12574 -m -N -s /bin/bash ubuntu && \

  # UPDATE, UPGRADE, ADD repositories
  apt-get update -y && \
  apt-get -y install software-properties-common && \
  apt-get update -y && \
  apt-get -y upgrade && \
  # CONFIGURE locales
  apt-get install -y locales && \
  locale-gen en_US.UTF-8 && \
  dpkg-reconfigure locales && \
  # INSTALL common
  apt-get -y install build-essential wget sudo curl apt-utils net-tools libzmq3-dev ed git openssh-server iputils-ping dnsutils && \
  apt-get install openjdk-8-jdk -y && \
  update-alternatives --config java && \
  apt-get install vim nano curl telnet -y && \
  apt-get install apt-transport-https -y && \
  apt-get -y install libssl-dev libxml2-dev libxt-dev libssh2-1-dev libcurl4-openssl-dev libsasl2-dev libssl-dev && \
  #apt AWS CLI
  apt-get install awscli -y  && \
  # ADD SSH start script
  mkdir -p /scripts && \
  printf "#!/bin/bash\\nservice ssh start\\n" > /scripts/start-ssh && \
  chmod +x /scripts/start-ssh && \
  echo 'export PYTHONIOENCODING=utf-8' >> /home/ubuntu/.domino-defaults && \
  echo 'export LANG=en_US.UTF-8' >> /home/ubuntu/.domino-defaults && \
  echo 'export JOBLIB_TEMP_FOLDER=/tmp' >> /home/ubuntu/.domino-defaults && \
  echo 'export LC_ALL=en_US.UTF-8' >> /home/ubuntu/.domino-defaults && \
  locale-gen en_US.UTF-8 && \
  export LANG=en_US.UTF-8 && \
  rm -rf /var/lib/apt/lists/*
    
ENV LANG en_US.UTF-8



#### R ####

#Install R
RUN \ 

apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
 add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/' && \

apt-get update -y && \
apt-get install r-base-core r-base --force-yes -y && \
 # INSTALL R packages dependencies
 #apt-get -y install libssl-dev libxml2-dev libxt-dev libssh2-1-dev libcurl4-openssl-dev libsasl2-dev libssl-dev && \
# INSTALL R packages required by Domino
R -e 'options(repos=structure(c(CRAN="http://cran.us.r-project.org"))); install.packages(c( "devtools", "stringi", "httpuv","RJSONIO", "Cairo", "jsonlite","RODBC","RJDBC"))' && \
cd /tmp && wget -q http://cran.us.r-project.org/src/contrib/Archive/plumber/plumber_0.3.2.tar.gz && R CMD INSTALL plumber_0.3.2.tar.gz && rm /tmp/plumber_0.3.2.tar.gz && \
#dependencies of various R packages
apt-get update && \
apt-get install -y libcairo2-dev  libxt-dev libgmp3-dev jags libgsl0-dev libx11-dev mesa-common-dev libglu1-mesa-dev libmpfr-dev libfftw3-dev libtiff5-dev libiodbc2-dev libudunits2-dev -y && \
#required for rJava
export LD_LIBRARY_PATH=/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server && \
R CMD javareconf && \
#install R packages
R --no-save -e 'install.packages(c("keras","sparklyr","mongolite","forecast","abind", "acepack", "ade4", "akima", "alr3", "animation", "ape", "argparse", "ascii", "assertthat", "aws.s3", "aws.signature", "backports", "base64", "base64enc", "BH", "bibtex", "biglm", "bit", "bit64", "bitops", "BradleyTerry2", "brew", "brglm", "BTYD", "bvls", "Cairo", "car", "caret", "caTools",  "chron", "circular", "clue", "clusterGeneration", "coda", "coin", "colorRamps", "colorspace", "combinat", "contfrac", "corpcor", "corrgram", "corrplot", "crayon", "curl", "data.table", "DBI", "deldir", "dendextend", "DEoptimR", "deSolve", "devtools", "dichromat", "digest", "diptest", "dmt", "doMC", "doParallel", "doRedis", "doRNG", "dplyr", "dynlm", "e1071", "earth", "elasticnet", "ellipse", "elliptic", "evaluate", "expm", "extrafont", "extrafontdb", "fastICA", "fastmatch", "fBasics", "ff", "findpython", "flexmix", "FMStable", "foreach", "forecast", "formatR", "Formula", "fpc", "fracdiff", "gains", "gam", "gbm", "gclus", "gdata", "gee", "geepack", "geiger", "getopt", "ggfortify", "ggplot2", "git2r", "glmnet", "gmp", "gplots", "googlesheets","gridExtra", "gss", "gtable", "gtools", "h2o", "hexbin", "hflights", "highlight", "highr", "Hmisc", "htmltools", "htmlwidgets", "httpuv", "httr", "hypergeo", "igraph", "igraphdata", "inline", "intervals", "ipred", "IRdisplay", "IRkernel", "iterators", "itertools", "jpeg", "jsonlite", "kernlab", "KFAS", "klaR", "knitr", "labeling", "Lahman", "lars", "lasso2", "lattice", "latticeExtra", "lava", "lazyeval", "lda", "LDPD", "leaflet","leaps", "LearnBayes", "lme4", "lmtest", "locfit", "logspline", "lokern", "lpSolve", "lubridate", "magrittr", "mailR", "mapproj", "maps", "maptools", "markdown", "MARSS", "MatrixModels", "matrixStats", "mclust", "mda", "memoise", "mgcv", "mice", "microbenchmark", "mime", "miniUI", "minqa", "misc3d", "mix", "mixtools", "mlbench", "mnormt", "modeltools", "msm", "multcomp", "munsell", "mvtnorm", "ncbit", "nleqslv", "nloptr", "NLP", "nnls", "nor1mix", "numDeriv", "nws", "OAIHarvester", "openssl", "pander", "party", "pbkrtest", "PerformanceAnalytics", "permute", "phangorn", "pheatmap", "phylobase", "phytools", "picante", "pipeR", "pixmap", "pkgmaker", "plotly", "plotmo", "plotrix", "pls", "plumber", "plyr", "png", "polspline", "PortfolioAnalytics", "ppcor", "prabclus", "pROC", "prodlim", "profileModel", "proto", "proxy", "psych", "qap", "quadprog", "Quandl", "quantmod", "quantreg", "R2jags", "R2WinBUGS", "R6", "randomForest", "RANN", "rbenchmark", "R.cache", "RColorBrewer", "Rcpp", "RcppArmadillo", "RcppEigen", "RcppGSL", "RcppRoll", "RCurl", "R.devices", "readr", "registry", "relations", "repr", "reshape", "reshape2", "R.filesets", "RGCCA", "rgl", "RGraphics", "R.huge", "ridge", "rjags", "rJava", "rjson", "RJSONIO", "rlecuyer", "rmarkdown", "R.methodsS3", "Rmpfr", "Rmpi", "rms", "rngtools", "robustbase", "ROCR", "RODBC", "R.oo", "Rook", "roxygen2", "RPMM", "rprojroot", "rredis", "R.rsp", "Rserve", "RSQLite", "rstan", "rstudioapi", "Rttf2pt1", "RUnit", "R.utils", "rversions", "rzmq", "sandwich", "scales", "scatterplot3d", "segmented", "seriation", "sets", "sfsmisc", "shinydashboard", "shinyjs", "sitools", "sjmisc", "sjPlot", "slackr", "slam", "sm", "snow", "SnowballC", "snowfall", "sourcetools", "sp", "spam", "SparseM", "spdep", "spls", "stabledist", "stargazer", "statmod", "stringi", "stringr", "strucchange", "subplex", "survey", "tables", "TeachingDemos", "testthat", "TH.data", "tibble", "tidyr", "tiff", "timeDate", "timeSeries", "tm", "topicmodels", "trimcluster", "tripack", "tseries", "TSP", "TTR", "tweedie", "uuid", "vcd", "vegan", "VGAM", "VGAMdata", "viridis", "whisker", "xgboost", "XLConnect", "XLConnectJars", "xlsx", "xlsxjars", "XML", "xml2", "xtable", "xts", "yaml", "zoo", "base", "boot", "class", "cluster", "codetools", "compiler", "datasets", "foreign", "graphics", "grDevices", "grid", "KernSmooth", "lattice", "MASS", "Matrix", "methods", "mgcv", "nlme", "nnet", "parallel", "rpart", "spatial", "splines", "stats", "stats4", "survival", "tcltk", "tools", "utils"),repos="https://cran.revolutionanalytics.com/",clean=TRUE,Ncpus = getOption("Ncpus", 4L))' && \
R --no-save -e "install.packages(c('tidyverse','domino','feather','choroplethr', 'choroplethrMaps','maps','shinyjs','data.table','DT','ggvis'), repos='https://cran.revolutionanalytics.com/',clean=TRUE,Ncpus = getOption('Ncpus', 4L))" && \
rm -rf /usr/local/lib/R/site-library/XLConnect/unitTests/resources/testBug61.xlsx && \

#Install rdgal package
 apt-get install -y libmysqlclient-dev libgdal-dev  libproj-dev && \
chown -R ubuntu:ubuntu /home/ubuntu && \
chown -R ubuntu:ubuntu /usr/local/lib/R/site-library 

# ################ rgdal ##################

RUN \
add-apt-repository -y ppa:ubuntugis/ubuntugis-unstable && \
 apt-get update && \
 apt-get install libgdal-dev -y && \
 apt install gdal-bin python-gdal python3-gdal libgdal-dev -y && \
 apt-get install gdal-bin && \
 R -e "install.packages('rgdal',repos='https://cran.revolutionanalytics.com/')" && \
 add-apt-repository -r ppa:ubuntugis/ubuntugis-unstable && \
 apt-get update -y && \
 
 ###fix R-3.5 API issue
 add-apt-repository ppa:marutter/c2d4u3.5 && \
 apt-get update -y 


  
#### Python #### 
ENV PATH /usr/local/anaconda/bin:$PATH


RUN \
  # Install Anaconda for Python 3.7 v 2018-12-21
  cd /tmp && wget -q https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh -O anaconda.sh   &&  \
    yes | bash anaconda.sh -b -p /usr/local/anaconda && \
    conda update -q -y --all   &&  \
    ipython kernel install   &&  \
    pip install --upgrade pip &&  \
    echo 'export PATH=/usr/local/anaconda/bin:${PATH:-}' >> /home/ubuntu/.domino-defaults &&  \
 # Point pip to use the one in Anaconda
    ln -s /usr/local/anaconda/bin/pip /usr/local/bin/pip &&  \
    rm -Rf /tmp/* && \
 # required for Python 3, Python endpoints
    apt-get update -y && \
    pip install tornado==5.1.1 && \
    pip uninstall colorama -y && \
    pip install jaydebeapi jpype1 && \
#Configure matplotlib
# INSTALL and CONFIGURE Matplotlib
    pip install matplotlib && \
    pip install cairocffi && \
    mkdir -p /home/ubuntu/.config/matplotlib && \
    echo "backend : Cairo" > /home/ubuntu/.config/matplotlib/matplotlibrc  && \
    sed -i -e 's/backend      : qt5agg/backend      : Cairo/g' /usr/local/anaconda/lib/python3.7/site-packages/matplotlib/mpl-data/matplotlibrc && \
    # INSTALL pip libraries that Domino requires
    pip install --upgrade pip urllib3 flask jsonify==0.5  jsonschema nbserverproxy && \
    pip install --ignore-installed certifi  && \
    conda install -c conda-forge libiconv &&  conda install -c conda-forge uwsgi && \
 # Additional Python packages
    pip install bson joblib jsonify pandoc paramiko plotly pymongo pypandoc beautifulsoup4 gensim ggplot gunicorn Markdown mpltools netCDF4 networkx seaborn xgboost dash dash-renderer dash-html-components dash-core-components dash-table-experiments simplejson memory_profiler pandas-datareader pandas-profiling regex unidecode websocket xarray quilt && \
    pip install git+https://github.com/dominodatalab/python-domino.git && \
    sleep 5 && \
    #Switching to numpy/scipy with Intel MKL (Note: not yet available for py3.7)
 #   pip uninstall numpy scipy -y && \
#    pip install intel-numpy intel-scipy mkl_fft mkl_random mkl ipp impi daal intel-openmp && \
      # SET ownership to ubuntu user
    ln -s /usr/local/anaconda/bin/python /usr/local/bin/python && \
    ln -s /usr/local/anaconda/bin/python /usr/local/bin/python3  && \
    chown ubuntu:ubuntu -R /usr/local/anaconda && \
    chown ubuntu:ubuntu -R /usr/local/bin/python && \
    chown ubuntu:ubuntu -R /usr/local/bin/python3 && \
    #addintion addinition python packages
    apt-get install -y libzmq5-dev libzmq5 pandoc pandoc-citeproc && \
    apt-get install -y libhdf5-dev libyaml-dev pkg-config  libopenmpi-dev r-cran-rmpi && \  
    apt-get install krb5-kdc krb5-admin-server -y && \
    ###Add codeserver dependencies
    apt-get install libssl1.0-dev node-gyp nodejs-dev nodejs=8.10* npm -y && \
    apt-get install -y libfuse-dev cups libcups2-dev python-gi python-gi-cairo python3-gi python3-gi-cairo gir1.2-gtk-3.0 python-mvpa2 libsmbclient-dev libcups2-dev python-debian python-igraph swig telnet nmap && \
    #cleaning up
    conda clean -pt && \
    rm -rf /var/lib/apt/lists/*



#### Install drivers for common data source connections #####

#Database drivers
#SQL 
RUN \
 # apt-get -y -q install vpnc && \
  apt-get update -y && apt-get install tdsodbc -y && \
  apt-get install -y libodbc1 unixodbc unixodbc-dev freetds-common freetds-dev
 
RUN \
  cd /tmp && \
  wget -q ftp://ftp.unixodbc.org/pub/unixODBC/unixODBC-2.3.4.tar.gz && \
  tar -xf unixODBC-2.3.4.tar.gz && \
  cd unixODBC-2.3.4 && \
  ./configure --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE --libdir=/usr/lib/x86_64-linux-gnu --prefix=/usr --sysconfdir=/etc --enable-stats=no && \
  make && \
  make install && \
  ln -s /lib/x86_64-linux-gnu/libssl.so.1.0.0 /lib/x86_64-linux-gnu/libssl.so.10 && \
  ln -s /lib/x86_64-linux-gnu/libcrypto.so.1.0.0 /lib/x86_64-linux-gnu/libcrypto.so.10 && \
  ldconfig && \
  rm -rf /tmp/*
  
# #Oracle
# #ROracle & PyOracle
RUN \
    mkdir -p /opt/oracle && \
    wget -q https://s3-us-west-2.amazonaws.com/domino-deployment/2016/02/22/instantclient-basic-linux.x64-12.1.0.2.0.zip -O /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip && \
    wget -q https://s3-us-west-2.amazonaws.com/domino-deployment/2016/02/22/instantclient-sdk-linux.x64-12.1.0.2.0.zip -O /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip && \
    apt-get install libaio1 && \
    mkdir -p /opt/oracle/instantclient_12_1 && \
    cd /opt/oracle && \
    unzip instantclient-basic-linux.x64-12.1.0.2.0.zip && \
    unzip instantclient-sdk-linux.x64-12.1.0.2.0.zip && \
    cd /opt/oracle/instantclient_12_1 && \
    ln -s libclntsh.so.12.1 libclntsh.so && \
    ln -s libocci.so.12.1 libocci.so && \
    echo "export LD_LIBRARY_PATH=/opt/oracle/instantclient_12_1:\${LD_LIBRARY_PATH:-}" >> /home/ubuntu/.domino-defaults && \
    echo 'export OCI_LIB=/opt/oracle/instantclient_12_1' >> /home/ubuntu/.domino-defaults && \
    echo 'export OCI_INC=/opt/oracle/instantclient_12_1/sdk/include' >> /home/ubuntu/.domino-defaults && \
    echo "export PATH=/opt/oracle/instantclient_12_1:\${PATH:-}" >> /home/ubuntu/.domino-defaults && \
    chown -R ubuntu:ubuntu /opt/oracle/instantclient_12_1 && \
    echo '/opt/oracle/instantclient_12_1' > /etc/ld.so.conf.d/oracle-instantclient.conf && \
    ldconfig -v && \
    
    export PATH=/opt/oracle/instantclient_12_1:${PATH:-} && \
    export LD_LIBRARY_PATH=/opt/oracle/instantclient_12_1:${LD_LIBRARY_PATH:-} && \
    pip install cx_Oracle  && \
    cd /home/ubuntu && \
    wget -q https://cran.r-project.org/src/contrib/ROracle_1.3-1.tar.gz && \
    R CMD INSTALL --configure-args='--with-oci-inc=/opt/oracle/instantclient_12_1/sdk/include --with-oci-lib=/opt/oracle/instantclient_12_1' ROracle_1.3-1.tar.gz
    
    
# #Install PostgreSQL client
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN apt-get update && apt-get -y -q install postgresql-9.3 postgresql-client-9.3 postgresql-contrib-9.3


 
####### R KERNEL IN JUPYTER ############

RUN R --no-save -e 'install.packages("pbdZMQ", repos="https://cran.revolutionanalytics.com/", clean=TRUE)'
USER ubuntu
RUN R --no-save -e 'devtools::install_github("IRkernel/IRkernel"); IRkernel::installspec()'
USER root

RUN R --no-save -e 'install.packages(c("RPostgreSQL","RODBC","RMySQL","RPostgres"))'



######Scala Kernel
RUN cd /tmp && wget -q https://downloads.lightbend.com/scala/2.12.6/scala-2.12.6.deb && dpkg -i scala-2.12.6.deb && apt-get update -y && apt-get install scala -y --allow-downgrades && \
echo 'export SCALA_HOME=/usr/share/scala' >> /home/ubuntu/.domino-defaults && \
echo 'export PATH=$PATH:$SCALA_HOME/bin:$PATH' >> /home/ubuntu/.domino-defaults && \
echo 'export PATH=$PATH:/tmp:$PATH' >> /home/ubuntu/.domino-defaults && \
cd /tmp && curl -L -o coursier https://git.io/coursier && chmod +x coursier && \
cd /tmp && wget -q https://github.com/almond-sh/almond/archive/v0.1.8.tar.gz && tar -zxvf v0.1.8.tar.gz && mv almond-0.1.8 almond && export SCALA_VERSION=2.12.6 && export ALMOND_VERSION=0.1.8 && ./coursier bootstrap -r jitpack -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION --sources --default=true -o almond-out && ./almond-out --install --global --id scala212 --display-name "Scala (2.12)"

## SBT
RUN echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list && \
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 && \
apt-get update -y && \
apt-get install sbt -y && \
rm -rf /var/lib/apt/lists/*

###Julia

RUN rm -rf /usr/bin/julia && \
    cd /home/ubuntu && \
    wget -q https://julialang-s3.julialang.org/bin/linux/x64/1.1/julia-1.1.0-linux-x86_64.tar.gz && \
    tar xzf julia-1.1.0-linux-x86_64.tar.gz && \
    chown -R ubuntu:ubuntu /home/ubuntu/julia-1.1.0 && \
    ln -s /home/ubuntu/julia-1.1.0/bin/julia /usr/bin/julia && \
    rm -rf /home/ubuntu/julia-1.1.0-linux-x86_64.tar.gz
 
USER ubuntu
RUN julia -e 'using Pkg; Pkg.update(); Pkg.add("IJulia")'
USER root


################ NLP ###############

RUN pip install -U nltk corpora && \
pip install -U spacy


########Enable nbserver proxy###########
USER ubuntu
RUN jupyter serverextension enable --py nbserverproxy
USER root

#######Force same nvidia version

ENV DEBIAN_FRONTEND noninteractive
 
RUN echo 'DPkg::options { "--force-confdef"; "--force-confnew"; }' >> /etc/apt/apt.conf.d/local
  
# Remove CUDA and Nvidia drivers
RUN apt-get update && \
    apt-get install -y update-manager-core && \
    apt-get install -y apt dpkg && \
    apt-mark unhold nvidia* cuda* && \
    apt-get purge -y --force-yes nvidia-* cuda*
  
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates apt-transport-https && \
    curl -s http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub | apt-key add - && \
    echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list && \
    echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get update -y
 
# Include the following if they need cuDNN 7 and the latest Tensorflow
ENV CUDNN_VERSION 7.4.2.24
  
RUN apt-get update && apt-get install -y --no-install-recommends \
            libcudnn7=$CUDNN_VERSION-1+cuda10.0
RUN cd /tmp && wget -q https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda_10.0.130_410.48_linux && \
    cd /tmp && chmod +x cuda_10.0.130_410.48_linux && \
    cd /tmp && sh cuda_10.0.130_410.48_linux --silent --toolkit

RUN apt-get install --no-install-recommends -y nvidia-driver-410 && cd /tmp && rm -rf cuda_10.0.130_410.48_linux

RUN ln -s /usr/local/cuda-10.0 /usr/local/cuda && \
echo 'export PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:$PATH' >> /home/ubuntu/.domino-defaults && \
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/nvidia/lib:/usr/local/nvidia/lib64:$LD_LIBRARY_PATH' >> /home/ubuntu/.domino-defaults
  
RUN pip install tensorflow-gpu && pip install -U keras


#add node js for use with code-server IDE
RUN apt-get update && \
apt-get install libssl1.0-dev node-gyp nodejs-dev nodejs=8.10* npm -y && \
pip install tornado==5.1.1

# Adding nbserverproxy for jupyter and jupyterlab
RUN pip install nbserverproxy python-language-server flake8 autopep8 && \
  jupyter serverextension enable --py --sys-prefix nbserverproxy && \
  jupyter labextension install jupyterlab-server-proxy


RUN chown -R ubuntu:ubuntu /home/ubuntu/.config


#### Installing Notebooks,Workspaces,IDEs,etc ####


# Clone in workspaces install scripts
# Add workspace configuration files
RUN mkdir -p /var/opt/workspaces && \
cd /tmp && wget -q https://github.com/dominodatalab/workspace-configs/archive/2019q2-v1.3.zip && unzip 2019q2-v1.3.zip  && cp -Rf workspace-configs-2019q2-v1.3/. /var/opt/workspaces && \
rm -rf /var/opt/workspaces/workspace-logos && rm -rf /tmp/workspace-configs-2019q2-v1.3


 # #add update .Rprofile with Domino customizations
RUN \
mv /var/opt/workspaces/rstudio/.Rprofile /home/ubuntu/.Rprofile && \
chown ubuntu:ubuntu /home/ubuntu/.Rprofile

# # # # #Install Rstudio from workspaces
RUN \
chmod +x /var/opt/workspaces/rstudio/install && sleep 2 && \
/var/opt/workspaces/rstudio/install

# # # # # #Install Jupyterlab from workspaces
 RUN chmod +x /var/opt/workspaces/Jupyterlab/install && sleep 2 && \
 /var/opt/workspaces/Jupyterlab/install
 
# # # #Install Jupyter from workspaces
RUN chmod +x /var/opt/workspaces/jupyter/install && sleep 2 && \
 /var/opt/workspaces/jupyter/install


##Install jupyter-tensorboard from workspaces
RUN chmod +x /var/opt/workspaces/jupyter-tensorboard/install && sleep 2 && \
 /var/opt/workspaces/jupyter-tensorboard/install

# # #Install vscode from workspaces
RUN \
pip install git+git://github.com/ChuckRIHead/jupyter_codeserver_proxy-.git && \
chmod +x /var/opt/workspaces/vscode/install && sleep 2 && \
/var/opt/workspaces/vscode/install


#Provide Sudo in container
RUN echo "ubuntu    ALL=NOPASSWD: ALL" >> /etc/sudoers