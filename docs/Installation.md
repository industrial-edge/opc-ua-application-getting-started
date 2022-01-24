# Configuration

- [Configuration](#configuration)
  - [Configure IE Databus](#configure-ie-databus)
  - [Configure IE SIMATIC S7 Connector](#configure-ie-simatic-s7-connector)
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

## Configure IE SIMATIC S7 Connector

In your IEM open the SIMATIC S7 Connector and launch the configurator.

Add a data source:

![S7_connector_data_source](graphics/S7_Connector_Data_Source.png)

Add needed tags (since we want to write variable values into the PLC, set "Read & Write" as access mode):

![s7_connector_config](graphics/S7_Connector_Configuration.png)

>Hint: Use the same tag names “ProducedBottles” and “FaultyBottles”. This names are used to calculate KPI in Flow Creator. If you change the names here, change it also in Flow Creator.

Edit the settings for Databus in upper right corner:

![s7_connector_settings](graphics/S7_Connector_Settings.png)

>Hint: Username and password should be the same as it was set in the IE Databus configuration, e.g., "edge" / "edge".

Deploy and start the project.

## Collect data in IE Flow Creator and calculate KPIs

Open the IE Flow Creator App from the IED Web UI and import the [flows.json](../src/flows.json) file from the source folder.

![importFlowCreator.PNG](graphics/importFlowCreator.png)

![importFlow2.PNG](graphics/importFlow2.png)

When flow is imported, it should look like:

![FlowCreator.png](graphics/FlowCreator.png)

After importing the JSON file, the password for IE Databus must be entered in the security settings of the MQTT-node.

![MQTTNode.PNG](graphics/MQTT_node.png)

![SecuritySetting.PNG](graphics/SecuritySetting.png)

Metadata from all connectors are coming in topic `ie/m/#`. **Yellow** group, receives all metadata and builds `NameIDMap` global map with name-ID pairs. Enabling debug node, metadata can be visible in debug window.

>HINT: Metadata are retentive and are not pushed constantly. They are published on establishing connection or on change.

**Blue** group receives dataPoints from all connectors and builds two global maps `IDValueMap` with ID-Value and `IDTimestampMap` with ID-Timestamp values. These maps stores only the last value.

## Create custom data source (new metadata, publish data to new topic)

**Green** group is used for setting metadata for new data source. Metadata and dataPoints needs to follow common payload JSON format. Topic for new metadata is `ie/m/j/simatic/v1/opcua1/dp` and topic for dataPoints is `ie/d/j/simatic/v1/opcua1/dp/r/OPCUA/default`. In inject node "set", you can customize your new metadata topic. There, you need to add name and type of connector, topic and definitions for data points. Because of the way of building global maps and storing data, IDs of new data points should be unique. Here, we are using "ProductionQuality" to calculate production KPI and "test" to test connection. When you finish, press "set". This needs to be done at least ones for flow to work. To delete metadata topic, click on "reset" node.

>Hint: Metadata MQTT node should be retained.

![MetadataPayload.png](graphics/MetadataPayload.png)

![RetainMetadata.png](graphics/RetainMetadata.png)

**Orange** group in Flow Creator, calculates KPI. When new "ProducedBottles" value comes, "ProductionQuality" KPI is calculated with this formula:

`"ProductionQuality" = 100 - ("FaultyBottles" / "ProducedBottles") * 100`

Then, it formats the data in common payload format and sends it to topic `ie/d/j/simatic/v1/opcua1/dp/r/OPCUA/default`.

![DataPointsPayload.png](graphics/DataPointsPayload.png)

![KPI_JSON.png](graphics/KPI_JSON.png)

## Install and configure OPC UA configurator and application

When previous steps are completed and KPI is calculated, OPC UA needs to be configured. This is done in IE Management -> Data Connections.

![OPCUAStatus.png](graphics/OPCUAStatus.png)

First, configure data source connection under "Data Source" tab. Insert new custom data source with KPI values. Here, you can also insert different connectors like SIMATIC S7 connector, Modbus TCP connector, PROFINET IO Connector... When you finish, you must either click **Deploy** or click **Add Data Source** icon to reflect the changes on the corresponding data points.

![OPCUAEditDataSource.png](graphics/OPCUAEditDataSource.png)

In "Data Points" tab, you can view and select all data points from configured data sources that needs to be available for external OPC UA clients.

![OPCUAEditDataPoints.png](graphics/OPCUAEditDataPoints.png)

Next, select security policy under "Security" tab. For now, select security to **None**, deselect other 2 options and choose **Generate self signed certificate**.

![OPCUASecurity.png](graphics/OPCUASecurity.png)

In "User Management" you can create a OPC UA users. Select **Enable guest access** and deselect- "User name and password authentication". Later, configure security according your demands.

![OPCUAUser.png](graphics/OPCUAUser.png)

Finally click **Deploy**.

After deployment finishes, data points will be available for OPC UA clients.
You can use UE Expert or second IED to test is it working. 
