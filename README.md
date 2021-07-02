# Open Data Cube (ODC) VA Cube Notebooks
The ODC VA Cube Notebooks are for the Virginia Open Data Cube project.

This repository includes several example notebooks in the `./notebooks`
directory. We suggest starting with
[VA_Riparian_Buffer_Landsat_GEE.ipynb](https://github.com/ceos-seo/odc-colab/blob/master/notebooks/VA_Riparian_Buffer_Landsat_GEE.ipynb).

Some notebooks - including the one suggested above - make use of Google Earth Engine data. You must be registered as an Earth Engine developer. If not, you may submit an [application to Google](https://signup.earthengine.google.com/). These notebooks make use of the CEOS ODC-GEE project which can be found here: [https://github.com/ceos-seo/odc-gee](https://github.com/ceos-seo/odc-gee).

TODO: Explain how to set GEE credentials.

<!-- They will require some user interaction for Google authentication, and the user needs to be registered as an Earth Engine developer.-->

**Note:** The `notebooks` use global datasets obtained from GEE
using [ODC-GEE real-time indexing
capabilities](https://github.com/ceos-seo/odc-gee#real-time-indexing).
ODC products that retrieve data from GEE are suffixed with `_google`. Other GEE datasets may also be used by
including an `asset` parameter in the `dc.load` as shown in the README of the
ODC-GEE project.

## Notebooks

The notebooks currently in the `notebooks/dev` directory are from the CEOS ODC-Colab project - an initiative to demonstrate ODC on Google Colab (see [here](https://github.com/ceos-seo/odc-colab)). These notebooks will not appear in the production (`prod`) environment.
