# OGC OWS Context Conceptual Model - Version 2.0

**OGC Document Number:** 12-080r3 (Draft)  
**Version:** 2.0  
**Publication Date:** 2025-12-17  
**Document Type:** OGC Implementation Standard  
**Editor:** Lucio Colaiacomo  
**Based on:** OGC 12-080r2 OWS Context Conceptual Model v1.0

---

## Abstract

This document describes the updated conceptual model for the OGC Web Services Context Document (OWS Context) standard, extended to support modern cloud-native data formats and OGC API specifications. The OWS Context enables the exchange of fully configured service sets and data resources between applications, supporting both traditional OGC Web Services (WMS, WFS, WCS, WMTS, WPS) and modern OGC APIs (Features, Tiles, Coverages, Processes, Records, Maps).

This version adds support for:
- **Cloud-native data formats**: Cloud Optimized GeoTIFF (COG), Analysis Ready Data (ARD), NetCDF, Zarr
- **OGC API standards**: RESTful, JSON-based alternatives to traditional OGC Web Services
- **Enhanced interoperability**: Between legacy and modern geospatial systems
- **Improved performance**: Optimized formats for cloud-based access and processing

## Keywords

OGC, Context, OWS Context, Common Operating Picture, COP, Web Services, OGC API, Cloud Optimized GeoTIFF, COG, Analysis Ready Data, ARD, NetCDF, Zarr, WMS, WFS, WCS, WMTS, WPS, CSW

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Scope](#2-scope)
3. [Conformance](#3-conformance)
4. [Normative References](#4-normative-references)
5. [Terms and Definitions](#5-terms-and-definitions)
6. [Conventions](#6-conventions)
7. [OWS Context Conceptual Model](#7-ows-context-conceptual-model)
8. [Data Formats](#8-data-formats)
9. [OGC API Integration](#9-ogc-api-integration)
10. [Cloud-Native Formats](#10-cloud-native-formats)
11. [Examples](#11-examples)
12. [Annex A: Abstract Test Suite](#annex-a-abstract-test-suite)
13. [Annex B: Revision History](#annex-b-revision-history)

---

## 1. Introduction

### 1.1 Background

The OGC Web Services Context Document (OWS Context) was created to enable the exchange of configured information resources (service sets) between applications, primarily as a collection of services. The original specification (12-080r2) focused on traditional OGC Web Services such as WMS, WFS, WCS, WMTS, and WPS.

Since the publication of version 1.0, the geospatial community has evolved significantly:

- **OGC APIs**: A new generation of standards based on OpenAPI, RESTful principles, and JSON
- **Cloud-native formats**: Optimized data formats designed for cloud storage and streaming access
- **Analysis Ready Data**: Standardized, preprocessed data ready for immediate analysis
- **Big Data processing**: Requirements for handling large-scale, multidimensional datasets

This revision extends the OWS Context conceptual model to support these modern capabilities while maintaining backward compatibility with existing implementations.

### 1.2 Objectives

The objectives of this updated specification are to:

1. Define how OWS Context documents reference OGC API endpoints
2. Specify support for cloud-native data formats (COG, NetCDF, Zarr)
3. Enable integration of Analysis Ready Data (ARD) resources
4. Maintain compatibility with existing OWS Context implementations
5. Provide clear migration paths from legacy to modern formats
6. Support hybrid environments mixing traditional and modern services

### 1.3 Relationship to Other Standards

This specification builds upon:

- **OGC 12-080r2**: OWS Context Conceptual Model v1.0
- **OGC 12-084r2**: OWS Context Atom Encoding
- **OGC 14-055r2**: OWS Context GeoJSON Encoding
- **OGC API - Features**: Part 1: Core (19-072)
- **OGC API - Tiles**: Part 1: Core (20-057)
- **OGC API - Coverages**: Part 1: Core (19-087)
- **OGC API - Processes**: Part 1: Core (18-062)
- **Cloud Optimized GeoTIFF**: Community standard
- **CEOS Analysis Ready Data**: CEOS-ARD specifications

---

## 2. Scope

This specification defines the conceptual model for OWS Context documents that can reference:

1. **Traditional OGC Web Services**: WMS, WFS, WCS, WMTS, WPS, CSW, WMTS
2. **OGC API services**: Features, Tiles, Coverages, Processes, Maps, Records
3. **Cloud-native data formats**: COG, NetCDF, Zarr, HDF5
4. **Analysis Ready Data**: Satellite imagery with standardized preprocessing
5. **Inline content**: GeoJSON, GML, KML embedded in context documents
6. **External resources**: Any URL-accessible geospatial resource

The scope includes:

- Conceptual model (UML) for all resource types
- Requirements for encoding specifications
- Abstract test suite for conformance testing
- Examples demonstrating integration patterns

---

## 3. Conformance

This specification defines the following conformance classes:

### 3.1 Core Conformance Class

**Requirements Class:** http://www.opengis.net/spec/owc/2.0/req/core

All OWS Context implementations SHALL conform to this class.

**Requirements:**
- Support for Context and Resource classes
- Basic metadata (title, abstract, update date)
- Geographic extent definition
- Author and contributor information

### 3.2 Traditional Services Conformance Class

**Requirements Class:** http://www.opengis.net/spec/owc/2.0/req/traditional-services

Implementations supporting legacy OGC Web Services SHALL conform to this class.

**Requirements:**
- WMS, WFS, WCS, WMTS, WPS service descriptions
- GetCapabilities and operation endpoint references
- Service-specific parameters (layers, styles, formats)

### 3.3 OGC API Conformance Class

**Requirements Class:** http://www.opengis.net/spec/owc/2.0/req/ogc-api

Implementations supporting OGC API standards SHALL conform to this class.

**Requirements:**
- API endpoint URIs following OGC API patterns
- OpenAPI specification references
- Conformance declaration links
- Collection and item references

### 3.4 Cloud-Native Formats Conformance Class

**Requirements Class:** http://www.opengis.net/spec/owc/2.0/req/cloud-native

Implementations supporting cloud-optimized formats SHALL conform to this class.

**Requirements:**
- Cloud Optimized GeoTIFF references
- NetCDF and Zarr dataset descriptions
- Range subsetting parameters
- Streaming access metadata

### 3.5 Analysis Ready Data Conformance Class

**Requirements Class:** http://www.opengis.net/spec/owc/2.0/req/ard

Implementations supporting ARD SHALL conform to this class.

**Requirements:**
- CEOS-ARD specification references
- Processing level indicators
- Atmospheric and geometric correction metadata
- Sensor and platform information

---

## 4. Normative References

The following documents are referred to in this document in such a way that some or all of their content constitutes requirements of this document.

- **OGC 12-080r2**: OGC OWS Context Conceptual Model
- **OGC 19-072**: OGC API - Features - Part 1: Core
- **OGC 20-057**: OGC API - Tiles - Part 1: Core
- **OGC 19-087**: OGC API - Coverages - Part 1: Core
- **OGC 18-062r2**: OGC API - Processes - Part 1: Core
- **RFC 2616**: Hypertext Transfer Protocol -- HTTP/1.1
- **RFC 3986**: Uniform Resource Identifier (URI): Generic Syntax
- **RFC 7946**: The GeoJSON Format
- **RFC 3339**: Date and Time on the Internet: Timestamps
- **ISO 19115**: Geographic information - Metadata
- **CEOS-ARD**: Committee on Earth Observation Satellites Analysis Ready Data Specifications

---

## 5. Terms and Definitions

### 5.1 Core Terms

**Analysis Ready Data (ARD)**  
Satellite data that have been processed to a minimum set of requirements and organized into a form that allows immediate analysis with minimum additional user effort

**Cloud Optimized GeoTIFF (COG)**  
A regular GeoTIFF file aimed at being hosted on a HTTP file server with internal organization that enables efficient workflows on the cloud

**Context Document**  
A document encoding a configured set of geospatial resources that can be exchanged between applications

**DGGS**  
Discrete Global Grid System - a spatial reference system using a hierarchical tessellation of cells

**OGC API**  
A family of standards that specify RESTful APIs for accessing geospatial data and services

**Resource**  
Any geospatial data, service, or information that can be referenced in a context document

**Service Offering**  
Description of how to access and use a particular geospatial service or dataset

### 5.2 Data Format Terms

**NetCDF**  
Network Common Data Form - a set of software libraries and machine-independent data formats for array-oriented scientific data

**Zarr**  
A format for storage of chunked, compressed, N-dimensional arrays optimized for cloud environments

**COG Profile**  
Specific organization of a GeoTIFF file with internal tiling and overviews for efficient HTTP range request access

---

## 6. Conventions

### 6.1 Symbols and Abbreviated Terms

| Term | Definition |
|------|------------|
| API | Application Programming Interface |
| ARD | Analysis Ready Data |
| CEOS | Committee on Earth Observation Satellites |
| COG | Cloud Optimized GeoTIFF |
| COP | Common Operating Picture |
| CRS | Coordinate Reference System |
| CSW | Catalogue Service for the Web |
| DGGS | Discrete Global Grid System |
| HTTP | Hypertext Transfer Protocol |
| JSON | JavaScript Object Notation |
| MIME | Multipurpose Internet Mail Extensions |
| NetCDF | Network Common Data Form |
| OGC | Open Geospatial Consortium |
| OWS | OGC Web Services |
| REST | Representational State Transfer |
| URI | Uniform Resource Identifier |
| URL | Uniform Resource Locator |
| WCS | Web Coverage Service |
| WFS | Web Feature Service |
| WMS | Web Map Service |
| WMTS | Web Map Tile Service |
| WPS | Web Processing Service |
| XML | Extensible Markup Language |

### 6.2 UML Notation

This document uses UML (Unified Modeling Language) class diagrams to describe the conceptual model. The following conventions apply:

- **Class**: Rectangle with class name
- **Attribute**: Name and type within class box
- **Association**: Line connecting classes
- **Multiplicity**: Numbers indicating relationship cardinality
- **Inheritance**: Arrow with hollow head pointing to parent class

---

## 7. OWS Context Conceptual Model

### 7.1 Overview

The OWS Context conceptual model defines a structure for organizing geospatial resources in a way that preserves their configuration and relationships. The model consists of:

1. **Context**: Top-level container with metadata about the resource collection
2. **Resource**: Individual geospatial dataset, service, or content
3. **Offering**: Description of how to access and use a resource
4. **Operation**: Specific service operation with parameters
5. **Content**: Inline or referenced data content

### 7.2 Core Classes

#### 7.2.1 Context Class

The Context class represents the top-level container for a collection of geospatial resources.

**Attributes:**

| Attribute | Type | Multiplicity | Description |
|-----------|------|--------------|-------------|
| id | URI | 1 | Unique identifier for the context |
| title | String | 1 | Human-readable title |
| abstract | String | 0..1 | Description of the context |
| updateDate | DateTime | 1 | Last update timestamp |
| author | Author | 0..* | Context creators |
| publisher | String | 0..1 | Publishing entity |
| creator | Creator | 0..1 | Creating application |
| rights | String | 0..1 | Usage rights |
| areaOfInterest | Envelope | 0..1 | Geographic extent |
| timeIntervalOfInterest | TimeInterval | 0..1 | Temporal extent |
| keyword | String | 0..* | Descriptive keywords |
| resource | Resource | 0..* | Contained resources |

#### 7.2.2 Resource Class

The Resource class represents an individual geospatial dataset, service, or content item.

**Attributes:**

| Attribute | Type | Multiplicity | Description |
|-----------|------|--------------|-------------|
| id | URI | 1 | Unique resource identifier |
| title | String | 1 | Resource title |
| abstract | String | 0..1 | Resource description |
| updateDate | DateTime | 1 | Last update timestamp |
| author | Author | 0..* | Resource creators |
| publisher | String | 0..1 | Publishing entity |
| rights | String | 0..1 | Usage rights |
| geospatialExtent | Envelope | 0..1 | Geographic extent |
| temporalExtent | TimeInterval | 0..1 | Temporal extent |
| contentDescription | String | 0..1 | Content description |
| preview | URL | 0..* | Preview images |
| contentByRef | URL | 0..* | External content references |
| offering | Offering | 1..* | Service offerings |
| active | Boolean | 0..1 | Resource activation state |
| resourceMetadata | Metadata | 0..* | Additional metadata |
| keyword | String | 0..* | Descriptive keywords |
| minScaleDenominator | Double | 0..1 | Minimum scale |
| maxScaleDenominator | Double | 0..1 | Maximum scale |
| folder | String | 0..1 | Logical grouping folder |

#### 7.2.3 Offering Class

The Offering class describes how to access and use a resource.

**Attributes:**

| Attribute | Type | Multiplicity | Description |
|-----------|------|--------------|-------------|
| code | URI | 1 | Offering type identifier |
| operation | Operation | 0..* | Available operations |
| content | Content | 0..* | Inline or referenced content |
| styleSet | StyleSet | 0..* | Rendering styles |

#### 7.2.4 Operation Class

The Operation class represents a specific service operation.

**Attributes:**

| Attribute | Type | Multiplicity | Description |
|-----------|------|--------------|-------------|
| code | String | 1 | Operation name |
| method | String | 1 | HTTP method (GET, POST, etc.) |
| requestURL | URL | 1 | Operation endpoint |
| request | Content | 0..1 | Request message template |
| result | Content | 0..1 | Expected response format |

### 7.3 Extended Model for Modern Formats

This version extends the core model to support modern geospatial formats and services.

#### 7.3.1 Resource Type Extension

The Resource class is extended with a **resourceType** attribute:

| Value | Description |
|-------|-------------|
| traditional-service | WMS, WFS, WCS, WMTS, WPS, CSW |
| ogc-api-service | OGC API endpoints |
| cloud-native-data | COG, NetCDF, Zarr |
| ard-data | Analysis Ready Data |
| inline-data | GeoJSON, GML, KML |
| external-resource | Generic URL reference |

#### 7.3.2 Offering Code Extension

New offering codes for modern services and formats:

| Code | Description |
|------|-------------|
| http://www.opengis.net/spec/owc/2.0/req/ogc-api/features | OGC API - Features |
| http://www.opengis.net/spec/owc/2.0/req/ogc-api/tiles | OGC API - Tiles |
| http://www.opengis.net/spec/owc/2.0/req/ogc-api/coverages | OGC API - Coverages |
| http://www.opengis.net/spec/owc/2.0/req/ogc-api/processes | OGC API - Processes |
| http://www.opengis.net/spec/owc/2.0/req/ogc-api/maps | OGC API - Maps |
| http://www.opengis.net/spec/owc/2.0/req/ogc-api/records | OGC API - Records |
| http://www.opengis.net/spec/owc/2.0/req/cloud-native/cog | Cloud Optimized GeoTIFF |
| http://www.opengis.net/spec/owc/2.0/req/cloud-native/netcdf | NetCDF dataset |
| http://www.opengis.net/spec/owc/2.0/req/cloud-native/zarr | Zarr array |
| http://www.opengis.net/spec/owc/2.0/req/ard/ceos | CEOS Analysis Ready Data |

---

## 8. Data Formats

### 8.1 Traditional Formats

OWS Context continues to support all formats from version 1.0:

#### 8.1.1 Vector Formats
- **GeoJSON**: RFC 7946 compliant JSON encoding
- **GML**: OGC Geography Markup Language
- **KML**: OGC Keyhole Markup Language
- **Shapefile**: ESRI Shapefile format (by reference)

#### 8.1.2 Raster Formats
- **GeoTIFF**: Tagged Image File Format for geospatial data
- **PNG**: Portable Network Graphics
- **JPEG**: Joint Photographic Experts Group format
- **JPEG 2000**: ISO/IEC 15444 standard

### 8.2 Cloud-Native Formats

#### 8.2.1 Cloud Optimized GeoTIFF (COG)

**Format Specification:**
- Standard GeoTIFF with specific internal organization
- Tiled structure (typically 512x512 or 256x256 pixels)
- Internal overviews for multiple resolution levels
- Optimized for HTTP range requests

**MIME Type:** `image/tiff; application=geotiff; profile=cloud-optimized`

**Requirements:**
- SHALL use tiled layout
- SHALL include overview images
- SHOULD use compression (LZW, DEFLATE, or JPEG)
- SHOULD be organized for efficient streaming

**Context Integration:**
```json
{
  "offering": {
    "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/cog",
    "content": {
      "type": "image/tiff; application=geotiff; profile=cloud-optimized",
      "href": "https://storage.example.com/data/elevation.tif"
    }
  }
}
```

#### 8.2.2 NetCDF (Network Common Data Form)

**Format Specification:**
- NetCDF-4 (HDF5 backend) or NetCDF Classic
- CF Conventions compliance for climate/forecast data
- Multidimensional array storage
- Self-describing with embedded metadata

**MIME Type:** `application/netcdf` or `application/x-netcdf`

**Requirements:**
- SHOULD follow CF Conventions for coordinate systems
- SHALL include dimension information
- SHOULD provide variable metadata
- MAY include data access protocols (OPeNDAP, THREDDS)

**Context Integration:**
```json
{
  "offering": {
    "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/netcdf",
    "content": {
      "type": "application/netcdf",
      "href": "https://data.example.org/climate/temperature.nc"
    }
  }
}
```

#### 8.2.3 Zarr

**Format Specification:**
- Chunked, compressed N-dimensional arrays
- Cloud-optimized with object storage support
- JSON-based metadata
- Multiple storage backends (filesystem, S3, GCS)

**MIME Type:** `application/zarr` or `application/vnd.zarr+json`

**Requirements:**
- SHALL define chunk structure
- SHALL specify compression codec
- SHOULD provide dimension and coordinate information
- MAY include Xarray-compatible metadata

**Context Integration:**
```json
{
  "offering": {
    "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/zarr",
    "content": {
      "type": "application/zarr",
      "href": "s3://bucket/data/array.zarr/"
    }
  }
}
```

### 8.3 Analysis Ready Data (ARD)

#### 8.3.1 CEOS-ARD Framework

**Overview:**
Analysis Ready Data is defined by the Committee on Earth Observation Satellites (CEOS) as satellite data that have been processed to a minimum set of requirements and organized for immediate analysis.

**Product Levels:**

| Level | Description | Requirements |
|-------|-------------|--------------|
| Surface Reflectance | Atmospherically corrected, orthorectified | Geometric accuracy < 25m (Landsat/Sentinel-2 scale) |
| Surface Temperature | TOA brightness temperature converted to surface temperature | Includes emissivity corrections |
| Radar Backscatter | Normalized radar backscatter | Radiometric terrain correction applied |

**CEOS-ARD Specifications:**
- CEOS-ARD for Land Surface Reflectance (LSR)
- CEOS-ARD for Land Surface Temperature (LST)
- CEOS-ARD for Synthetic Aperture Radar (SAR)
- CEOS-ARD for Aquatic Reflectance

**Requirements:**
- SHALL conform to relevant CEOS-ARD Product Family Specification
- SHALL provide metadata documenting:
  - Processing level
  - Geometric correction method
  - Atmospheric correction algorithm
  - Sensor calibration information
  - Data quality indicators
- SHOULD be provided in COG format
- SHOULD include per-pixel quality flags

**Context Integration:**
```json
{
  "offering": {
    "code": "http://www.opengis.net/spec/owc/2.0/req/ard/ceos",
    "content": {
      "type": "image/tiff; application=geotiff; profile=cloud-optimized",
      "href": "https://ard.example.org/sentinel2/L2A/tile.tif"
    },
    "metadata": {
      "ard:specification": "CEOS-ARD LSR v5.0",
      "ard:processing_level": "Surface Reflectance",
      "ard:atmospheric_correction": "Sen2Cor v2.10",
      "ard:geometric_correction": "Sentinel-2 Global Reference Image"
    }
  }
}
```

---

## 9. OGC API Integration

### 9.1 Overview

OGC APIs represent a modernization of OGC Web Services, providing:
- RESTful architecture
- JSON encoding (in addition to other formats)
- OpenAPI specification for service description
- Conformance classes for feature discovery
- Simplified access patterns

### 9.2 OGC API - Features

**Standard:** OGC 19-072 (formerly WFS 3.0)

**Core Endpoints:**

| Endpoint | Purpose |
|----------|---------|
| `/` | Landing page |
| `/conformance` | Conformance declaration |
| `/collections` | List of feature collections |
| `/collections/{collectionId}` | Collection metadata |
| `/collections/{collectionId}/items` | Feature query |
| `/collections/{collectionId}/items/{featureId}` | Single feature |

**Context Integration:**
```json
{
  "resource": {
    "id": "buildings-api",
    "title": "Building Footprints",
    "offering": {
      "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/features",
      "operation": [
        {
          "code": "landing-page",
          "method": "GET",
          "requestURL": "https://api.example.org/features/"
        },
        {
          "code": "items",
          "method": "GET",
          "requestURL": "https://api.example.org/features/collections/buildings/items"
        }
      ]
    },
    "link": [
      {
        "rel": "service-desc",
        "type": "application/vnd.oai.openapi+json;version=3.0",
        "href": "https://api.example.org/features/openapi"
      }
    ]
  }
}
```

### 9.3 OGC API - Tiles

**Standard:** OGC 20-057

**Core Endpoints:**

| Endpoint | Purpose |
|----------|---------|
| `/collections/{collectionId}/tiles` | Tilesets for collection |
| `/collections/{collectionId}/tiles/{tileMatrixSetId}` | Tileset metadata |
| `/collections/{collectionId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}` | Individual tile |

**Context Integration:**
```json
{
  "resource": {
    "id": "satellite-tiles",
    "title": "Satellite Imagery Tiles",
    "offering": {
      "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/tiles",
      "operation": [
        {
          "code": "tile",
          "method": "GET",
          "requestURL": "https://api.example.org/tiles/collections/imagery/tiles/WebMercatorQuad/{z}/{y}/{x}"
        }
      ]
    }
  }
}
```

### 9.4 OGC API - Coverages

**Standard:** OGC 19-087

**Core Endpoints:**

| Endpoint | Purpose |
|----------|---------|
| `/collections/{collectionId}/coverage` | Coverage metadata |
| `/collections/{collectionId}/coverage/rangetype` | Range type description |
| `/collections/{collectionId}/coverage/domainset` | Domain set description |

**Context Integration:**
```json
{
  "resource": {
    "id": "elevation-coverage",
    "title": "Digital Elevation Model",
    "offering": {
      "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/coverages",
      "operation": [
        {
          "code": "coverage",
          "method": "GET",
          "requestURL": "https://api.example.org/coverages/collections/dem/coverage"
        }
      ]
    }
  }
}
```

### 9.5 OGC API - Processes

**Standard:** OGC 18-062r2 (formerly WPS 2.0)

**Core Endpoints:**

| Endpoint | Purpose |
|----------|---------|
| `/processes` | List of processes |
| `/processes/{processId}` | Process description |
| `/processes/{processId}/execution` | Execute process |
| `/jobs/{jobId}` | Job status |
| `/jobs/{jobId}/results` | Job results |

**Context Integration:**
```json
{
  "resource": {
    "id": "buffer-process",
    "title": "Buffer Analysis Process",
    "offering": {
      "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/processes",
      "operation": [
        {
          "code": "execute",
          "method": "POST",
          "requestURL": "https://api.example.org/processes/buffer/execution"
        }
      ]
    }
  }
}
```

### 9.6 API-Specific Metadata

When referencing OGC API services, the following metadata SHOULD be provided:

**Required:**
- Landing page URL
- Collection identifier (if applicable)
- API version information

**Recommended:**
- OpenAPI specification link (`service-desc` relation)
- Conformance declaration link
- Available output formats
- Query parameters and filters
- Authentication requirements

---

## 10. Cloud-Native Formats

### 10.1 Cloud Optimization Principles

Cloud-native geospatial formats share common principles:

1. **Chunked Organization**: Data divided into smaller pieces for parallel access
2. **HTTP Range Request Support**: Partial file reading without downloading entire dataset
3. **Internal Metadata**: Self-describing format with embedded information
4. **Compression**: Efficient storage and transmission
5. **Multiple Resolutions**: Overview images or zoom levels for scale-appropriate access

### 10.2 Cloud Optimized GeoTIFF (COG) Implementation

#### 10.2.1 Technical Requirements

**Structure:**
- Tiled layout (not stripped)
- Tile size: 512×512 or 256×256 pixels (recommended)
- Internal overviews for each power-of-2 reduction
- Overview resampling: average, nearest, bilinear, or cubic

**Organization:**
```
[IFD Header]
  → [Tile Index]
  → [Overview IFD] (level 1)
    → [Tile Index]
    → [Overview IFD] (level 2)
      → [Tile Index]
      → ...
[Tile Data Level 0]
[Tile Data Level 1]
[Tile Data Level 2]
...
```

**Validation:**
Tools like `rio cogeo validate` can verify COG compliance.

#### 10.2.2 COG Creation

**Using GDAL:**
```bash
gdal_translate input.tif output.tif \
  -co TILED=YES \
  -co COPY_SRC_OVERVIEWS=YES \
  -co COMPRESS=DEFLATE \
  -co BLOCKXSIZE=512 \
  -co BLOCKYSIZE=512
```

**Using Rio-cogeo:**
```bash
rio cogeo create input.tif output.tif \
  --overview-level 5 \
  --overview-resampling bilinear
```

#### 10.2.3 COG Access Patterns

**Partial Reading:**
```python
import rasterio
from rasterio.windows import Window

with rasterio.open('https://example.com/data.tif') as src:
    # Read only a subset
    window = Window(0, 0, 512, 512)
    data = src.read(1, window=window)
```

**Multi-resolution Access:**
```python
# Read from overview level
with rasterio.open('https://example.com/data.tif') as src:
    overview_data = src.read(1, out_shape=(256, 256))
```

### 10.3 NetCDF Implementation

#### 10.3.1 CF Conventions

NetCDF files SHOULD follow CF (Climate and Forecast) Conventions:

**Coordinate Variables:**
```
dimensions:
    time = UNLIMITED ;
    lat = 180 ;
    lon = 360 ;
variables:
    double time(time) ;
        time:units = "days since 1900-01-01" ;
        time:calendar = "gregorian" ;
    double lat(lat) ;
        lat:units = "degrees_north" ;
        lat:standard_name = "latitude" ;
    double lon(lon) ;
        lon:units = "degrees_east" ;
        lon:standard_name = "longitude" ;
    float temperature(time, lat, lon) ;
        temperature:units = "K" ;
        temperature:standard_name = "air_temperature" ;
```

#### 10.3.2 NetCDF-4 Features

**Chunking:**
```python
import netCDF4

ds = netCDF4.Dataset('output.nc', 'w', format='NETCDF4')
# Define dimensions
time_dim = ds.createDimension('time', None)
lat_dim = ds.createDimension('lat', 180)
lon_dim = ds.createDimension('lon', 360)

# Create variable with chunking
temp_var = ds.createVariable('temperature', 'f4', 
                             ('time', 'lat', 'lon'),
                             chunksizes=(1, 90, 180),
                             compression='zlib',
                             complevel=4)
```

**Compression:**
- Deflate (zlib) compression levels 1-9
- Shuffling filter for improved compression
- Scale/offset for lossy compression

#### 10.3.3 OPeNDAP Integration

NetCDF files can be served via OPeNDAP protocol:

**Context Reference:**
```json
{
  "offering": {
    "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/netcdf",
    "operation": [
      {
        "code": "opendap",
        "method": "GET",
        "requestURL": "https://thredds.example.org/dodsC/data/model.nc"
      },
      {
        "code": "direct-access",
        "method": "GET",
        "requestURL": "https://data.example.org/files/model.nc"
      }
    ]
  }
}
```

### 10.4 Zarr Implementation

#### 10.4.1 Zarr Structure

**Directory Organization:**
```
data.zarr/
├── .zarray          # Array metadata
├── .zattrs          # User attributes
├── .zgroup          # Group metadata
├── 0.0              # Chunk files
├── 0.1
├── 1.0
└── 1.1
```

**Metadata (.zarray):**
```json
{
  "chunks": [1000, 1000],
  "compressor": {
    "id": "blosc",
    "cname": "lz4",
    "clevel": 5,
    "shuffle": 1
  },
  "dtype": "<f4",
  "fill_value": "NaN",
  "filters": null,
  "order": "C",
  "shape": [10000, 10000],
  "zarr_format": 2
}
```

#### 10.4.2 Cloud Storage

**S3 Backend:**
```python
import zarr
import s3fs

# S3 filesystem
s3 = s3fs.S3FileSystem()

# Open Zarr array from S3
store = s3fs.S3Map('s3://bucket/data.zarr', s3=s3)
z = zarr.open(store, mode='r')
```

**Context Reference:**
```json
{
  "offering": {
    "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/zarr",
    "content": {
      "type": "application/zarr",
      "href": "s3://bucket/data.zarr/"
    },
    "metadata": {
      "zarr:chunks": [1000, 1000],
      "zarr:compressor": "blosc/lz4",
      "zarr:shape": [10000, 10000]
    }
  }
}
```

### 10.5 Format Selection Guidelines

| Use Case | Recommended Format | Rationale |
|----------|-------------------|-----------|
| Single-band imagery | COG | Efficient HTTP range requests |
| Multi-band satellite | COG or NetCDF | COG for RGB/NIR, NetCDF for many bands |
| Time series | NetCDF or Zarr | Native multidimensional support |
| Large datasets (>1TB) | Zarr | Better chunking, cloud optimization |
| Climate/ocean models | NetCDF | CF conventions, community standard |
| Real-time streaming | COG | Fast partial access |
| Machine learning | Zarr | Optimized for array operations |

---

## 11. Examples

### 11.1 Mixed Environment Context

A context document combining traditional services, OGC APIs, and cloud-native formats:

```json
{
  "type": "FeatureCollection",
  "id": "urn:uuid:mixed-environment-context",
  "properties": {
    "title": "Disaster Response Context - Mixed Services",
    "updated": "2025-12-17T10:00:00Z",
    "author": "Emergency Operations Center",
    "generator": {
      "title": "OWS Context v2.0",
      "uri": "http://www.opengis.net/spec/owc/2.0"
    },
    "categories": [
      {"term": "Emergency Response"},
      {"term": "Wildfire"}
    ]
  },
  "bbox": [-122.5, 37.5, -121.5, 38.5],
  "features": [
    {
      "type": "Feature",
      "id": "basemap-imagery",
      "properties": {
        "title": "Satellite Base Imagery",
        "updated": "2025-12-15T00:00:00Z",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/1.0/req/atom/wms",
          "operations": [{
            "code": "GetMap",
            "method": "GET",
            "href": "https://services.example.org/wms?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&LAYERS=satellite&STYLES=&CRS=EPSG:3857&BBOX={bbox}&WIDTH={width}&HEIGHT={height}&FORMAT=image/png"
          }]
        }]
      }
    },
    {
      "type": "Feature",
      "id": "fire-perimeters",
      "properties": {
        "title": "Active Fire Perimeters (OGC API)",
        "updated": "2025-12-17T09:30:00Z",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/features",
          "operations": [{
            "code": "items",
            "method": "GET",
            "href": "https://api.emergency.gov/features/collections/fire-perimeters/items"
          }]
        }]
      },
      "links": [{
        "rel": "service-desc",
        "type": "application/vnd.oai.openapi+json;version=3.0",
        "href": "https://api.emergency.gov/features/openapi"
      }]
    },
    {
      "type": "Feature",
      "id": "elevation-model",
      "properties": {
        "title": "High-Resolution Elevation (COG)",
        "updated": "2025-12-01T00:00:00Z",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/cog",
          "contents": [{
            "type": "image/tiff; application=geotiff; profile=cloud-optimized",
            "href": "https://storage.example.com/elevation/area-123.tif"
          }]
        }]
      }
    },
    {
      "type": "Feature",
      "id": "ard-imagery",
      "properties": {
        "title": "Pre-fire Analysis Ready Data",
        "updated": "2025-11-20T00:00:00Z",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/ard/ceos",
          "contents": [{
            "type": "image/tiff; application=geotiff; profile=cloud-optimized",
            "href": "https://ard.example.org/sentinel2/2025-11-20/tile.tif"
          }],
          "metadata": {
            "ard:specification": "CEOS-ARD LSR v5.0",
            "ard:processing_level": "Surface Reflectance",
            "platform": "Sentinel-2B",
            "sensor": "MSI"
          }
        }]
      }
    },
    {
      "type": "Feature",
      "id": "weather-forecast",
      "properties": {
        "title": "Weather Forecast Model (NetCDF)",
        "updated": "2025-12-17T06:00:00Z",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/netcdf",
          "operations": [{
            "code": "opendap",
            "method": "GET",
            "href": "https://thredds.weather.gov/dodsC/gfs/20251217/gfs_0.25deg_06z.nc"
          }],
          "contents": [{
            "type": "application/netcdf",
            "href": "https://data.weather.gov/gfs/20251217/gfs_0.25deg_06z.nc"
          }]
        }]
      }
    }
  ]
}
```

### 11.2 Pure OGC API Context

A modern context using only OGC API services:

```json
{
  "type": "FeatureCollection",
  "id": "urn:uuid:ogc-api-context",
  "properties": {
    "title": "Urban Planning - OGC API Services",
    "updated": "2025-12-17T14:30:00Z"
  },
  "features": [
    {
      "type": "Feature",
      "id": "buildings",
      "properties": {
        "title": "Building Footprints",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/features",
          "operations": [{
            "code": "items",
            "method": "GET",
            "href": "https://api.city.gov/features/v1/collections/buildings/items"
          }]
        }]
      },
      "links": [{
        "rel": "service-desc",
        "href": "https://api.city.gov/features/v1/openapi",
        "type": "application/vnd.oai.openapi+json;version=3.0"
      }]
    },
    {
      "type": "Feature",
      "id": "basemap-tiles",
      "properties": {
        "title": "City Basemap Tiles",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/tiles",
          "operations": [{
            "code": "tile",
            "method": "GET",
            "href": "https://api.city.gov/tiles/v1/collections/basemap/tiles/WebMercatorQuad/{z}/{y}/{x}"
          }]
        }]
      }
    },
    {
      "type": "Feature",
      "id": "elevation-coverage",
      "properties": {
        "title": "Digital Elevation Model",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/ogc-api/coverages",
          "operations": [{
            "code": "coverage",
            "method": "GET",
            "href": "https://api.city.gov/coverages/v1/collections/elevation/coverage"
          }]
        }]
      }
    }
  ]
}
```

### 11.3 Cloud-Native Data Context

A context focused on cloud-optimized formats:

```json
{
  "type": "FeatureCollection",
  "id": "urn:uuid:cloud-native-context",
  "properties": {
    "title": "Satellite Data Archive - Cloud-Native",
    "updated": "2025-12-17T16:00:00Z"
  },
  "features": [
    {
      "type": "Feature",
      "id": "landsat-cog",
      "properties": {
        "title": "Landsat 8 Scene (COG)",
        "datetime": "2025-08-15T10:30:00Z",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/cog",
          "contents": [{
            "type": "image/tiff; application=geotiff; profile=cloud-optimized",
            "href": "s3://landsat-pds/c2/l2/2025/123/045/LC08_L2SP_123045_20250815_20250820_02_T1/LC08_L2SP_123045_20250815_20250820_02_T1_SR_B4.TIF",
            "title": "Red Band"
          }]
        }]
      }
    },
    {
      "type": "Feature",
      "id": "climate-zarr",
      "properties": {
        "title": "Climate Model Output (Zarr)",
        "offerings": [{
          "code": "http://www.opengis.net/spec/owc/2.0/req/cloud-native/zarr",
          "contents": [{
            "type": "application/zarr",
            "href": "s3://climate-data/models/cmip6/temperature.zarr/"
          }],
          "metadata": {
            "zarr:chunks": [1, 180, 360],
            "zarr:dimensions": ["time", "lat", "lon"]
          }
        }]
      }
    }
  ]
}
```

---

## 12. Annex A: Abstract Test Suite

### A.1 Core Conformance Tests

#### Test A.1.1: Context Structure
**Purpose:** Verify basic context document structure  
**Method:** Parse context document and validate required elements  
**Pass Criteria:** Document contains id, title, updateDate, and resources array

#### Test A.1.2: Resource References
**Purpose:** Verify resources can be accessed  
**Method:** Attempt to access each resource href  
**Pass Criteria:** HTTP 200 response or valid alternative status

### A.2 OGC API Conformance Tests

#### Test A.2.1: Landing Page Access
**Purpose:** Verify OGC API landing page is accessible  
**Method:** GET request to root endpoint  
**Pass Criteria:** Returns JSON with conformance and collections links

#### Test A.2.2: Conformance Declaration
**Purpose:** Verify API conformance classes  
**Method:** GET request to /conformance endpoint  
**Pass Criteria:** Returns conformsTo array with valid URIs

#### Test A.2.3: Collection Access
**Purpose:** Verify collection can be queried  
**Method:** GET request to collection items endpoint  
**Pass Criteria:** Returns GeoJSON FeatureCollection

### A.3 Cloud-Native Format Tests

#### Test A.3.1: COG Validation
**Purpose:** Verify GeoTIFF is cloud-optimized  
**Method:** Check internal structure for tiling and overviews  
**Pass Criteria:** File has tiled layout and internal overviews

#### Test A.3.2: HTTP Range Request
**Purpose:** Verify partial file access  
**Method:** HTTP GET with Range header  
**Pass Criteria:** Server returns 206 Partial Content

#### Test A.3.3: NetCDF Structure
**Purpose:** Verify NetCDF format compliance  
**Method:** Open with NetCDF library and check dimensions  
**Pass Criteria:** File opens and contains expected dimensions

### A.4 ARD Conformance Tests

#### Test A.4.1: CEOS-ARD Metadata
**Purpose:** Verify ARD metadata presence  
**Method:** Check for required ARD metadata fields  
**Pass Criteria:** Contains specification version, processing level, corrections applied

#### Test A.4.2: Quality Flags
**Purpose:** Verify per-pixel quality information  
**Method:** Check for quality band or separate QA file  
**Pass Criteria:** Quality information is present and documented

---

## 13. Annex B: Revision History

| Version | Date | Editor | Description |
|---------|------|--------|-------------|
| 1.0 | 2014-01-22 | Roger Brackin, Pedro Gonçalves | Initial release (12-080r2) |
| 2.0 | 2025-12-17 | Lucio Colaiacomo | Added OGC APIs, cloud-native formats, ARD support |

### Changes in Version 2.0

**Major Additions:**
- OGC API integration (Features, Tiles, Coverages, Processes)
- Cloud Optimized GeoTIFF (COG) support
- NetCDF and Zarr format specifications
- CEOS Analysis Ready Data (ARD) framework
- New conformance classes for modern formats
- Extended offering codes for new resource types

**Backward Compatibility:**
- All version 1.0 features remain supported
- Existing OWS Context documents remain valid
- New fields are optional extensions

**Deprecations:**
- None - traditional OGC Web Services remain fully supported

---

## Bibliography

- **OGC 12-080r2** (2014): OGC OWS Context Conceptual Model
- **OGC 19-072** (2022): OGC API - Features - Part 1: Core
- **OGC 20-057** (2022): OGC API - Tiles - Part 1: Core  
- **OGC 19-087** (2021): OGC API - Coverages - Part 1: Core
- **OGC 18-062r2** (2021): OGC API - Processes - Part 1: Core
- **CEOS-ARD** (2021): CEOS Analysis Ready Data Product Family Specifications
- **Cloud Optimized GeoTIFF** (2019): COG Specification v1.0
- **NetCDF Users Guide** (2023): Unidata NetCDF Documentation
- **Zarr Specification** (2023): Zarr Format Specification v2
- **RFC 7946** (2016): The GeoJSON Format
- **RFC 3339** (2002): Date and Time on the Internet: Timestamps
- **ISO 19115-1** (2014): Geographic information - Metadata - Part 1: Fundamentals
- **CF Conventions** (2023): Climate and Forecast Metadata Conventions v1.10

---

**Document End**
