# Datasets Overview

Below is a summary of the details about each ODC product that should be available to these notebooks. The products suffixed with `_google` are GEE products.

| name                | description                                                        | area |crs       | resolution          |
|---------------------|--------------------------------------------------------------------|------|-----------|---------------------|
| ls5_l2_c2           | Landsat 5 Collection 2 Level 2 Surface Reflectance from S3         | Virginia | EPSG:4326 | 30 meters per pixel |
| ls7_l2_c1_t1_google | Landsat 7 Collection 1 Level 2 Surface Reflectance Tier 1 from GEE | World    | EPSG:4326 | 30 meters per pixel |
| ls7_l2_c1_t2_google | Landsat 7 Collection 1 Level 2 Surface Reflectance Tier 2 from GEE | World    | EPSG:4326 | 30 meters per pixel |
| ls7_l2_c2           | Landsat 7 Collection 2 Level 2 Surface Reflectance from S3         | Virginia | EPSG:4326 | 30 meters per pixel |
| ls8_l2_c1_t1_google | Landsat 8 Collection 1 Level 2 Surface Reflectance Tier 1 from GEE | World    | EPSG:4326 | 30 meters per pixel |
| ls8_l2_c1_t2_google | Landsat 8 Collection 1 Level 2 Surface Reflectance Tier 2 from GEE | World    | EPSG:4326 | 30 meters per pixel |
| ls8_l2_c2           | Landsat 8 Collection 2 Level 2 Surface Reflectance from S3         | Virginia | EPSG:4326 | 30 meters per pixel |
| s1_grd_google       | Sentinel-1 GRD from GEE                                            | World    | EPSG:4326 | 10 meters per pixel |

So in summary, data included is:
* **Landsat 5/7/8 Level 2 Colelction 2 data from S3** This data requires the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables to be set. Normal AWS S3 data transfer charges apply to these products.
* **Landsat 7/8 Level 2 Collection 1 data from GEE** Loading from these products is preferred for cost savings but not for datasets that are larger than memory or datasets for which a good data througput is needed. The Tier 1 and 2 data are separate products (e.g. `ls8_l2_c1_t1_google` and `ls8_l2_c1_t2_google`), so for example if all Landsat 8 Level 2 Collection 1 data for a spatiotemporal area needs to be loaded, then 2 `load()` calls have to happen with the same parameters except `product`, then the data from both products must be combined with `xarray.merge()`.
