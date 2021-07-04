# Notebooks Overview

This document provides an overview of the available notebooks in the `notebooks` directory.

There are several example notebooks in the `notebooks` directory. We suggest starting with [VA_Riparian_Buffer_Landsat_GEE.ipynb](../notebooks/VA_Riparian_Buffer/VA_Riparian_Buffer_Landsat_GEE.ipynb).

The notebooks use global datasets obtained from GEE
using [ODC-GEE real-time indexing capabilities](https://github.com/ceos-seo/odc-gee#real-time-indexing). ODC products that retrieve data from GEE are suffixed with `_google`. Other GEE datasets may also be used by
including an `asset` parameter in the `dc.load` as shown in the README of the
ODC-GEE project.

The notebooks currently in the `notebooks/dev` directory are from the CEOS ODC-Colab project - an initiative to demonstrate ODC on Google Colab (see [here](https://github.com/ceos-seo/odc-colab)). These notebooks will not appear in the production (`prod`) environment.
