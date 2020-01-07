FROM ubuntu:18.04
LABEL maintainer="Domino Data Lab <support@dominodatalab.com>"

#### Utilities required by Domino ####
ENV DEBIAN_FRONTEND noninteractive

#create a Ubuntu User
RUN \
  groupadd -g 12574 ubuntu && \
  useradd -u 12574 -g 12574 -m -N -s /bin/bash ubuntu && \

  # UPDATE, UPGRADE, ADD repositories
  apt-get update -y && \
  apt-get -y install software-properties-common && \
  apt-get -y upgrade && \
  # CONFIGURE locales
  apt-get install -y locales && \
  locale-gen en_US.UTF-8 && \
  dpkg-reconfigure locales && \
  # INSTALL common
  apt-get -y install build-essential wget sudo curl apt-utils net-tools libzmq3-dev ed git ca-certificates iputils-ping dnsutils telnet apt-transport-https vim python3-pip jq && \
  apt-get install openjdk-8-jdk -y && \
  update-alternatives --config java && \
  echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> /home/ubuntu/.domino-defaults && \
  apt-get -y install libssl-dev libxml2-dev libxt-dev libssh2-1-dev libcurl4-openssl-dev libsasl2-dev libssl-dev && \
  #apt AWS CLI
  apt-get install awscli -y  && \
  # ADD SSH start script for ssh'ing to run container in Domino <v4.0
  apt-get install openssh-server -y && \
  mkdir -p /scripts && \
  printf "#!/bin/bash\\nservice ssh start\\n" > /scripts/start-ssh && \
  chmod +x /scripts/start-ssh && \
  
  echo 'export PYTHONIOENCODING=utf-8' >> /home/ubuntu/.domino-defaults && \
  echo 'export LANG=en_US.UTF-8' >> /home/ubuntu/.domino-defaults && \
  echo 'export JOBLIB_TEMP_FOLDER=/tmp' >> /home/ubuntu/.domino-defaults && \
  echo 'export LC_ALL=en_US.UTF-8' >> /home/ubuntu/.domino-defaults && \
  locale-gen en_US.UTF-8 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*
    
ENV LANG en_US.UTF-8
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

###### Install R #####
ENV R_BASE_VERSION 3.6.2

RUN \ 
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
    add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/' && \
    apt-get update -y && \
    apt-get install \ 
    r-base=${R_BASE_VERSION}-* \
  r-base-dev=${R_BASE_VERSION}-* -y && \
#dependencies of various R packages
    apt-get install -y libcairo2-dev  libxt-dev libgmp3-dev jags libgsl0-dev libx11-dev mesa-common-dev libglu1-mesa-dev libmpfr-dev libfftw3-dev libtiff5-dev libiodbc2-dev libudunits2-dev libopenmpi-dev libmysqlclient-dev -y && \
#required for rJava
    export LD_LIBRARY_PATH=/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server && \
    echo "export LD_LIBRARY_PATH=/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server:\${LD_LIBRARY_PATH:-}" >> /home/ubuntu/.domino-defaults && \
    R CMD javareconf && \
# INSTALL R packages required by Domino
    R -e 'options(repos=structure(c(CRAN="http://cran.us.r-project.org"))); install.packages(c( "plumber","yaml", "shiny"))' && \
#install R packages
    apt-get install libgdal-dev -y && \
    R -e "install.packages('rgdal',repos='https://cran.revolutionanalytics.com/')" && \
    R -e 'options(repos=structure(c(CRAN="http://cran.us.r-project.org"))); install.packages(c( "devtools", "stringi", "httpuv","RJSONIO", "Cairo", "jsonlite","RJDBC"))' && \
    R --no-save -e 'install.packages(c("keras","sparklyr","mongolite","forecast","abind", "acepack", "ade4", "akima", "alr3","ape", "argparse", "assertthat", "aws.s3", "aws.signature", "backports", "base64", "base64enc", "BH", "bibtex", "biglm", "bit", "bit64", "bitops", "BradleyTerry2", "brew", "brglm", "BTYD", "bvls", "car", "caret", "caTools",  "chron", "circular", "clue", "clusterGeneration", "coda", "coin", "colorRamps", "colorspace", "combinat", "contfrac", "corpcor", "corrgram", "corrplot", "crayon", "curl", "data.table", "DBI", "deldir", "dendextend", "DEoptimR", "deSolve", "devtools", "dichromat", "digest", "diptest", "dmt", "doMC", "doParallel", "doRedis", "doRNG", "dynlm", "e1071", "earth", "elasticnet", "ellipse", "elliptic", "evaluate", "expm", "extrafont", "extrafontdb", "fastICA", "fastmatch", "fBasics", "ff", "findpython", "flexmix", "FMStable", "foreach", "forecast", "formatR", "Formula", "fpc", "fracdiff", "gains", "gam", "gbm", "gclus", "gdata", "gee", "geepack", "geiger", "getopt", "ggfortify", "git2r", "glmnet", "gmp", "gplots", "googlesheets","gridExtra", "gss", "gtable", "gtools", "h2o", "hexbin", "hflights", "highlight", "highr", "Hmisc", "htmltools", "htmlwidgets", "httpuv", "httr", "hypergeo", "igraph", "igraphdata", "inline", "intervals", "ipred", "IRdisplay", "IRkernel", "iterators", "itertools", "jpeg", "jsonlite", "kernlab", "KFAS", "klaR", "knitr", "labeling", "Lahman", "lars", "lasso2", "lattice", "latticeExtra", "lava", "lazyeval", "lda", "LDPD", "leaflet","leaps", "LearnBayes", "lme4", "lmtest", "locfit", "logspline", "lokern", "lpSolve", "lubridate", "magrittr", "mailR", "mapproj", "maps", "maptools", "markdown", "MARSS", "MatrixModels", "matrixStats", "mclust", "mda", "memoise", "mgcv", "mice", "microbenchmark", "mime", "miniUI", "minqa", "misc3d", "mix", "mixtools", "mlbench", "mnormt", "modeltools", "msm", "multcomp", "munsell", "mvtnorm", "ncbit", "nleqslv", "nloptr", "NLP", "nnls", "nor1mix", "numDeriv", "nws", "OAIHarvester", "openssl", "pander", "party", "pbkrtest", "PerformanceAnalytics", "permute", "phangorn", "pheatmap", "phylobase", "picante", "pipeR", "pixmap", "pkgmaker", "plotly", "plotmo", "plotrix", "pls", "plyr", "png", "polspline", "PortfolioAnalytics", "ppcor", "prabclus", "pROC", "prodlim", "profileModel", "proto", "proxy", "psych", "qap", "quadprog", "Quandl", "quantmod", "quantreg", "R2jags", "R2WinBUGS", "R6", "randomForest", "RANN", "rbenchmark", "R.cache", "RColorBrewer", "Rcpp", "RcppArmadillo", "RcppEigen", "RcppGSL", "RcppRoll", "RCurl", "R.devices", "registry", "relations", "repr", "reshape", "reshape2", "R.filesets", "RGCCA", "rgl", "RGraphics", "R.huge", "ridge", "rjags", "rJava", "rjson", "RJSONIO", "rlecuyer", "rmarkdown", "R.methodsS3", "Rmpfr", "Rmpi", "rms", "rngtools", "robustbase", "ROCR", "R.oo", "Rook", "roxygen2", "RPMM", "rprojroot", "rredis", "R.rsp", "Rserve", "RSQLite", "rstan", "rstudioapi", "Rttf2pt1", "RUnit", "R.utils", "rversions", "rzmq", "sandwich", "scales", "scatterplot3d", "segmented", "seriation", "sets", "sfsmisc", "shinydashboard", "shinyjs", "sitools", "sjmisc", "sjPlot", "slackr", "slam", "sm", "snow", "SnowballC", "snowfall", "sourcetools", "sp", "spam", "SparseM", "spdep", "spls", "stabledist", "stargazer", "statmod", "stringi", "strucchange", "subplex", "survey", "tables", "TeachingDemos", "testthat", "TH.data", "tiff", "timeDate", "timeSeries", "tm", "topicmodels", "trimcluster", "tripack", "tseries", "TSP", "TTR", "tweedie", "uuid", "vcd", "vegan", "VGAM", "VGAMdata", "viridis", "whisker", "xgboost", "XLConnect", "XLConnectJars", "xlsx", "xlsxjars", "XML", "xml2", "xtable", "xts", "zoo", "base", "boot", "class", "cluster", "codetools", "compiler", "datasets", "foreign", "graphics", "grDevices", "grid", "KernSmooth", "lattice", "MASS", "Matrix", "methods", "mgcv", "nlme", "nnet", "parallel", "rpart", "spatial", "splines", "stats", "stats4", "survival", "tcltk", "tools", "utils"),repos="https://cran.revolutionanalytics.com/",clean=TRUE,Ncpus = getOption("Ncpus", 4L))' && \
    R --no-save -e "install.packages(c('tidyverse','domino','feather','choroplethr', 'choroplethrMaps','DT','ggvis'), repos='https://cran.revolutionanalytics.com/',clean=TRUE,Ncpus = getOption('Ncpus', 4L))" && \
    rm -rf /usr/local/lib/R/site-library/XLConnect/unitTests/resources/testBug61.xlsx && \
    chown -R ubuntu:ubuntu /usr/local/lib/R/site-library && \
#Cleanup
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -Rf /tmp/*


######Install Python 3.7.4 and Miniconda######
#Inspriration: https://github.com/jupyter/docker-stacks/blob/master/base-notebook/Dockerfile

# https://repo.continuum.io/miniconda/
ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH 
ENV MINICONDA_VERSION 4.7.12.1     
ENV MINICONDA_MD5 81c773ff87af5cfac79ab862942ab6b3
ENV PYTHON_VER 3.7

#set env variables so they are available in Domino runs/workspaces
RUN \
    echo 'export CONDA_DIR=/opt/conda' >> /home/ubuntu/.domino-defaults && \
    echo 'export PATH=$CONDA_DIR/bin:$PATH' >> /home/ubuntu/.domino-defaults && \
    echo 'export PATH=/home/ubuntu/.local/bin:$PATH' >> /home/ubuntu/.domino-defaults && \

#Install Python and Mini-conda
    cd /tmp && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh && \
    echo "${MINICONDA_MD5} *Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh" | md5sum -c - && \
    /bin/bash Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh -f -b -p $CONDA_DIR && \
    rm Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh && \
#make conda folder permissioned for ubuntu user
    chown ubuntu:ubuntu -R $CONDA_DIR && \
# Use Mini-conda's pip
    ln -s $CONDA_DIR/bin/pip /usr/bin/pip && \
# Use Mini-conda's python   
    ln -s $CONDA_DIR/bin/python /usr/local/bin/python && \
    ln -s $CONDA_DIR/anaconda/bin/python /usr/local/bin/python3  && \
#Set permissions
    chown -R ubuntu:ubuntu  $CONDA_DIR && \
#Upgrade Pip
    pip install --upgrade pip && \

#Add various package dependencies and useful libraries
    apt-get update && \
    apt-get install -y libhdf5-dev libyaml-dev pkg-config libfuse-dev cups libcups2-dev python-gi python-gi-cairo python3-gi python3-gi-cairo gir1.2-gtk-3.0 python-mvpa2 libsmbclient-dev libcups2-dev python-debian python-igraph swig  && \

###Install Domino Dependencies ####  
#packages used for model APIs and Apps
    $CONDA_DIR/bin/conda install -c conda-forge uWSGI==2.0.18 && \
    pip install Flask==1.0.2 Flask-Compress==1.4.0 Flask-Cors==3.0.6 jsonify==0.5 && \

### Install packages used in Domino quick-start project
    pip install git+https://github.com/dominodatalab/python-domino.git && \

## Additional packages in full anaconda 5.3.1 but not mini-conda 4.7.12.1
    pip install \
    alabaster==0.7.11 \
    appdirs==1.4.3 \
    astroid==2.0.4 \
    astropy==3.0.4 \
    atomicwrites==1.2.1 \
    Automat==0.7.0 \
    Babel==2.6.0 \
    backports.shutil-get-terminal-size==1.0.0 \
    beautifulsoup4==4.6.3 \
    bitarray==0.8.3 \
    bkcharts==0.2 \
    # 0.11.3 not on pypi so reverting to 0.10.1
    blaze==0.10.1 \
    bokeh==0.13.0 \
    boto==2.49.0 \
    Bottleneck==1.2.1 \
    click==6.7 \
    cloudpickle==0.5.5 \
    # 1.2.2 not on pypi so reverting to 1.2.1
    clyent==1.2.1 \
    colorama==0.3.9 \
    #not required
    constantly==15.1.0 \
    contextlib2==0.5.5 \
    cycler==0.10.0 \
    Cython==0.28.5 \
    cytoolz==0.9.0.1 \
    dask==2.9.0 \
    #0.5.4 not on pypi so reverting to 0.5.2
    datashape==0.5.2 \
    distributed==1.23.1 \
    docutils==0.14 \
    et-xmlfile==1.0.1 \
    fastcache==1.0.2 \
    filelock==3.0.8 \
    gevent==1.3.6 \
    glob2==0.6 \
    greenlet==0.4.15 \
    h5py==2.8.0 \
    heapdict==1.0.0 \
    html5lib==1.0.1 \
    hyperlink==18.0.0 \
    imageio==2.4.1 \
    imagesize==1.1.0 \
    incremental==17.5.0 \
    isort==4.3.4 \
    itsdangerous==0.24 \
    jdcal==1.4 \
    jeepney==0.3.1 \
    keras==2.3.1 \
    keyring==13.2.1 \
    kiwisolver==1.0.1 \
    lazy-object-proxy==1.3.1 \
    llvmlite==0.24.0 \
    locket==0.2.0 \
    lxml==4.2.5 \
    matplotlib==2.2.3 \
    mccabe==0.6.1 \
    #1.0.4 not available using 1.0.5
    mpmath==1.0.0 \
    msgpack==0.5.6 \
    multipledispatch==0.6.0 \
    #not required. Only used with anaconda
    networkx==2.1 \
    nltk==3.3 \
    nose==1.3.7 \
    numba==0.39.0 \
    numexpr==2.6.8 \
    numpy==1.18.0 \
    numpydoc==0.8.0 \
    # # 0.5.1 not on pypi so reverting to 0.5.0
    odo==0.5.0 \
    olefile==0.46 \
    openpyxl==2.5.6 \
    packaging==17.1 \
    pandas==0.23.4 \
    partd==0.3.8 \
    path.py==11.1.0 \
    pathlib2==2.3.2 \
    patsy==0.5.0 \
    pep8==1.7.1 \
    Pillow==5.2.0 \
    pkginfo==1.4.2 \
    pluggy==0.7.1 \
    ply==3.11 \
    psutil==5.4.7 \
    py==1.6.0 \
    pyasn1==0.4.4 \
    pyasn1-modules==0.2.2 \
    pycodestyle==2.4.0 \
    pycrypto==2.6.1 \
    pycurl==7.43.0.2 \
    pyflakes==2.0.0 \
    pylint==2.1.1 \
    pyparsing==2.2.0 \
    pytest==3.8.0 \
    pytest-arraydiff==0.2 \
    pytest-astropy==0.4.0 \
    pytest-doctestplus==0.1.3 \
    pytest-openfiles==0.3.0 \
    pytest-remotedata==0.3.0 \
    pytz==2018.5 \
    PyWavelets==1.0.0 \
    PyYAML==3.13 \
    QtAwesome==0.4.4 \
    QtPy==1.5.0 \
    rope==0.11.0 \
    scikit-image==0.14.0 \
    scikit-learn==0.19.2 \
    scipy==1.1.0 \
    seaborn==0.9.0 \
    SecretStorage==3.1.0 \
    service-identity==17.0.0 \
    simplegeneric==0.8.1 \
    singledispatch==3.4.0.3 \
    snowballstemmer==1.2.1 \
    sortedcollections==1.0.1 \
    sortedcontainers==2.0.5 \
    Sphinx==1.7.9 \
    sphinxcontrib-websupport==1.1.0 \
    spyder==3.3.1 \
    spyder-kernels==0.2.6 \
    SQLAlchemy==1.2.11 \
    statsmodels==0.9.0 \
    sympy==1.2 \
    tables==3.6.1 \
    tblib==1.3.2 \
    tensorflow-gpu==2.0.0 \
    toolz==0.9.0 \
    Twisted==18.7.0 \
    unicodecsv==0.14.1 \
    Werkzeug==0.14.1 \
    wrapt==1.11.2 \
    xlrd==1.1.0 \
    XlsxWriter==1.1.0 \
    xlwt==1.3.0 \
    zict==0.1.3 \
    zope.interface==4.5.0 \
    ###Install addition useful Data Science Python Packages
    cairocffi==1.1.0 \
    colorama==0.3.9 \
    jaydebeapi==1.1.1 \
    jpype1==0.7.1 \
    bson==0.5.8 \
    pypandoc==1.4 \
    ggplot==0.11.5 \
    mpltools==0.2.0 \
    websocket==0.2.1 && \     

    apt-get install libgmp-dev libmpfr-dev libmpc-dev -y && \
    pip install gmpy2==2.0.8 && \

    $CONDA_DIR/bin/conda install mkl_fft==1.0.4 mkl_random==1.0.1 && \
    
    apt-get install unixodbc-dev -y && \
    pip install pyodbc==4.0.27 && \
    
    apt-get install -y pandoc && \
#configure matplotlib
    mkdir -p /home/ubuntu/.config/matplotlib && \
    echo "backend : Cairo" > /home/ubuntu/.config/matplotlib/matplotlibrc  && \
    sed -i -e 's/backend      : qt5agg/backend      : Cairo/g' $CONDA_DIR/lib/python$PYTHON_VER/site-packages/matplotlib/mpl-data/matplotlibrc && \

#Kerberos
    apt-get install krb5-kdc krb5-admin-server -y && \
#clean up
    find /opt/conda/ -follow -type f -name '*.a' -delete && \
    find /opt/conda/ -follow -type f -name '*.js.map' -delete && \
    $CONDA_DIR/bin/conda clean -afy && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -Rf /tmp/*

### Install drivers for common data source connections #####
#SQL 
RUN \
    apt-get update -y && apt-get install tdsodbc -y && \
    apt-get install -y libodbc1 unixodbc freetds-common freetds-dev && \
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
    rm -rf /tmp/* && \
# #Oracle
# #ROracle & PyOracle
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
    R CMD INSTALL --configure-args='--with-oci-inc=/opt/oracle/instantclient_12_1/sdk/include --with-oci-lib=/opt/oracle/instantclient_12_1' ROracle_1.3-1.tar.gz && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip && \
    rm -rf /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip && \
    
# #Install PostgreSQL client
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8 && \
    echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    apt-get update && apt-get -y -q install postgresql-9.3 postgresql-client-9.3 postgresql-contrib-9.3 && \
    rm -rf /var/lib/apt/lists/* && \
    R --no-save -e 'install.packages(c("RPostgreSQL","RODBC","RMySQL","RPostgres"))'


# ####### R KERNEL IN JUPYTER ############

 RUN R --no-save -e 'install.packages("pbdZMQ", repos="https://cran.revolutionanalytics.com/", clean=TRUE)'
 USER ubuntu
 RUN R --no-save -e 'devtools::install_github("IRkernel/IRkernel"); IRkernel::installspec()'
 USER root


# ######Scala Kernel
RUN cd /tmp && wget -q https://downloads.lightbend.com/scala/2.12.6/scala-2.12.6.deb && dpkg -i scala-2.12.6.deb && apt-get update -y && apt-get install scala -y --allow-downgrades && \
 echo 'export SCALA_HOME=/usr/share/scala' >> /home/ubuntu/.domino-defaults && \
 echo 'export PATH=$PATH:$SCALA_HOME/bin:$PATH' >> /home/ubuntu/.domino-defaults && \
 echo 'export PATH=$PATH:/tmp:$PATH' >> /home/ubuntu/.domino-defaults && \
 cd /tmp && curl -L -o coursier https://git.io/coursier && chmod +x coursier && \
 cd /tmp && wget -q https://github.com/almond-sh/almond/archive/v0.1.8.tar.gz && tar -zxvf v0.1.8.tar.gz && mv almond-0.1.8 almond && export SCALA_VERSION=2.12.6 && export ALMOND_VERSION=0.1.8 && ./coursier bootstrap -r jitpack -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION --sources --default=true -o almond-out && ./almond-out --install --global --id scala212 --display-name "Scala (2.12)" && \
# ## SBT
 echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list && \
 apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 && \
 apt-get update -y && \
 apt-get install sbt -y && \
###Julia
rm -rf /usr/bin/julia && \
    cd /home/ubuntu && \
    wget -q https://julialang-s3.julialang.org/bin/linux/x64/1.1/julia-1.1.0-linux-x86_64.tar.gz && \
    tar xzf julia-1.1.0-linux-x86_64.tar.gz && \
    chown -R ubuntu:ubuntu /home/ubuntu/julia-1.1.0 && \
    ln -s /home/ubuntu/julia-1.1.0/bin/julia /usr/bin/julia && \
    rm -rf /home/ubuntu/julia-1.1.0-linux-x86_64.tar.gz && \
    rm -rf /var/lib/apt/lists/* && \
    rm -Rf /tmp/*
 
USER ubuntu
RUN julia -e 'using Pkg; Pkg.update(); Pkg.add("IJulia")'
USER root


#### Installing Notebooks,Workspaces,IDEs,etc ####
# Add workspace install and configuration scripts
RUN \
    cd /tmp && \
    wget -q https://github.com/dominodatalab/workspace-configs/archive/2019q4-v1.zip && \
    unzip 2019q4-v1.zip && \
    cp -Rf workspace-configs-2019q4-v1/. /var/opt/workspaces && \
    rm -rf /var/opt/workspaces/workspace-logos && rm -rf /tmp/workspace-configs-2019q4-v1 && \

# # # # #Install Rstudio from workspaces
#add update .Rprofile with Domino customizations
    mv /var/opt/workspaces/rstudio/.Rprofile /home/ubuntu/.Rprofile && \
    chown ubuntu:ubuntu /home/ubuntu/.Rprofile && \
#Install Rstudio
    chmod +x /var/opt/workspaces/rstudio/install  && \
    /var/opt/workspaces/rstudio/install && \
    
# # # # #Install Jupyter from workspaces
    chmod +x /var/opt/workspaces/jupyter/install && \
    /var/opt/workspaces/jupyter/install && \

# # # # #Install vscode from workspaces
#Required for VSCode
    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - && \
    apt-get update && \
    apt-get install libssl1.0-dev node-gyp nodejs -y && \
    pip install python-language-server autopep8 flake8 pylint && \
    pip install git+git://github.com/dominodatalab/jupyter_codeserver_proxy-.git && \
#Install VScode
    chmod +x /var/opt/workspaces/vscode/install && \
    /var/opt/workspaces/vscode/install && \
    
# # # # #nstall Jupyterlab from workspaces
    chmod +x /var/opt/workspaces/Jupyterlab/install && \
    /var/opt/workspaces/Jupyterlab/install && \
# Adding jupyter-server-proxy for jupyter and jupyterlab
    pip install jupyter-server-proxy && \
    jupyter labextension install @jupyterlab/server-proxy && \
#   chown -R ubuntu:ubuntu /home/ubuntu/.config

#Clean up
    rm -rf /var/lib/apt/lists/* && \
    rm -Rf /tmp/* && \
#set permissions
    chown -R ubuntu:ubuntu /home/ubuntu/.local/

#### Install CUDA and GPU dependencies #####

#NVIDIA
ENV CUDA_VERSION 10.0.130
ENV CUDA_PKG_VERSION 10-0=$CUDA_VERSION-1


RUN \
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/nvidia/lib:/usr/local/nvidia/lib64:\${LD_LIBRARY_PATH:-} && \
    echo "export LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/nvidia/lib:/usr/local/nvidia/lib64:\${LD_LIBRARY_PATH:-}" >> /home/ubuntu/.domino-defaults && \
    
    export PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:\${PATH:-} && \
    echo "export PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:\${PATH:-}" >> /home/ubuntu/.domino-defaults && \
    
    apt-get update && apt-get install -y --no-install-recommends \
    gnupg2 curl ca-certificates && \
    curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub | apt-key add - && \
    echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list && \
    echo "deb https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get purge --autoremove -y curl && \

# For libraries in the cuda-compat-* package: https://docs.nvidia.com/cuda/eula/index.html#attachment-a
    apt-get install -y --no-install-recommends cuda-cudart-$CUDA_PKG_VERSION cuda-compat-10-0 && \
    ln -s cuda-10.0 /usr/local/cuda && \
    rm -rf /var/lib/apt/lists/*


# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.0 brand=tesla,driver>=384,driver<385 brand=tesla,driver>=410,driver<411"

#RUNTIME
ENV NCCL_VERSION 2.4.8

RUN \
    apt-get update && \
    apt-get install -y --no-install-recommends cuda-libraries-$CUDA_PKG_VERSION cuda-nvtx-$CUDA_PKG_VERSION libnccl2=$NCCL_VERSION-1+cuda10.0 apt-mark hold libnccl2 && \
    rm -rf /var/lib/apt/lists/*
    
    
ENV CUDNN_VERSION 7.6.3.30

RUN \
    apt-get update && \
    apt-get install -y --no-install-recommendslibcudnn7=$CUDNN_VERSION-1+cuda10.0 && \
    apt-mark hold libcudnn7 && \
    rm -rf /var/lib/apt/lists/*
    
#Provide Sudo in container
RUN echo "ubuntu    ALL=NOPASSWD: ALL" >> /etc/sudoers
