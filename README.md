# Open Data Cube (ODC) VA Cube Notebooks

The ODC VA Cube Notebooks are Jupyter Notebooks for the Virginia Open Data Cube project.

For an overview of the available notebooks, see the [Notebooks Overview](docs/notebooks_overview.md) document.

## Installation
-------

First follow the instructions in the [Docker Installation Guide](https://github.com/ceos-seo/data_cube_ui/blob/master/docs/docker_install.md) if you do not have Docker installed yet.

Follow the instructions in the [Open Data Cube Database Installation Guide](https://github.com/ceos-seo/data_cube_ui/blob/master/docs/odc_db_setup.md) to setup the Open Data Cube (ODC) database.

Follow the instructions in the [Operation Manual](docs/notebooks_operation_manual.md) to set up and operate the Jupyter Notebook environment.

Some notebooks - generally prefixed with `_GEE` - make use of Google Earth Engine data. You must be registered as an Earth Engine developer. If not, you may submit an [application to Google](https://signup.earthengine.google.com/). These notebooks make use of the CEOS ODC-GEE project which can be found here: [https://github.com/ceos-seo/odc-gee](https://github.com/ceos-seo/odc-gee).

You will also need [GEE service account credentials](https://developers.google.com/earth-engine/guides/service_account) - specifically the private key JSON file.
