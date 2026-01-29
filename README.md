# Common Operating Picture (COP) Extension Specification

- **Title:** Common Operating Picture (COP)
- **Identifier:** <https://stac-extensions.github.io/cop/v1.0.0/schema.json>
- **Field Name Prefix:** cop
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @luciocola <https://secure-dimensions.de>

This extension provides fields for documenting Common Operating Picture (COP) information in STAC catalogs. This work is based on AI DGGS pilot with OGC Open Geospatial Consortium. It facilitates the exchange of operational data using Discrete Global Grid Systems (DGGS) for spatial organization, supporting emergency response, defense operations, and real-time situational awareness.

## Background

A Common Operating Picture (COP) is a standardized format for transferring operational data between systems, platforms, and applications. Based on the OGC OWS Context Conceptual Model (12-080r2) and extended to support modern OGC APIs and cloud-native data formats, this extension enables:

- **Standardized Data Exchange**: Consistent format for operational information across OGC Web Services (WMS, WFS, WCS, WMTS, WPS) and OGC APIs (Features, Tiles, Coverages, Processes)
- **Cloud-Native Data Formats**: Support for Analysis Ready Data (ARD), NetCDF, Cloud Optimized GeoTIFF (COG), and other modern formats
- **DGGS-based Spatial Organization**: Uses rHEALPix or other DGGS for spatial indexing
- **Real-time Situational Awareness**: Support for time-sensitive operational data
- **Multi-domain Operations**: Emergency response, defense, disaster management
- **Interoperability**: Seamless exchange across different systems and platforms

## Use Cases

1. **Emergency Response Operations**: Track resources, incidents, and response activities during flooding, wildfires, or natural disasters with vector features and raster elevation/hazard models. Access via OGC API - Features for real-time updates and Cloud Optimized GeoTIFF for rapid terrain visualization
2. **Defense and Security**: Coordinate military operations with spatial and temporal precision using both vector intelligence data and raster imagery/terrain analysis, leveraging Analysis Ready Data (ARD) for immediate exploitation
3. **Disaster Management**: Organize relief efforts using DGGS-based spatial cells, combining vector asset locations with raster damage assessments from COG-formatted satellite imagery
4. **Real-time Sensor Networks**: Integrate sensor data into operational picture, including vector point observations and raster interpolated surfaces stored in NetCDF for multidimensional analysis
5. **Multi-agency Coordination**: Share information across organizational boundaries with appropriate access controls via OGC API standards, supporting both vector features and cloud-native raster datasets
6. **Terrain Analysis**: Distribute elevation models, slope analysis, and other raster-based terrain products for operational planning using Cloud Optimized GeoTIFF for efficient streaming access
7. **Earth Observation Integration**: Incorporate Analysis Ready Data (ARD) from satellite missions with standardized preprocessing and atmospheric correction for immediate operational use

## Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

### Item and Collection Properties

| Field Name              | Type   | Description |
| ----------------------- | ------ | ----------- |
| cop:mission             | string | **RECOMMENDED.** Mission or operation identifier |
| cop:classification      | string | **RECOMMENDED.** Security classification level. One of: `public release`, `internal`, `confidential`, `restricted`, `classified` |
| cop:releasability       | string | Releasability specification (e.g., `1:N` for one-to-many, specific entity/group identifiers) |
| cop:dggs_zone_id        | string | DGGS zone identifier for a single operational area (e.g., rHEALPix cell ID like `R312603625535`) |
| cop:dggs_zone_ids       | [string] | Array of DGGS zone identifiers for collections or items covering multiple zones |
| cop:dggs_center_zone    | string | DGGS zone identifier for the center point of the operational area |
| cop:dggs_crs            | string | DGGS Coordinate Reference System (e.g., `rHEALPix-R12`, `H3-R5`, `S2-L10`) |
| cop:dggs_resolution     | string \| integer | DGGS resolution level (e.g., `12` or `"12"` for rHEALPix-R12) |
| cop:service_provider    | string | Provider of the service or data |
| cop:manifest_ref        | string (URI) | Reference to the master COP manifest |
| cop:volume_of_interest  | Volume Object | 3D volume of interest definition using DGGS zones |
| cop:platform            | string | Platform that captured or generated the data (e.g., satellite name, aircraft, UAV, sensor system) |
| cop:sensor              | string | Sensor or instrument that captured the data |
| cop:software_identifier | string | Software used to create or process the data (e.g., 'QGIS/3.28', 'ArcGIS/10.8') |

### Asset-Level Fields

| Field Name              | Type   | Description |
| ----------------------- | ------ | ----------- |
| cop:asset_type          | string | Type of COP asset. One of: `feature`, `feature-query-result`, `point-of-interest`, `web-service`, `sensor-data`, `imagery`, `other` |
| cop:integrity_hash      | string | Integrity hash for asset verification (format: `algorithm:hash`, e.g., `sha256:abc123...`) |

### Additional Field Information

#### cop:classification

Security classification levels for operational data:

- `public release`: Publicly accessible information
- `internal`: Internal use only
- `confidential`: Confidential operational information
- `restricted`: Highly restricted (e.g., attorney-client privilege, sensitive operations)
- `classified`: Classified information requiring security clearance

#### cop:releasability

Specifies who can access the data:
- `1:N`: One-to-many (broadcast to all authorized parties)
- Entity/group identifiers: Specific organizations or individuals
- Coalition identifiers: Multi-national or multi-agency groups

#### cop:dggs_zone_id and cop:dggs_crs

DGGS (Discrete Global Grid System) fields enable precise spatial organization:
- **cop:dggs_zone_id**: Unique cell identifier for a single zone (e.g., `R312603625535` for rHEALPix)
- **cop:dggs_zone_ids**: Array of zone identifiers for collections or items covering multiple zones
- **cop:dggs_center_zone**: Zone identifier at the center of the area of interest
- **cop:dggs_crs**: CRS specification including resolution (e.g., `rHEALPix-R12`, `H3-R5`, `S2-L10`, `ISEA3H-R12`)
- **cop:dggs_resolution**: Resolution level as integer or string (e.g., `12` or `"12"`)

Supports various DGGS implementations including rHEALPix, H3, S2, ISEA3H, and others.

**Usage Guidelines:**
- Use `cop:dggs_zone_id` for Items representing a single DGGS zone
- Use `cop:dggs_zone_ids` for Collections or Items covering multiple zones (e.g., from AOI corners)
- Use `cop:dggs_center_zone` to identify the central reference point
- Always specify `cop:dggs_crs` when using any DGGS zone fields
- Optionally add `cop:dggs_resolution` for explicit resolution documentation

#### cop:asset_type

Categories of operational assets:

- `feature`: GeoJSON feature or feature collection
- `feature-query-result`: Results from spatial/temporal queries
- `point-of-interest`: Critical locations in operational area
- `web-service`: Traditional OGC web services (WMS, WFS, WCS, WMTS, WPS, CSW)
- `ogc-api`: Modern OGC API endpoints (Features, Tiles, Coverages, Processes, Records, Maps)
- `sensor-data`: Real-time sensor observations
- `imagery`: Satellite, aerial, or drone imagery
- `raster`: Raster datasets including elevation models, analysis results, and gridded data
- `cog`: Cloud Optimized GeoTIFF - web-optimized raster format with internal tiling
- `ard`: Analysis Ready Data - preprocessed satellite imagery ready for analysis
- `netcdf`: Network Common Data Form - multidimensional scientific data
- `zarr`: Zarr format - chunked, compressed, cloud-optimized multidimensional arrays
- `other`: Other asset types

#### cop:integrity_hash

Self-identifying hash following the [Multihash specification](https://github.com/multiformats/multihash), encoded as hexadecimal string with lowercase letters (e.g., `sha256:a1b2c3...`).

#### cop:platform

Identifies the platform that captured or generated the data. Examples:
- Satellite missions: `Sentinel-2A`, `Landsat-8`, `WorldView-3`
- Aircraft: `Boeing 747-SP`, `Cessna 172`
- UAV/Drones: `DJI Phantom 4`, `Fixed-wing UAV`
- Ground systems: `Desktop QGIS`, `Mobile Sensor Array`
- Other: `Ground Station`, `Weather Buoy`

#### cop:sensor

Specifies the sensor or instrument used to capture the data. Examples:
- Satellite sensors: `MSI`, `OLI`, `TIRS`
- Camera systems: `RGB Camera`, `Multispectral Camera`, `Thermal Imaging`
- Software-generated: `QGIS Raster Layer`, `QGIS Vector Layer`
- Other sensors: `LiDAR`, `SAR`, `Hyperspectral Imager`

#### cop:software_identifier

Identifies the software and version used to create or process the data. Format: `SoftwareName/Version`

Examples:
- `QGIS/3.28.1`
- `ArcGIS/10.8.2`
- `GDAL/3.4.1`
- `Python/3.9.7`

#### Volume of Interest Object

Used in `cop:volume_of_interest` field:

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| min_zone    | string | Minimum DGGS zone ID (bottom/lower bound) |
| max_zone    | string | Maximum DGGS zone ID (top/upper bound) |
| resolution  | string | DGGS resolution level |

## Examples

### Example 1: Point of Interest Feature

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json"
  ],
  "type": "Feature",
  "id": "poi-00123",
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-74.0062, 40.7130], [-74.0058, 40.7130], 
                     [-74.0058, 40.7126], [-74.0062, 40.7126], 
                     [-74.0062, 40.7130]]]
  },
  "properties": {
    "datetime": "2025-11-03T09:00:00Z",
    "cop:mission": "Emergency Response Team A",
    "cop:dggs_zone_id": "R312603625535",
    "cop:dggs_crs": "rHEALPix-R12",
    "cop:classification": "public release",
    "cop:releasability": "1:N"
  },
  "assets": {
    "feature_data": {
      "href": "s3://cop-data/features/poi-00123.geojson",
      "type": "application/geo+json",
      "cop:asset_type": "feature",
      "cop:integrity_hash": "sha256:a1b2c3d4e5f6..."
    }
  }
}
```

### Example 2: Raster Data (Elevation Model)

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json",
    "https://stac-extensions.github.io/raster/v1.1.0/schema.json"
  ],
  "type": "Feature",
  "id": "elevation-model-00456",
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-122.5, 37.9], [-122.3, 37.9], 
                     [-122.3, 37.7], [-122.5, 37.7], 
                     [-122.5, 37.9]]]
  },
  "properties": {
    "datetime": "2025-11-27T12:00:00Z",
    "cop:mission": "Disaster Assessment Operation 2025-11",
    "cop:dggs_zone_id": "R315782134567",
    "cop:dggs_crs": "rHEALPix-R12",
    "cop:classification": "public release",
    "cop:platform": "Desktop QGIS",
    "cop:sensor": "QGIS Raster Layer",
    "cop:software_identifier": "QGIS/3.28.1"
  },
  "assets": {
    "raster_data": {
      "href": "https://assets.ogc.secd.eu/cop/rasters/elevation-model-00456.tif",
      "type": "image/tiff; application=geotiff",
      "cop:asset_type": "raster",
      "cop:integrity_hash": "sha256:1a2b3c4d..."
    }
  }
}
```

### Example 3: Cloud Optimized GeoTIFF (COG)

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json",
    "https://stac-extensions.github.io/raster/v1.1.0/schema.json"
  ],
  "type": "Feature",
  "id": "cog-terrain-xyz",
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-120.0, 35.0], [-119.0, 35.0], 
                     [-119.0, 36.0], [-120.0, 36.0], 
                     [-120.0, 35.0]]]
  },
  "properties": {
    "datetime": "2025-12-15T10:30:00Z",
    "cop:mission": "Tactical Terrain Analysis",
    "cop:classification": "internal",
    "cop:platform": "Sentinel-2A",
    "cop:sensor": "MSI"
  },
  "assets": {
    "cog_terrain": {
      "href": "https://storage.cloud.example/terrain/area-xyz.tif",
      "type": "image/tiff; application=geotiff; profile=cloud-optimized",
      "roles": ["data", "visual"],
      "cop:asset_type": "cog",
      "cop:integrity_hash": "sha256:7f8e9a1b2c3d..."
    }
  }
}
```

### Example 4: Analysis Ready Data (ARD)

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json",
    "https://stac-extensions.github.io/eo/v1.1.0/schema.json"
  ],
  "type": "Feature",
  "id": "ard-s2-20251215",
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-121.5, 38.0], [-121.0, 38.0], 
                     [-121.0, 38.5], [-121.5, 38.5], 
                     [-121.5, 38.0]]]
  },
  "properties": {
    "datetime": "2025-12-15T18:45:00Z",
    "cop:mission": "Disaster Assessment - Wildfire Monitoring",
    "cop:classification": "public release",
    "cop:releasability": "1:N",
    "cop:platform": "Sentinel-2B",
    "cop:sensor": "MSI",
    "cop:software_identifier": "ESA-SNAP/9.0"
  },
  "assets": {
    "surface_reflectance": {
      "href": "s3://ard-bucket/sentinel2/L2A/2025/12/15/tile.tif",
      "type": "image/tiff; application=geotiff; profile=cloud-optimized",
      "roles": ["data", "reflectance"],
      "title": "Surface Reflectance ARD",
      "cop:asset_type": "ard",
      "cop:integrity_hash": "sha256:9d8c7b6a5e4f..."
    }
  }
}
```

### Example 5: NetCDF Climate Data

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json",
    "https://stac-extensions.github.io/datacube/v2.2.0/schema.json"
  ],
  "type": "Feature",
  "id": "netcdf-forecast-20251217",
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-180, -90], [180, -90], 
                     [180, 90], [-180, 90], 
                     [-180, -90]]]
  },
  "properties": {
    "datetime": "2025-12-17T00:00:00Z",
    "cop:mission": "Weather Forecast Model Run",
    "cop:classification": "public release",
    "cop:service_provider": "National Weather Service"
  },
  "assets": {
    "forecast_data": {
      "href": "https://data.weather.gov/forecasts/gfs_20251217_00z.nc",
      "type": "application/netcdf",
      "roles": ["data"],
      "title": "GFS Forecast NetCDF",
      "cop:asset_type": "netcdf",
      "cop:integrity_hash": "sha256:3c4d5e6f7a8b..."
    }
  }
}
```

### Example 6: Collection with Multiple DGGS Zones

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json"
  ],
  "type": "Collection",
  "id": "cop-flood-response-2025",
  "title": "Flood Response Operation - 2025 Red River Basin",
  "description": "Common Operating Picture collection for flood response operations covering Red River basin area of interest",
  "license": "proprietary",
  "extent": {
    "spatial": {
      "bbox": [[-97.5, 49.0, -96.5, 50.0]]
    },
    "temporal": {
      "interval": [["2025-01-15T00:00:00Z", "2025-01-20T23:59:59Z"]]
    }
  },
  "properties": {
    "cop:mission": "Red River Flood Response 2025",
    "cop:classification": "internal",
    "cop:releasability": "1:N",
    "cop:dggs_crs": "rHEALPix-R12",
    "cop:dggs_resolution": 12,
    "cop:dggs_zone_ids": ["R312603625535", "R312603625536", "R312603625537", "R312603625544"],
    "cop:dggs_center_zone": "R312603625536"
  },
  "links": [
    {
      "rel": "self",
      "href": "./collection.json",
      "type": "application/json"
    },
    {
      "rel": "item",
      "href": "./flood_extent_jan15.json",
      "type": "application/json"
    },
    {
      "rel": "item",
      "href": "./shelter_locations.json",
      "type": "application/json"
    }
  ]
}
```

### Example 7: OGC API - Features Endpoint

```json
{
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/cop/v1.0.0/schema.json"
  ],
  "type": "Feature",
  "id": "ogc-api-features-incidents",
  "bbox": null,
  "geometry": null,
  "properties": {
    "datetime": "2025-12-17T09:30:00Z",
    "cop:mission": "Emergency Response - Incident Tracking",
    "cop:classification": "internal",
    "cop:service_provider": "Emergency Operations Center"
  },
  "links": [
    {
      "rel": "service-desc",
      "href": "https://api.emergency.gov/ogcapi/features/v1/openapi",
      "type": "application/vnd.oai.openapi+json;version=3.0"
    },
    {
      "rel": "conformance",
      "href": "https://api.emergency.gov/ogcapi/features/v1/conformance",
      "type": "application/json"
    }
  ],
  "assets": {
    "api_endpoint": {
      "href": "https://api.emergency.gov/ogcapi/features/v1/collections/incidents",
      "type": "application/json",
      "roles": ["data", "service"],
      "title": "OGC API - Features: Incident Collection",
      "description": "Real-time incident features via OGC API - Features",
      "cop:asset_type": "ogc-api",
      "cop:integrity_hash": "sha256:5f6a7b8c9d0e..."
    }
  }
}
```

See the [examples directory](examples/) for complete examples including service endpoints and collections.

## Relation Types

The following relation types are recommended for use in COP documents:

| Type   | Description |
| ------ | ----------- |
| about  | Link to the master COP manifest or operational plan |

## Best Practices

1. **DGGS Usage**: 
   - Always specify both `cop:dggs_zone_id` (or `cop:dggs_zone_ids`) and `cop:dggs_crs` when using DGGS-based spatial organization
   - Use `cop:dggs_zone_id` for Items representing a single zone
   - Use `cop:dggs_zone_ids` (array) for Collections or Items covering multiple zones
   - Include `cop:dggs_center_zone` to identify the central reference point
   - Add `cop:dggs_resolution` for explicit resolution documentation
2. **Security Classification**: Set appropriate `cop:classification` and `cop:releasability` for all operational data
3. **Asset Integrity**: Use `cop:integrity_hash` for critical assets to ensure data integrity (prefer BLAKE3 for IPFS/blockchain interoperability)
4. **Manifest References**: Link to master COP manifests using `cop:manifest_ref` or `about` relation links
5. **Temporal Precision**: Use RFC 3339 timestamps for all datetime fields
6. **Raster Data**: When using raster assets, combine with the [Raster Extension](https://github.com/stac-extensions/raster) for complete band and data type information
7. **Platform and Sensor**: Use `cop:platform` and `cop:sensor` to track data provenance, especially important for multi-source operational environments
8. **Software Tracking**: Include `cop:software_identifier` to maintain processing lineage and ensure reproducibility
9. **Cloud-Native Formats**: Prefer Cloud Optimized GeoTIFF (COG) over traditional GeoTIFF for raster data to enable efficient cloud-based access and streaming
10. **Analysis Ready Data**: Use ARD assets when satellite imagery has been preprocessed with atmospheric correction and geometric correction for immediate analysis
11. **NetCDF for Scientific Data**: Use NetCDF format for multidimensional data (time series, climate models, ocean data) with proper CF conventions metadata
12. **OGC API Adoption**: Prefer OGC API standards (Features, Tiles, Coverages, Processes) over traditional OGC Web Services for new implementations, providing RESTful, JSON-based interfaces
13. **Service Documentation**: For OGC API endpoints, include links to OpenAPI documentation (`service-desc` relation) and conformance declarations
14. **Format Profiles**: Specify format profiles in MIME types (e.g., `image/tiff; application=geotiff; profile=cloud-optimized`) to indicate optimization level
15. **Web Service Metadata**: When exporting web services (WMS, XYZ tiles), create JSON metadata assets with service parameters rather than attempting raster export
16. **BLAKE3 Integration**: For blockchain/IPFS workflows, use BLAKE3 hashing with multihash prefix (`1e20` for BLAKE3, `1220` for SHA256) in `cop:integrity_hash`

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md).

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Navigate to the root of this repository and run:

```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema:

```bash
npm test
```

If the tests reveal formatting problems with the examples, you can fix them with:

```bash
npm run format-examples
```

## License

This extension is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

