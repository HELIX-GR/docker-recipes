FROM athenarc/singleuser-notebook-with-python2:0.9a

RUN $CONDA_DIR/envs/python2/bin/pip install datadiff

RUN conda install --yes -p $CONDA_DIR/envs/python2/ numpy pandas matplotlib
# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN MPLBACKEND=Agg $CONDA_DIR/envs/python2/bin/python -c "import matplotlib.pyplot"

ENV EBAS_VERSION "3.2.2"
ENV EBAS_DIST_URL "https://git.nilu.no/ebas/ebas-io/-/raw/master/dist/ebas_io-${EBAS_VERSION}-py2.7.egg"
RUN $CONDA_DIR/envs/python2/bin/python -m easy_install ${EBAS_DIST_URL}
