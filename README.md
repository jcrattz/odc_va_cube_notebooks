# Open Data Cube (ODC) VA Cube Notebooks

The ODC VA Cube Notebooks are Jupyter Notebooks for the Virginia Open Data Cube project.

For an overview of the available notebooks, see the [Notebooks Overview](https://github.com/jcrattz/odc_va_cube_notebooks/blob/master/docs/notebooks_overview.md) document.

For an overview of the available datasets, see the [Datasets Overview](https://github.com/jcrattz/odc_va_cube_notebooks/blob/master/docs/datasets_overview.md)

## Installation
-------

First follow the instructions in the [Docker Installation Guide](https://github.com/ceos-seo/data_cube_ui/blob/master/docs/docker_install.md) if you do not have Docker installed yet.

Follow the instructions in the [Open Data Cube Database Installation Guide](https://github.com/ceos-seo/data_cube_ui/blob/master/docs/odc_db_setup.md) to setup the Open Data Cube (ODC) database.

Follow the instructions in the [Operation Manual](https://github.com/jcrattz/odc_va_cube_notebooks/blob/master/docs/notebooks_operation_manual.md) to set up and operate the Jupyter Notebook environment.

Some notebooks - generally prefixed with `_GEE` - make use of Google Earth Engine (GEE) data. You must be registered as an Earth Engine developer. If not, you may submit an [application to Google](https://signup.earthengine.google.com/). These notebooks make use of the CEOS ODC-GEE project which can be found here: [https://github.com/ceos-seo/odc-gee](https://github.com/ceos-seo/odc-gee).

You will also need [GEE service account credentials](https://developers.google.com/earth-engine/guides/service_account) - specifically the private key JSON file.

## Adding New GEE Datasets as ODC Products
-------

To use a GEE dataset from the [Earth Engine Data Catalog[(https://developers.google.com/earth-engine/datasets/), a new product must be created using the `new_product` command. Format: `new_product --asset <asset_id> <product_name.yaml>` where the `asset_id` is provided in the "Earth Engine Snippet" string on the dataset's page on the catalog and `product_name.yaml` is the path to the output YAML file containing the ODC product definition. For example, to index [Landsat 8 Level 2 Collection 2 Tier 1](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C02_T1_L2?hl=en) data: `new_product --asset LANDSAT/LC08/C02/T1_L2 ls8_l2_c2_gee.yaml`. The full process is as follows:

1. Run the `new_product` command to create the product definition.
2. Reformat the product definition to match a standard format, such as [this one](https://github.com/ceos-seo/odc_manual_indexer/blob/develop/prod_defs/Landsat/collection_2/ls8_l2_c2.yaml).
3. Change the `aliases` field for the measurements as desired. Do NOT change the `name` field of any measurement - creating the product will fail if the `name` fields are changed.
4. Run `datacube product add <path-to-product-definition-file>` to add the product.

Notably, you will need to add a `storage` section with `crs` and `resolution` entries to avoid having to specify the `output_crs` and `resolution` each time data is loaded from the product.

After adding the product, it is a **non-indexed GEE product**. It must be loaded using a modified version of the `datacube.Datacube` class, as will be shown later.

Alternatively, the data can be indexed using the `index_gee` command, making it an **indexed GEE product**, but **this is deprecated**. Format: `index_gee --asset <asset_id> --product <product_name> [--latitude (lat1, lat2) --longitude (lon1, lon2) --time (YYYY-MM-DD, YYYY-MM-DD) --region <region_name>]` (for information on the optional arguments and others not listed here, run `index_gee --help`). For example, to index [Landsat 8 Level 2 Collection 2 Tier 1](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C02_T1_L2?hl=en) data for the United States: `index_gee --asset LANDSAT/LC08/C02/T1_L2 --product <product_name> --latitude (25.3168, 49.4885) --longitude (-125.2052, -66.6657)`. Data for these products can be loaded by the normal `datacube.Datacube` class.

## Using GEE vs non-GEE Data
-------

To load data from non-GEE products, use the `datacube.Datacube` class as always:

```
from datacube import Datacube
dc = datacube.Datacube()
```

To load data from GEE products, use the `odc_gee.earthengine.Datacube` class:

```
from odc_gee.earthengine import Datacube as GEE_Datacube
dc = GEE_Datacube()
```

To load data from indexed GEE products (remember **this is deprecated**), use the `datacube.Datacube` class as shown above.

## GEE versus Alternative Datasources

These are the benefits and penalties of loading data from Google Earth Engine through the ODC-GEE module instead of from other datasources such as S3.

Benefits:
1. Data does not need to be indexed before loading, which allows new datasets to be added and queried quickly, which allows faster prototyping. This also results in a much smaller ODC index database.
2. There is no cost to loading data from GEE.

Penalties:
1. Data has a very low throughput - just a few MiB per second.
2. (Advanced) Using `dask_chunks` in the `load()` call does not work as expected. Normally, loads specifying the `dask_chunks` parameters will not immediately load data - instead creating the plan to load data with Dask. Instead, the data immediately begins loading as if `dask_chunks` was not specified. This can be problematic for datasets that are larger than the amount of available memory. This problem does not occur when loading data using the normal `datacube.Datacube` class.
