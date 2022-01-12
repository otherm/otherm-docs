### Tables with Site Data

#### Site

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 50 characters | Recommended to be the M&amp;V Program Management 
Identifier without personally identifiable information |
| city | **Required**** Syntax**Max 60 characters | The name of the city or town in which the site is located. |
| state | **Required**** ForeignKey** State.name | The two-character state abbreviation in which the site is located. |
| description | Optional **Syntax** Text field | An optional field for additional information and/or comments. |
| application | **Required**** Syntax**Max 60 characters | Typically used to denote whether renewable thermal 
system is for new construction or retrofit. |
| uuid | **Required**** Syntax**RFC 4122 uuid4()automatically generated
 | Automatically generated universal unique identifier for the site. |
| thermal\_load | **Optional**** ForeignKey** thermal\_load.name | Reference to entry in thermal\_load table 
describing the overall heating and cooling loads for the site. |
| weather\_station | **Required**** ForeignKey** weather\_station.nws\_id | Four-character code for National 
Weather Service station to be used for site weather data. |

#### Equipment

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Recommended format** [site.name]\_thermal-load **Syntax** Max 40 characters | Name 
for the thermal load table entry. This is useful when assigning a thermal load to a site.
In the initial release, a site can only have one thermal load table entry |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| conditioned\_area | **Required**** Syntax**Float fieldUnits = &#39;Sq Ft&#39; | The total floor area of the conditioned 
space served by the renewable thermal system. Future releases may include zones. |
| heating\_design\_load | **Required**** Syntax**Float fieldUnits = &#39;MBtuH&#39; | The peak heating load required to 
meet the indoor design temperature when the outdoor temperature is the heating\_design\_oat. Typically determined from 
an ACCA Manual J analysis. |
| cooling\_design\_load | **Required**** Syntax**Float field, Units: &#39;MBtuH&#39; | The peak cooling load required to
 meet the indoor design temperature when the outdoor temperature is the cooling\_design\_oat. Typically determined from 
 an ACCA Manual J analysis. |
| heating\_design\_oat | **Required**** Syntax**Float field Units: &#39;Degrees F&#39; | The outdoor air temperature for 
which the peak heating load is designed. Typically determined for the location from ASHRAE table. |
| cooling\_design\_oat | **Required**** Syntax**Float fieldUnits: &#39;Degrees F&#39; | The outdoor air temperature for 
which the peak cooling load is designed. Typically determined for the location from ASHRAE table. |
| uuid | **Required**** Syntax**RFC 4122 uuid4()automatically generated
 | Automatically generated universal unique identifier for the thermal load table entry. |

#### Equipment Monitoring System Specification

Maps a pre-defined monitoring system to an existing piece of renewable thermal equipment.

| Attribute | Format | Comments |
| --- | --- | --- |
| equip\_id | **Required**** ForeignKey** equipment.id | ID for the equipment that has a monitoring system attached. |
| monitoring\_system\_spec | **Required**** ForeignKey** monitoring\_system\_spec | id for the monitoring system that is 
attached to equipment. More than one monitoring system may be associated with a piece of equipment |
| start\_date | **Optional**** Syntax**DateField
 | date that the monitoring system went into operation |
| end\_date | **Optional**** Syntax**DateField
 | date that the monitoring system was no longer installed or operating. If a change is made to a monitoring system, 
 the change would be recorded with a new monitoring system with a new start date. |

#### Equipment Maintenance History

| Attribute | Format | Comments |
| --- | --- | --- |
| equip\_id | **Required**** ForeignKey** equipment.id | ID for the equipment that is serviced |
| description | **Required**** Syntax**Text field | description of service done |
| service\_date | **Required**** Syntax**DateField
 | date that the equipment was serviced |
| contractor | **Optional**** Syntax**Max 50 characters
 | The name of the contracting company that performed the service. |
| technician | **Optional**** Syntax**Max 50 characters
 | The name or initials of the technician(s) that performed the service. |

#### Source

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Recommended format** [site.name]\_[source.type] **Syntax** Max 50 characters | Name 
for a thermal source located at a site and associated with one or more pieces of equipment. A site must have at least 
one thermal source and can have more than one.
 |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| type | **Required**** ForeignKey** source.type | The type of thermal source, e.g. vertical borehole heat exchanger. |
| spec | **Required**** ForeignKey** source.spec | The specifications of the thermal source, based on type. |

#### Source Specification

| Attribute | Format | Comments |
| --- | --- | --- |
| uuid | **Required**** Syntax**RFC 4122 uuid4()automatically generated
 | Automatically generated universal unique identifier for the site. |
| name | **Required**** Unique ****Syntax** Max 50 characters | The name of the source specification for the site. While 
a source spec can be used for multiple site, it is most often specific to a site. |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| type | **Required**** ForeignKey** source.type | The type of thermal source, e.g. vertical borehole heat exchanger. |

#### Vertical Loop Specification (Source subclass)

| Attribute | Format | Comments |
| --- | --- | --- |
| formation\_conductivity | **Optional**  **Syntax** Float field | The formation thermal conductivity in units of 
Btu/hr-ft-F. |
| grout\_conductivity | **Optional**  **Syntax** Float field | The grout thermal conductivity in units of Btu/hr-ft-F. |
| grout\_type | **Optional**  **Syntax** Max 50 characters | The of grout used in the borehole heat exchanger |
| freeze\_protection | **Optional**** Syntax**Float | The lowest temperature at which antifreeze will prevent freezing. 
Report in degrees F. |
| formation\_type | **Optional**** Syntax**Max 50 characters | The type of geologic material in which the heat exchanger 
is installed. |
| ghex\_pipe\_spec | **Optional**** Foreign Key**ghex\_pipe\_specification | Mapping to the table with the ground heat 
exchanger pipe specification. |

#### Air Source Spec

| Attribute | Format | Comments |
| --- | --- | --- |
| compressor\_location | **Optional**  **Syntax** Max 25 characters | An optional field to describe the location of 
the air-source heat pump compressor. For example, ground-mount, wall-mount, roof, etc. |
| duct\_configuration | **Optional**  **Syntax** Max 35 characters | An optional field to describe the duct 
configuration of the air-source heat pump. For example., &#39;single-zone ducted&#39;, etc. |

#### Thermal Load

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Recommended format** [site.name]\_thermal-load **Syntax** Max 40 characters | Name 
for the thermal load table entry. This is useful when assigning a thermal load to a site.
In the initial release, a site can only have one thermal load table entry |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| conditioned\_area | **Required**** Syntax**Float fieldUnits = &#39;Sq Ft&#39; | The total floor area of the 
conditioned space served by the renewable thermal system. Future releases may include zones. |
| heating\_design\_load | **Required**** Syntax**Float fieldUnits = &#39;MBtuH&#39; | The peak heating load required to
 meet the indoor design temperature when the outdoor temperature is the heating\_design\_oat. Typically determined from 
 an ACCA Manual J analysis. |
| cooling\_design\_load | **Required**** Syntax**Float field, Units: &#39;MBtuH&#39; | The peak cooling load required to meet the indoor design temperature when the outdoor temperature is the cooling\_design\_oat. Typically determined from an ACCA Manual J analysis. |
| heating\_design\_oat | **Required**** Syntax**Float field Units: &#39;Degrees F&#39; | The outdoor air temperature for which the peak heating load is designed. Typically determined for the location from ASHRAE table. |
| cooling\_design\_oat | **Required**** Syntax**Float fieldUnits: &#39;Degrees F&#39; | The outdoor air temperature for which the peak cooling load is designed. Typically determined for the location from ASHRAE table. |
| uuid | **Required**** Syntax**RFC 4122 uuid4()automatically generated
 | Automatically generated universal unique identifier for the thermal load table entry. |

### Multiple Site Tables

#### Equipment Type

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 20 characters | The type of equipment provided by manufacturer. These are general classes of equipment, such as ASHP, GSHP, etc. |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |

#### GHEX Pipe Specification

| Attribute | Format | Comments |
| --- | --- | --- |
| uuid | **Required**** Syntax**RFC 4122 uuid4()automatically generated
 | Automatically generated universal unique identifier for the thermal load table entry. |
| name | **Required**** Unique ****Syntax** Max 50 characters | A descriptive name of the GHEX pipe specification so that it may be reused on multiple sites. |
| dimension\_ratio | **Optional**  **Syntax** Max 50 characters | The of ratio of the outer pipe diameter to the minimum wall thickness. For example, DR11. |
| no\_flowmeter\_flowrate | **Optional**  **Syntax** Float field | The ground loop flow rate (in gallons per minute) for fixed flow systems without an installed flowmeter. |
| n\_pipes\_in\_circuit | **Optional**  **Syntax** Integer field | The number of pipes in individual circuits. For a single u-tube, the value is 1. |
| n\_circuits | **Optional**  **Syntax** Integer field | The number of circuits in the ground loop. For example, for 2 boreholes with split flow, enter 2. |
| total\_pipe\_length | **Optional**** Syntax**Float | Enter value in units of feet. For a single u-tube in a 200 foot bore, the total pipe length would be 400 feet. |

#### Manufacturer

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 20 characters | Name of the equipment manufacturer. This will typically include manufacturers of renewable thermal equipment and associated monitoring systems. For manufacturers that provide both heat pumps and monitoring systems, enter a separate record for each (e.g. Waterfurnace\_hp and Waterfurnace\_ms) |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| equipment\_type | **Required**** Foreign Key**equipment\_type | The type of equipment provided by manufacturer. Separate records are required for manufacturers that provide multiple types of equipment |

#### Measurement Location

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 20 characters **Examples**
- &#39;in-pipe&#39;
- &#39;heat pump&#39;
- &#39;service panel&#39;
 | Name of the measurement location for a specific sensor of a montirong system. For example, an electrical measurement may be made in the electrical panel or in the heat pump. Temperature measurements may be made with in-pipe sensors or on-pipe sensor affixed the exterior of a pipe. equipment manufacturer. |
| Description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |

#### Measurement Specification

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 30 characters **Examples** See comments | Name of the measurement for a specific sensor of a monitoring system. This name should be informative so that when a measurement specification is added to a monitoring system, the correct measurement specification can be identified from a list of options. For example, a measure of leaving water temperature made on metal pipe in units of Celsius with an accuracy of 0.1C may be &#39;LWT OMP 0.1 C&#39; |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| type | **Required**** Foreign Key**measurement\_type | Mapping of measurement spec to obtain oTherm name, possible MSP names, units. |
| accuracy | **Recommended**** Syntax**Decimal Field 10 digits, 5 decimal | When available, numeric accuracy should be reported. If a % of reading value, the accuracy\_pct attribute should be set to TRUE. Otherwise, accuracy will be interpreted as sensor error in units of measurement\_type. |
| accuracy\_pct | **Recommended**** Syntax**Boolean | Denotes whether accuracy is reported as a percent of reading (TRUE) or in units of measurement\_type (FALSE) |
| meas\_bias\_abs | **Required**** Syntax**Float field | Measurement bias, other than sensor bias. This may due to an incorrect monitoring system setting. Default = 0.0Reported as absolute or percent. |
| meas\_bias\_pct | **Required**** Syntax**Float field | Measurement bias, other than sensor bias. This may due to an incorrect monitoring system setting. Default = 0.0Reported as absolute or percent. |
| location | **Optional**  **Foreign Key** measurement\_location.location | Th location of a measurement. |

#### Measurement Type

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 20 characters **Examples**
- &#39;heatpump\_power&#39;
- &#39;heatpump\_aux&#39;
- &#39;source\_supplytemp&#39;
 | oTherm measurement type name for a specific sensor of a monitoring system. These should coincide with names in Table 3 of the Device Level Data Dictionary. |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| msp\_colunns | **Optional**  **Syntax** Array field | An optional list of coinciding column names for data provided by monitoring system provider (msp). |
| unit | **Required**** Foreign Key**Measurement\_unit.name | The abbreviation of measurement unit, such as &quot;C&quot; for Celsius, &quot;W&quot; for Watts, etc. |

#### Measurement Unit

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 10 characters **Examples**
- &#39;C&#39;, &#39;F&#39;, &#39;W&#39;, &#39;gpm&#39;, etc.&#39;

 | Measurement unit abbreviation |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |

#### Model

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 20 characters | Name of the equipment manufacturer. This will typically include manufacturers of renewable thermal equipment and associated monitoring systems. For manufacturers that provide both heat pumps and monitoring systems, enter a separate record for each (e.g. Waterfurnace\_hp and Waterfurnace\_ms) |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| equipment\_type | **Required**** Foreign Key**equipment\_type | The type of equipment provided by manufacturer. Separate records are required for manufacturers that provide multiple types of equipment |

#### Monitoring System

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 40 characters | Name of the monitoring system should be sufficient so that user can select correct one when associating a monitoring system with a piece of equipment. |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. Notes on known measurement bias should be included here. |
| manufacturer
 | **Required**** Foreign Key**manufacturer | The manufacturer of the monitoring system. |

#### Source Type

| Attribute | Format | Comments |
| --- | --- | --- |
| name | **Required**** Unique ****Syntax** Max 50 characters | The name of the general type of thermal source, for example, air source, ground source, district, etc. |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |

#### Weather Station

| Attribute | Format | Comments |
| --- | --- | --- |
| nws\_id | **Required**** Unique ****Syntax** Max 30 characters **Example**&#39;KPSM&#39; for Portsmouth NH | The National Weather Service station identifier that is most representative of weather conditions at the site. |
| description | **Optional**  **Syntax** Text field | An optional field for additional information and/or comments. |
| lat | **Required**** Syntax**Float field Units: Decimal Degrees | The latitude of the NWS station. |
| lon | **Required**** Syntax**Float field Units: Decimal Degrees | The longitude of the NWS station. For North America, typically reported in negative degrees relative to the prime meridian. |

## Time Series Data (No-SQL)

![](RackMultipart20220112-4-1ltd4ad_html_da8630bdafb307b2.png)While we often associate the term &#39;measurement&#39; with a single instance. In the context of time series data, a measurement is a collection of tags, fields, and timestamps.

In oTherm, the heat pump operating data for all heat pumps and all times is considered a measurement &#39;monitoring-data&#39; and the weather data is considered a separate measurement (&#39;weather-data&#39;). The elements for each of these measurements are described in the tables below.

### Monitoring Data

| Data Element | Format | Comments |
| --- | --- | --- |
| timestamp | **Required**** Format on input**epoch (unix timestamp)Example: 1577836800**Format on output **RFC3339Example: 2020-01-01T00:00:00.00Z** Precision**seconds | When inputting time series data with a text file, the line protocol format requires that time is entered in epoch time. In oTherm, the precision is defined as &#39;seconds&#39; |
| tag | **Required**** tag key: **&#39;equipment-uuid&#39;** tag value:** equipment.uuid
 | Each time series record for heat pump operating is tagged with the equipment uuid. |
| field | **Required**** field key: **name of measurement typeExample:&#39;source\_supplytemp&#39;** field value:** float | Name of measurement type for monitoring system.
MeasurementType.name Each record must have least one field and most records will have multiple fields constituting a &#39;field set&#39;. |

### Weather Data

| Data Element | Format | Comments |
| --- | --- | --- |
| timestamp | **Required**** Format on input**epoch (unix timestamp)Example: 1577836800**Format on output **RFC3339Example: 2020-01-01T00:00:00.00Z** Precision**seconds | When inputting time series data with a text file, the line protocol format requires that time is entered in epoch time. In oTherm, the precision is defined as &#39;seconds&#39; |
| tag | **Required**** tag key:**National Weather Service Station ID (e.g, &#39;KPSM&#39;)**tag value:** weather\_station.name
 | Each time series record for weather data is tagged with the weather station name. |
| field | **Required**** field key: **name of weather measurement Example:&#39;temperature\_c&#39;** field value:** float | Name of weather measurement type
Each record must have least one field and most records will have multiple fields constituting a &#39;field set&#39;. |

### Line Protocol Input

In some cases, it may be necessary to upload time series data into the database. This can be done using text files with data in a &#39;line protocol&#39; format. Each line represents a collection of (1) measurement name, (2) tag key:value pair, (3) a set of field key:value pairs, and (4) a time stamp in epoch time Single spaces delimit each of these elements. Key value pairs in a field set are delimited by commas. It is important that spaces are not included after commas.