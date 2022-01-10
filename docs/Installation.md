# Configuration

- [Configuration](#configuration)
  - [Configure IE Databus](#configure-ie-databus)
  - [Configure IE S7 Connector](#configure-ie-s7-connector)
  - [Collect data in IE Flow Creator and calculate KPIs](#collect-data-in-ie-flow-creator-and-calculate-kpis)
  - [Create custom data source (new metadata, publish data to new topic)](#create-custom-data-source-new-metadata-publish-data-to-new-topic)
  - [Install and configure OPC UA configurator and application](#install-and-configure-opc-ua-configurator-and-application)
  
## Configure IE Databus

In your IEM open the IE Databus and launch the configurator.
Add a user with this topic:
`"ie/#"`

![ie_databus_user](graphics/IE_Databus_User.png)

![ie_databus](graphics/IE_Databus.png)

Deploy the configuration.

## Configure IE S7 Connector

In your IEM open the Simatic S7 Connector and launch the configurator.

Add a data source:

![S7_connector_data_source](graphics/S7_Connector_Data_Source.png)

Add needed tags (since we want to write variable values into the PLC, set "Read & Write" as access mode):

![s7_connector_config](graphics/S7_Connector_Configuration.png)

Edit the settings for Databus in upper right corner:

![s7_connector_settings](graphics/S7_Connector_Settings.png)

>Hint: Username and password should be the same as it was set in the IE Databus configuration, e.g., "edge" / "edge".

Deploy and start the project.

## Collect data in IE Flow Creator and calculate KPIs

Open the IE Flow Creator App from the IED Web UI and import the [FlowCreator.JSON](src/FlowCreator.JSON) file from the source folder.

![importFlowCreator.PNG](graphics/importFlowCreator.png)

![importFlow2.PNG](graphics/importFlow2.png)

After importing the JSON file, the password for IE Databus must be entered in the security settings of the MQTT-node.

![MQTTNode.PNG](graphics/MQTT_node.png)

![SecuritySetting.PNG](graphics/SecuritySetting.png)

When flow is imported, it should look like:

![FlowCreator.png](graphics/FlowCreator.png)

Metadata from all connectors are coming in topic `ie/m/#`.
**Yellow** group, receives all metadata and builds `NameIDMap` global map with name-ID pairs.
**Blue** group receives dataPoints from all connectors and builds two global maps `IDValueMap` with ID-Value and `IDTimestampMap` with ID-Timestamp values.
**Green** group is used for setting metadata and topics for new data source. Metadata and dataPoints needs to follow common payload JSON format.

![MetadataPayload.png](graphics/MetadataPayload.png)

![DataPointsPayload.png](graphics/DataPointsPayload.png)

Topic for new metadata is `ie/m/j/simatic/v1/opcua1/dp` and topic for dataPoints is `ie/d/j/simatic/v1/opcua1/dp/r`.

## Create custom data source (new metadata, publish data to new topic)

**Orange** group in Flow Creator, calculates KPI when new data comes. Then, it formats the data in JSON payload format and sends to topic `ie/d/j/simatic/v1/opcua1/dp/r`.

![KPI_JSON.png](graphics/KPI_JSON.png)

## Install and configure OPC UA configurator and application
