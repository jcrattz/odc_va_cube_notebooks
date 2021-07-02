ARG BASE_IMG
FROM ${BASE_IMG}

WORKDIR ${ROOT_DIR}

COPY notebooks notebooks
COPY README.ipynb README.ipynb

USER root
RUN chown -R jovyan ${ROOT_DIR}
COPY odc_gee odc_gee
RUN cd odc_gee; python3 setup.py build && python3 setup.py install
# Set the recently changed or added packages' ownership to jovyan. 
RUN find /env/lib/python3.6/site-packages -group root -mtime -1 -exec chown -R jovyan:users {} +
USER jovyan
