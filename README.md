# thingworx-influxdb-flux-toolbox
[**Unofficial/Not Supported**] Contains capability to query in ThingWorx aggregated data from InfluxDB Cloud TSM

**This Extension is provided as-is and without warranty or support. It is not part of the PTC product suite. This project is licensed under the terms of the MIT license.**
Considering the statement above, in case you have any questions regarding this extension:
- do **not** open PTC Technical Support tickets for this extension (since it is not part of the PTC product suite)

This extension allows using InfluxDB Cloud TSM's data aggregation capabilities through Flux.<br>
It does that by effectively using the aggregateWindow() Flux function that is called through the ThingWorx PostText ContentLoader snippet.<br>
The main service in this Extension has a signature similar to QueryNamedPropertyHistory in order to be easy to use by the user. <br>
It contains 3 ThingWorx entities, a ThingShape and 2 Datashapes (there is no Java code).

## How to Use in ThingWorx
1. Download the extension from the Releases section.
2. Install the extension in ThingWorx
3. Assign the **Influx.TS** ThingShape to any Thing or ThingTemplate. This will expose access to the **QueryNamedPropertyHistoryInflux** service.
4. From the Thing execute the service **QueryNamedPropertyHistoryInflux** to read aggregated data from Influx DB Cloud TSM directly. Note there are two other services that are not meant to be used by the user.
   
Input parameters:
     
- **propertyNames**: infotable that contains the name/names of the properties that need to be aggregated on InfluxDB. This is the primary parameter and data must exist for these properties in the Influx server in order for this service to work.
     Note: the fieldType is not used as of now
- **startDate** and **endDate**: start and end dates for the data range to be queried in Influx.
     Note: specifying a large time range can lead to increased processing times in Influx, especially if the createEmpty values parameter = true or if the groupByTimeResolution is too high.
- **groupByTimeResolution**: specify the time resolution of the aggregated data. Examples:1ms,1s,1m,1h,1d,1w,1mo,1y. Duration of the group by time. Units of measure are available here: https://docs.influxdata.com/flux/v0/data-types/basic/duration/
- **createEmptyValues**: if true, InfluxDB will generate rows for each time range specified in the groupByResolution. These rows will contain no data if fillMissingData is set to false (eg: they will contain only timestamp).
     Note: activating this in conjunction with a large time range and a high groupByTimeResolution can lead to increased processing times in InfluxDB.
- **fillMissingData**: if true, InfluxDB will fill in the empty cell data with values, depending on the fillMissingDataUsePrevious parameter.
- **fillMissingDataUsePrevious**: if true, InfluxDB will use the previous value in order to fill in missing data. Otherwise, it will use 0 as a fill in data.

**This Extension is provided as-is and without warranty or support. It is not part of the PTC product suite**. This project is licensed under the terms of the MIT license.
