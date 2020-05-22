ARG PFLEXIBLE_VERSION=0.9.0
ARG PFLEXIBLE_PACKAGE_URL=https://bitbucket.org/jfburkhart/pflexible/raw/3f4c992b0088e38de7bff7a86682cbc362f463db/dist/pflexible-0.9.0.zip
ARG NUMPY_VERSION=1.16.5 

# Build module `pflexible`

FROM python:2.7 AS build1

ARG PFLEXIBLE_VERSION
ARG PFLEXIBLE_PACKAGE_URL
ARG NUMPY_VERSION

ADD ${PFLEXIBLE_PACKAGE_URL} /opt
RUN cd /opt && unzip pflexible-${PFLEXIBLE_VERSION}.zip

RUN pip install numpy==${NUMPY_VERSION}

WORKDIR /opt/pflexible-${PFLEXIBLE_VERSION}

RUN python setup.py build
RUN python setup.py bdist_egg

# Build final image

FROM athenarc/datascience-notebook-with-python2:0.9a

ARG PFLEXIBLE_VERSION

RUN conda install --yes -p $CONDA_DIR/envs/python2/ hdbscan==0.8.13 joblib==0.11 basemap netcdf4 && \
    conda clean --all -f -y

RUN $CONDA_DIR/envs/python2/bin/pip install --no-cache-dir datadiff seaborn==0.9.1

COPY --from=build1 /opt/pflexible-${PFLEXIBLE_VERSION}/dist/*.egg ./
RUN $CONDA_DIR/envs/python2/bin/python -m easy_install pflexible-${PFLEXIBLE_VERSION}-py2.7-linux-$(uname -m).egg && \
    rm -v pflexible-*.egg

ENV EBAS_VERSION=3.2.2
ENV EBAS_DIST_URL=https://git.nilu.no/ebas/ebas-io/-/raw/master/dist/ebas_io-${EBAS_VERSION}-py2.7.egg
RUN $CONDA_DIR/envs/python2/bin/python -m easy_install ${EBAS_DIST_URL}
