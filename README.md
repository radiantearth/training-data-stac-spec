# Training Data STAC Profile

The Training Data STAC Profile is an extension of the SpatioTemporal Asset Catalog core to handle 'training data' assets. 
Training data is earth observation imagery (and potentially other types of assets) with associated labels that describe what 
is in the imagery. Labels typically describe a set of geospatial 'things' that are contained in the image, be it forests, 
roads, ships or walmarts. The training data specification is agnostic as to what is actually labeled - the structure specified 
can be used to describe anything that can be identified on the earth. The primary use of training data is as input in to 
Machine Learning models, training them to automatically recognize or segment the same types of objects in new imagery. But the 
labels can be used for a variety of purposes. 

## Training Data STAC Item

The core of the Training Data profile is a STAC Training Data Item that extends the [core STAC definition](https://github.com/radiantearth/stac-spec/blob/master/json-spec/json-spec.md). 
Some of the meanings have been tweaked and refined. There are two required assets for a Training Data Item - it should have a 
source asset that the labels are created from, and
    
| element         | type info       | name                       | description       | 
|-----------------|-----------------|----------------------------|--------------------------------------------------------------------------------------------------| 
| id              | string          | Training Data Item ID                | The ID of the Item assigned by the Labels Creator                                                                                   | 
| geometry        | geojson         | Geometry                   | A polygon of the area of the image that labels are valid for, in lat/long (EPSG 4326),                                       |
| datetime                   | date and time   | Date and Time                  | The searchable date/time of the source asset for the labels, in UTC (Formatted in RFC 3339)                          | 
| links           | array           | Resource Links             | Dict of link objects to resources and related URLs (self required)                                                                 |
| assets          | array           | Assets                   | Dict of asset objects that can be be download: 'source-asset' and 'labels' required, with thumbnail strongly recommended)       |
| td:contributor | string         | Contributor           |   The name of the contributor who created the Training Data Item   |
| td:method      | string         |  Method                | The method of gathering the training data - from an image, from ground truth, etc (TODO: pick the possible values) |
| td:task_type  | string (enum) | Task             |  One of 'Tile Classification', 'Object Detection', 'Segmentation', or 'Other'
| provider        | string          | Provider     (optional)    | The provider of the labels (image provider is in the input-asset                                                        |
| license         | string          | Data License (optional)    | Item's license name based on SPDX License List or following guidelines for non-SPDX licenses         |

