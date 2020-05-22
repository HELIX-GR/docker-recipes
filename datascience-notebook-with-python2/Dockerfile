FROM athenarc/singleuser-notebook-with-python2:0.9a

RUN conda install --yes -p $CONDA_DIR/envs/python2/ scipy==1.2.1 scikit-learn==0.20.3 numpy==1.16.5 pandas matplotlib==2.2.5 && \
    conda clean --all -f -y

# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN MPLBACKEND=AGG $CONDA_DIR/envs/python2/bin/python -c "import matplotlib.pyplot"  
