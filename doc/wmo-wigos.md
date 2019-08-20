# WMO WIGOS Metadata Standard Reference

This documentation focuses on the [WMO WIGOS Metadata Standard](https://library.wmo.int/opac/doc_num.php?explnum_id=3653) based schema
enhancements in pygeometa.

pygeometa's MCF model for WIGOS Metadata inherits as well as extends the core
MCF constructs.

## Reference:
WIGOS Metadata Representation - Specification of data model and xml schema 1.0RC9 [WIGOS Metadata Representation](http://www.wmo.int/schemas/wmdr/1.0RC9/documentation/WMDR_ModelAndSchemaSpecification.pdf)

## Codes

Codes for WMO WIGOS are available at https://github.com/wmo-im/wmds/tree/master/tables_en

## Sections

### `metadata`

See MCF reference

### `contact`

See MCF reference.  WMO WIGOS MCF add the contact type `facility` to
attach contact information to a facility.  The main MCF contact is attached
to the `wmdr:Header` element.

### `identification`

See MCF reference

### `facility`

The `facility` object consists of 1..n keys.  Key names are up to the user
with key objects having the model below.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
identifier|Mandatory|WMO WIGOS identifier|0-20008-0-JFJ|WIGOS Metadata Representation, Section 8.6.4
name|Mandatory|||WIGOS Metadata Representation, Section 4.3
type|Mandatory|The type of the observing facility from the Station/platform type codelist (http://test.wmocodes.info/wmdr/_FacilityType)|landFixed|WIGOS Metadata Representation, Section 4.3.2
geopositioning_method|Optional|Element describes the geospatial refer ence system used for the specified geolocation (codelist http://test.wmocodes.info/wmdr/_GeopositioningMethod)|gps|WIGOS Metadata Representation, Section 4.2.2
url|Optional|An online resource containing additional information about the facility or equipment|https://example.org/station/123|WIGOS Metadata Representation, Section 4.2.2
date_established|Mandatory|Date at which the observingFacility was established. Normally considered to be the date the first observations were made|2011-11-11T11:11:11Z|WIGOS Metadata Representation, Section 4.3.2
wmo_region|Conditional|Mandatory for fixed land-based stations; The WMO region the observing facility is located in, from the WMORegionType codelist (http://test.wmocodes.info/wmdr/_WMORegion)|northCentralAmericaCaribbean|WIGOS Metadata Representation, Section 4.3.2

child objects:
* territory
* spatiotemporal
* program_affiliation
* climate_zone
* surface_cover
* surface_roughness
* topography_bathymetry
* observation

#### `territory`

The `territory` object is a child of the `facility` object and
allows for specifying 0..n child objects to model changing territory names
over time.  For fixed land-based stations at least one child object is required. For other stations types it may be omitted.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
name|Mandatory|The territory the observing facility is located in, from the TerritoryType codelist (http://test.wmocodes.info/wmdr/_TerritoryName)|`CAN`|WIGOS Metadata Representation, Section 4.3.2
valid_period|Optional|Specifies at least the begin date of the indicated territoryName. If omitted, the dateEstablished of the facility will be assumed|`begin:2011-11-11`, `end: now`|WIGOS Metadata Representation, Section 4.3.2

#### `spatiotemporal`

The `spatiotemporal` object is a child of the `facility` object and
allows for specifying 1..n child objects to model a moving location
over time.  At least one child object is required.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
timeperiod|Mandatory|Specifies at least the begin date accompanying the location|`begin:2011-11-11`, `end: now`|WIGOS Metadata Representation, Section 4.2.3.2
location|Mandatory.  The location property includes a `crs` property (EPSG code), and `point` property (x,y,z)|Representative or conventional geospatial location of observing facility, the reference location. This will always be a point location, but this location can change with time. |`crs: 4326, point: -75,45,400`, `end: now`|WIGOS Metadata Representation, Section 4.2.3.2

#### `program_affiliation`
The `program_affiliation` object is a child of the `facility` object and
allows for specifying 1..n child objects to model program affiliations.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
program|Mandatory|Program Affiliation, see http://test.wmocodes.info/wmdr/ProgramAffiliation|`GOS`|WIGOS Metadata Representation, Section 4.3.2

child objects:
* reporting_status

#### `reporting_status`
The `reporting_status` object is a child of the `program_affiliation` object and
allows for specifying 1..n child objects to model program affiliations reporting status
over time.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
status|Mandatory|Declared reporting status of the observing facility from the ReportingStatusType codelist (http://test.wmocodes.info/wmdr/_ReportingStatus)|`oerational`|WIGOS Metadata Representation, Section 4.3.3.7
valid_period|Optional|Specifies at least the begin date of the indicated reportingStatus.|`begin:2011-11-11`, `end: now`|

#### `climate_zone`
The `climate_zone` object is a child of the `facility` object and
allows for specifying 0..n child objects to model changing climate zones over time.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
name|Mandatory|Climate zone of the observing facility, from the ClimateZone codelist (http://test.wmocodes.info/wmdr/_ClimateZone)|`snowFullyHumidCoolSummer`|WIGOS Metadata Representation, Section 4.3.3.3
valid_period|Optional|Specifies at least the begin date of the indicated climate zone. If omitted, the dateEstablished of the facility will be assumed|`begin:2011-11-11`, `end: now`|

#### `surface_cover`
The `surface_cover` object is a child of the `facility` object and
allows for specifying 0..n child objects to model changing surface covers over time.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
name|Mandatory|Predominant surface cover, from the given surface cover classification scheme and the SurfaceCover codelist (http://test.wmocodes.info/wmdr/_SurfaceCover)|`rainfedCroplands`|WIGOS Metadata Representation, Section 4.3.3.4
surface_cover_classification|Mandatory|Surface cover classification scheme, from the SurfaceCoverClassification codelist (http://test.wmocodes.info/wmdr/_SurfaceCoverClassification)|`globCover2009`|WIGOS Metadata Representation, Section 4.3.3.4
valid_period|Optional|Specifies at least the begin date. If omitted, the dateEstablished of the facility will be assumed|`begin:2011-11-11`, `end: now`|

#### `surface_roughness`
The `surface_roughness` object is a child of the `facility` object and
allows for specifying 0..n child objects.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
name|Mandatory|Surface roughness of surrounding of the observing facility, from the SurfaceRoughness codelist (http://test.wmocodes.info/wmdr/_SurfaceRoughness)|`rough`|WIGOS Metadata Representation, Section 4.3.3.5
valid_period|Optional|Specifies at least the begin date of the indicated surface roughness. If omitted, the dateEstablished of the facility will be assumed|`begin:2011-11-11`, `end: now`|

#### `topography_bathymetry`
The `topography_bathymetry` object is a child of the `facility` object and
allows for specifying 0..n child objects to model topography or bathymetry descriptions over time.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
local_topography|Optional|Local topography of the observing facility from the LocalTopography codelist (http://test.wmocodes.info/wmdr/_LocalTopography)|`flat`|WIGOS Metadata Representation, Section 4.3.3.6
relative_elevation|Optional|Relative elevation of the observing facility compared to its surrounding, from the RelativeElevation codelist (http://test.wmocodes.info/wmdr/_RelativeElevation)|`inapplicable`|WIGOS Metadata Representation, Section 4.3.3.6
topographic_context|Optional|Topographic context of the observing facility, from the TopographicContext codelist (http://test.wmocodes.info/wmdr/_TopographicContext)|`plains`|WIGOS Metadata Representation, Section 4.3.3.62
altitude_or_depth|Optional|Altitude or depth of observing facility, from the AltitudeOrDepth codelist (http://test.wmocodes.info/wmdr/_AltitudeOrDepth)|`middleAltitude`|WIGOS Metadata Representation, Section 4.3.3.6
valid_period|Optional|Specifies at least the begin date. If omitted, the dateEstablished of the facility will be assumed|`begin:2011-11-11`, `end: now`|

#### `observation`
The `observation` object is a child of the `facility` object and
allows for specifying 0..n child objects to model various observations at the facility. 

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
program_affiliation|Mandatory|Program Affiliation, see http://test.wmocodes.info/wmdr/ProgramAffiliation|`GOS,CLIMATc`|
geometry|Mandatory|From the spatial extend or geometry codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/1-04.csv|`point`|
observed_property|Mandatory|From one of the ObservedVariable codelist https://github.com/wmo-im/wmds/tree/master/tables_en 1-01-01.csv - 1-01-05.csv|`216`|WIGOS Metadata Representation, Section 6.2.5

child objects:
* deployment

#### `deployment`
The `deployment` object is a child of the `observation` object and allows for specifying 1..n child objects. At least one child object is required.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
local_reference_surface|Conditional|Mandatory for instrumental observations or if proximity of ref. surface impacts on observation; From the type of reference surface codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/5-05.csv|`naturalGround`|WIGOS Metadata Representation, Section 7.2.2
height_above_local_reference_surface|Conditional|Mandatory for instrumental observations or if proximity of ref. surface impacts on observation; Height (with unit) above/below local reference surface|`height:2`, `unit:m`|WIGOS Metadata Representation, Section 7.2.2
valid_period|Mandatory|Specifies at least the begin date. If omitted, the dateEstablished of the facility will be assumed|`begin:2011-11-11`, `end: now`|
application_area|Mandatory|Application area(s) from the ApplicationAreas codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/2-01.csv, at least one is required|`nowcasting`,`climateMonitoring`|WIGOS Metadata Representation, Section 7.2.2
source_of_observation|Mandatory|From the sourceOfObservation codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/5-01.csv|`automaticReading`|WIGOS Metadata Representation, Section 7.2.2
communication_method|Optional|From the Data communication metehod codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/3-08.csv|`dataCellular`|WIGOS Metadata Representation, Section 7.2.2
exposure|Conditional|Mandatory for instrumental observations; From the Exposure codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/5-15.csv|`class1`|WIGOS Metadata Representation, Section 7.2.2
representativeness|Optional|From the Representativeness codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/1-05.csv|`toposcale`|WIGOS Metadata Representation, Section 7.2.2

Child objects:
* data_generation

#### `data_generation`
The `data_generation` object is a child of the `deployment` and allows for specifying 1..n child objects. At least one child object is required.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
valid_period|Mandatory|The period of time for which this processing arrangement was/is in place. (Note: this time period must fall within the time period specified in the Deployment). Specifies at least the begin date.|`begin:2011-11-11`, `end: now`|

Child objects:
* schedule
* sampling
* processing
* reporting

#### `schedule`
The `schedule` object is a child of the `data_generation` object. Exactly one child object is required.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
diurnal_base_time|Optional|Time (of day) to which diurnal statistics are referenced. For example, a 24 h accumulated total precipitation might refer to 0700z as the diurnal base time||WIGOS Metadata Representation, Section 7.4.2
end_hour|Mandatory|End hour of schedule (0 to 23)|23|WIGOS Metadata Representation, Section 7.4.2
end_minute|Mandatory|End minute of schedule (0 to 59)|0|WIGOS Metadata Representation, Section 7.4.2
end_month|Mandatory|End month of schedule (January = 1, December = 12)|12|WIGOS Metadata Representation, Section 7.4.2
end_weekday|Mandatory|End day of schedule (Monday = 1, Sunday = 7)|1|WIGOS Metadata Representation, Section 7.4.2
start_hour|Mandatory|Start hour of schedule (0 to 23)|23|WIGOS Metadata Representation, Section 7.4.2
start_minute|Mandatory|Start minute of schedule (0 to 59)|0|WIGOS Metadata Representation, Section 7.4.2
start_month|Mandatory|Start month of schedule (January = 1, December = 12)|1|WIGOS Metadata Representation, Section 7.4.2
start_weekday|Mandatory|Start day of schedule (Monday = 1, Sunday = 7)|7|WIGOS Metadata Representation, Section 7.4.2

#### 'reporting'
The `reporting` object is a child of the `data_generation` object. Exactly one child object is required.

Property Name|Mandatory/Optional|Description|Example|Reference
-------------|------------------|-----------|-------|---------:
international_exchange|Mandatory|A binary element (True/False), that should be associated with the observed variable for each declared observing schedule (temporal_reporting_period) |`True`|Element 7-14  from the WIGSO Metadata Standard
measurement_unit|Mandatory|Unit of measurement from the Measurement unit codelist https://github.com/wmo-im/wmds/blob/Development/tables_en/1-02.csv|`Cel`|WIGOS Metadata Representation, Section 7.7.2
temporal_reporting_interval|Mandatory|Time interval over which the observed variable is reported. Note that this is a temporal distance, e.g., (every) 1 hour. Use ISO8601 notation. |`PT1H`|WIGOS Metadata Representation, Section 7.7.2
time_stamp_meaning|Optional|Meaning of the time stamp in the temporalReportingInterval taken from the TimeStampMeaning codelist.https://github.com/wmo-im/wmds/blob/Development/tables_en/11-03.csv|`end`|WIGOS Metadata Representation, Section 7.7.2


