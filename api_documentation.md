# oTherm API Documentation

The primary method to access data in an oTherm instance is through a set of APIs.  The recommended usage is to use them from a python script.  For example,
```python
import requests

site_name = '03824'
site_url = "https://[otherm_instance_url]/api/site/?name=%s" % (site_name)
site_response = requests.get(site_url, auth=([username], [password]))

site_dict = site_url.response()[0]

```

## Site Endpoint
Retrieves data about an oTherm site.

| API Endpoint | 
|------------|  
|/api/site/|

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| name | Optional  | site name | string |
| id  | Optional | site id  | int |

If no query pameter is provided, information for all sites is returned.

### Response
```json
[{id:1,
  name:"Keene NH",
  description:"Single family residence",
  city:"Keene",
  zip_code:"03455",
  application:"New construction",
  uuid:"0483e71e-974c-4ea6-8096-640c2ed9c44a",
  state:"New Hampshire",
  timezone:"US/Eastern",
  thermal_load:"adcedbf2-4a11-4f4d-890a-64c7430092f7",
  weather_station_nws_id:"KPSM"}
]
```
## Equipment Endpoint

| API Endpoint | 
| ------------------|  
|/api/equipment/|

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| site | Required | Site id | int |

### Response
```json
[{id:3,
  uuid:"a5521cc6-825b-450b-a487-637b002777ea",
  model:"HXT048",
  description:"GES install 45",
  type:2,
  site:2,
  manufacturer:3,
  no_flowmeter_flowrate:null,
  maintenance:3,
  maintenance_history:{
      id:3,
      name:"Commissioning",
      service_date:"2016-01-03",
      description:"On site commissioning and  verification of monitoring system",
      contractor:"ABC geo",
      technician:"jmd",
      equip_id:3}
}]
```

## Equipment Data Endpoint
Returns monitoring data for all equipment at a site.  
  
|  API Endpoint   | 
| --------------- |  
| /api/equipment_data/ |
 

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| site | Required | Site id | int |
| start_date | Optional | Start date of records to retrieve in format `YYYY-MM-DD` | string |
| end_date | Optional | End of record to retrieve, in format `YYYY-MM-DD` | string |

### Response
List of json objects, each with monitoring data for a piece of equipment 
```json
 [{id:5,
  uuid:"5406f27f-5b03-4435-b705-fbdd3e814696",
  model:"HXT048",
  description:"",
  type:2,
  site:3,
  manufacturer:3,
  heat_pump_metrics:[
    {time:"2016-01-01T00:00:18Z",
       equipment:"5406f27f-5b03-4435-b705-fbdd3e814696",
       heat_flow_rate :null,
       heatpump_aux:0.0,
       heatpump_power:null,
       outdoor_temperature:3.0,
       source_returntemp:null,
       source_supplytemp:10.187292008993,
       sourcefluid_flowrate:0.0},
    {time:"2016-01-01T00:35:54Z",
       equipment:"5406f27f-5b03-4435-b705-fbdd3e814696",
       heat_flow_rate:17105.2249418171,
       heatpump_aux:0.0,
       heatpump_power:1359.6,
       outdoor_temperature:3.0,
       source_returntemp:6.5596691201413,
       source_supplytemp:8.749792008993,
       sourcefluid_flowrate:9.0}]]
```
## Equipment Specifications Endpoint
Returns heating and cooling capacities of equipment

| API Endpoint | 
| ------------------|  
|/api/equipment_specs/|

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| model | Optional | equipment model | string |

### Response
```json
[{n_stages:12,
  manufacturer:7,
  equip_model_info:{id:"EX-MR036",
                    equipment_type:{name:"ASHP"},
                                    model_number:null,
                                    manufacturer:7},
                    equip_specs:{id:4,
                                 name:"Example spec",
                                 uuid:"1b16eb2c-2bfa-4b6c-9f17-d55f93886159",
                                 description:"",
                                 n_stages:12,
                                 hc_at_5F:1.0,
                                 hc_at_17F:2.0,
                                 hc_at_47F:3.0,
                                 cc_at_82F:4.0,
                                 cc_at_95F:5.0,
                                 cop_at_5F:6.0,
                                 cop_at_17F:7.0,
                                 cop_at_47F:8.0,
                                 cop_at_82F:9.0,
                                 cop_at_95F:10.0,
                                 manufacturer:7,
                                 model:"EX-MR036"}}]
```

## Monitoring System Endpoint
Returns specification of one ore more monitoring systems

|  API Endpoint   | 
| --------------- |  
| /api/monitoring_system/ |

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| name | Optional | Name of monitoring system.  If not provided, specs for all monitoring systems are returned | string |


### Response
```json
[{id:1,
  name:"GxTracker Power",
  description:"",
  manufacturer:1,
  monitoring_system_specs:
      [{uuid:"89f2138a-98ad-442a-8899-f22debe16af3",
            measurement_spec:{name:"HPP VA W 8% EP",
                          description:"Heat pump power, volt-amps, electrical panel",
                          type:{name:"heatpump_power",
                                msp_columns:null,
                                description:""},
                          accuracy:8.00000,
                          accuracy_pct:true,
                          meas_bias_abs:0.0,
                          meas_bias_pct:0.0,
                          location:{name:"Electrical Panel",
                                    description:""},
                          unit:{name:"W","description":"watts"}}},
       {uuid:"ada86c55-6b61-4044-8775-77a7d7a7aa03",
            measurement_spec:{name:"LWT OMP 0.1 C",
                          description:"source return temperature, on metal pipe, calibrated",
                          type:{name:"source_returntemp_C",
                                msp_columns:null,
                                description:"source return (leaving) water temperature"},
                          accuracy:0.10000,
                          accuracy_pct:false,
                          meas_bias_abs:0.0,
                          meas_bias_pct:0.0,
                          location:{name:"on metal pipe",
                                    description:""},
                          unit:{name:"C",
                                description:"degrees Celsius"}}},
         {uuid:"ba2060c5-7027-447c-b50a-a327d5250543",
              measurement_spec:{name:"EWT OMP 0.1 C",
                            description:"source fluid supply temp on metal pipe, calibrated sensor",
                            type:{name:"source_supplytemp_C",
                                  msp_columns:null,
                                  description:"ground loop source (entering) water temperature"},
                            accuracy:0.10000,
                            accuracy_pct:false,
                            meas_bias_abs:0.0,
                            meas_bias_pct:0.0,
                            location:{name:"on metal pipe",
                                      description:""},
                            unit:{name:"C",
                                  description:"degrees Celsius"}}},
         {uuid:"f11340cf-800d-446f-99b4-5617717039b3",
              measurement_spec:{name:"AuP VA W 8% HP",
                            description:"Aux power with volt-amps in heat pump",
                            type:{name:"heatpump_aux",
                                  msp_columns:null,
                                  description:"auxiliary electric heat"},
                            accuracy:8.00000,
                            accuracy_pct:true,
                            meas_bias_abs:0.0,
                            meas_bias_pct:0.0,
                            location:{name:"heat pump",
                                      description:""},
                            unit:{name:"W",
                                  description:"watts"}}}]}]
```
## Equipment Monitoring Endpoint
Returns the monitoring system information for a specified piece of equipment

|  API Endpoint   | 
| --------------- |  
| /api/equipment_monitoring/ |

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| equip_id | Required | Postgres id of equipment (not uuid) | string |


### Response
```json
[{id:1,
  start_date:"2012-06-01",
  end_date:null,
  equip_id:3, 
  monitoring_system_spec:1,
      monitoring_sys_info:{id:1,
                           name:"GxTracker Power",
                           description:"",
                           manufacturer:1,
                           monitoring_system_specs:[*see monitoring_system api*]}}]  
```

## Thermal Source Endpoint
Returns the thermal sources for a site.


|  API Endpoint   | 
| --------------- |  
| /api/thermal_source/ |

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| site  | Required | Site id | int |

### Response
```json

[{id:2,
  site:2,
  source_id:1,
  name:"site_source_map",
  source_info:{id:1,
               uuid:"cee6ac70-053c-40c1-8eab-0333f5d2f1e7",
               name:"vertical_ghex",
               description:"",
               spec:2,
               source_type:{id:1, 
                            name:"ground source",
                            description:""},
               source_spec_info:{freeze_protection:20.0, 
                                 grout_type:"enhanced",
                                 formation_conductivity:2.2,
                                 formation_type:"rock",
                                 grout_conductivity:1.2,
                                 antifreeze_info:
                                      {id:1,
                                       name:"Kilfrost GEO",
                                       description:""},
                                 ghex_specs:{id:1,
                                             uuid:"6f3519bb-4b68-4a10-9f8e-95e6e2d26014",
                                             name:"2 x 2 x 400 ghex pipe spec",
                                             dimension_ratio:"DR11",
                                             n_pipes_in_circuit:2,
                                             n_circuits:2,
                                             total_pipe_length:400.0}}}}]
```
## Thermal Load Endpoint
Returns the thermal load specs for a site


|  API Endpoint   | 
| --------------- |  
| /api/thermal_load/ |

### Query Parameters

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| id  | Required | Site id | int |

### Response
```json
[{id:2,
  name:"Durham",
  city:"Durham",
  state:"New Hampshire",
  thermal_load:{uuid:"f219d328-bd69-4ed9-ac6d-7da5585c6794",
                name:"load for Durham site",
                description:"",
                conditioned_area:2200.0,
                heating_design_load:38.0,
                cooling_design_load:62.0,
                heating_design_oat:-2.0,
                cooling_design_oat:90.0}}]
```

## Weather Data Endpoint
Returns the weather data observations for specified weather station.  Data must be in the oTherm database.

|  API Endpoint   | 
| --------------- |  
| /api/weather_station/ |

| Query string parameter | Required/optional | Description | Type |
| ----------------------- | ---------------| ------------ | -------- |
| nws_id | Required | Weather station id  | string |
| start_date | Optional | Start date of records to retrieve in format `YYYY-MM-DD` | string |
| end_date | Optional | End of record to retrieve, in format `YYYY-MM-DD` | string |

```json
[{nws_id:"KPSM",
  lat:43.083,
  lon:-70.817,
  weather_data:[{time:"2019-12-06T13:56:00Z",
                 humidity_percent:57.16,
                 pressure_kpa:101.73, 
                 site:"KPSM",
                 temperature_c:-2.9},
                {time:"2019-12-06T14:56:00Z",
                 humidity_percent:56.02,
                 pressure_kpa:101.73,
                 site:"KPSM",
                 temperature_c:-2.2}]}]
```
[oTherm homepage](./)