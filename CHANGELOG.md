# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- **JSON-LD Vocabulary** (`context.jsonld`):
  - Formal semantic mappings for all COP fields
  - Integration with OWS Context, DGGS Ontology, Schema.org, Dublin Core, W3C PROV, and GeoSPARQL
  - Enables linked data and RDF/OWL interoperability
  - Supports semantic web integration and knowledge graph construction
- Enhanced DGGS support based on share_common_operating_picture implementation:
  - `cop:dggs_zone_ids` - Array of DGGS zone identifiers for collections/items covering multiple zones
  - `cop:dggs_center_zone` - DGGS zone identifier for the center point
  - `cop:dggs_resolution` - DGGS resolution level (string or integer)
- New Collection example (`collection-dggs-zones.json`) demonstrating multi-zone DGGS coverage
- Semantic Vocabulary section in README with complete ontology mappings
- Best practices for BLAKE3 integration with blockchain/IPFS workflows
- Best practices for web service metadata export
- Documentation improvements for DGGS field usage patterns

### Changed

- Updated schema to accept both string and integer types for `cop:dggs_resolution`
- Enhanced DGGS documentation with usage guidelines for single vs. multiple zones
- Expanded `cop:dggs_crs` examples to include H3, S2, and ISEA3H systems
- Added JSON-LD Context link to README header

## [1.0.0] - 2025-11-25

### Added

- Initial release of STAC Common Operating Picture (COP) Extension
- Core COP fields for operational data exchange:
  - `cop:mission` - Mission/operation identifier
  - `cop:classification` - Security classification level
  - `cop:releasability` - Data releasability specification
  - `cop:dggs_zone_id` - DGGS zone identifier
  - `cop:dggs_crs` - DGGS Coordinate Reference System
  - `cop:asset_type` - Type of COP asset
  - `cop:integrity_hash` - Asset integrity verification
  - `cop:manifest_ref` - Reference to COP manifest
  - `cop:service_provider` - Service/data provider
  - `cop:volume_of_interest` - 3D volume definition
- JSON Schema for validation
- Complete documentation with use cases and best practices
- Example STAC Items (POI, web service)
- Example STAC Collection

### Changed

### Deprecated

### Removed

### Fixed

[Unreleased]: https://github.com/luciocola/cop/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/luciocola/cop/releases/tag/v1.0.0
