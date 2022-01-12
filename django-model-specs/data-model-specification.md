## oTherm Data Specification for GSHP Systems

The oTherm framework consists of a backend web application written in Python (Django platform) with two databases 
(SQL and Time Series) that is ‘containerized’ using Docker for efficient deployment.   The front end and APIs supports 
efficient data entry and retrieval. 

The oTherm data models are generally divided into the Device-Level Data Model and the Facility-Level Data Model. 
The rationale for the tables and relationship are covered in some detail in other project documents.   Generally, 
the Device-Level Data Model focuses on monitoring systems and monitoring data while the Facility-Level Data Model 
focuses on information about the site, the thermal sources, and the thermal load.   This Data Specification provides 
a comprehensive description of each of the tables and their relationships.  

![oTherm SQL Structure](./data_structure_emp_sql.png)


### Facility Level Data (SQL)
The static data is stored in a PostgreSQL database and the tables can be split into two general groups.  The first 
group of tables are those that likely contain new and site-specific information.  The second group of 
tables contain information that can likely be utilized by multiple sites.  For example, a monitoring system 
may be defined once and then an instance of that monitoring system may be deployed at multiple sites.   Tables 
with site data can be configured to be accessible to oTherm users while tables that can be used between sites can 
be restricted to those with administrative privileges.   The [SQL data model specification](./django-data-model-specs.pdf) 
provides a detailed description of the SQL tables and fields.
 [here]  

The relationships between the tables is summarized in SchemaSpy images in both [compact](./relationships.real.compact.png) 
and the [large](./relationships.real.large.png) formats.

### Time Series Data (no-SQL)
Time Series Data (No-SQL)
While we often associate the term ‘measurement’ with a single instance. In the context of time series data, a 
measurement is a collection of tags, fields, and timestamps.  

![oTherm Influx Structure](./data_structure_emp_time-series.png)

In oTherm, the heat pump operating data for all heat pumps and all times is considered a measurement ‘monitoring-data’ 
and the weather data is considered a separate measurement (‘weather-data’). The elements for each of these measurements 
are described in the [Time-seried data model specification](./influx-data-model-specs.pdf).

#### Line Protocol Input
In some cases, it may be necessary to upload time series data into the database.  This can be done using text files 
with data in a ‘line protocol’ format.  Each line represents a collection of (1) measurement name, (2) tag key:value pair, 
(3) a set of field key:value pairs, and (4) a time stamp in epoch time   Single spaces delimit each of these elements.  
Key value pairs in a field set are delimited by commas.   It is important that spaces are not included after commas. A 
sample Python Script for creating line-protocol files is provided in the [oTherm GSHP analytics repository](https://github.com/otherm/gshp-analysis) 


## Mapping to related DOE Data Specifications

### Mapping to BEDES
[oTherm mapping to BEDES](./oTherm_BEDES_mapping.pdf)

### Mapping to NGDS 
[oTherm mapping to NGDS](./oTherm_NGDS-HeatPumpFacility_mapping.pdf)
  
