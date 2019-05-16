FROM jupyterhub/singleuser:0.9

RUN conda install --yes dask distributed \
    && conda clean --yes --tarballs --index-cache --packages

