# OPC UA Application example

This example shows how to use Industrial Edge OPC UA Application.

- [OPC UA Application example](#opc-ua-application-example)
  - [Description](#description)
    - [Overview](#overview)
    - [General Task](#general-task)
  - [Requirements](#requirements)
    - [Prerequisites](#prerequisites)
    - [Used components](#used-components)
    - [TIA Project](#tia-project)
  - [Configuration steps](#configuration-steps)
  - [Usage](#usage)
  - [Documentation](#documentation)
  - [Contribution](#contribution)
  - [License and Legal Information](#license-and-legal-information)
  - [Disclaimer](#Disclaimer)

## Description

### Overview

Industrial Edge OPC UA application acts as OPC UA server. It connects to the data source and extract the data using Industrial Edge Databus (Databus). The data source can be OPC UA Connector, PROFINET IO Connector, Modbus TCP Connector and Ethernet/IP Connector. Customized data sources can also be created. When data are connected and server configured, data becomes available for OPC UA clients.

### General Task

In this example, data were collected from PLC with OPC UA connector and publish to Databus. From that data, in Flow Creator, KPIs were calculated and new custom data source is created. OPC UA Application, subscribes to these two data sources and makes them available for OPC UA clients. As client, another Industrial Edge device can be used or some another application like UA Expert.

![opcnew.PNG](docs/graphics/opcnew.PNG) 


## Requirements

### Prerequisites

- Access to an Industrial Edge Management System 
- Onboarded Industial Edge Device on Industrial Edge Management 
- Installed System Configurators for Databus
- Installed System Apps Databus
- Installed and running all connectors and configurators (OPC UA Connector, PROFINET IO, ModbusTCP) that Application uses
- Installed OPC UA connector
- Installed Flow Creator
- Google Chrome (Version ≥ 72) or Firefox (Version ≥ 62)

### Used components

- Industrial Edge Management (IEM) V1.14.10
- Databus V2.2.0-3
- Common Configurator V1.9.0-4
- OPC UA Connector V2.0.1-0
- Flow Creator V1.16.0
- Industrial Edge Device V1.16.1.1-a
- TIA Portal V18
- PLC S7-1513
- Web browser (Mozilla or Chrome)

### TIA Project

The used TIA Portal project can be found in the [miscellenous repository](https://github.com/industrial-edge/miscellaneous/tree/main/tank%20application) and is also used for several further application examples.

## Configuration steps

You can find the further information about the following steps in the [docs](docs/Installation.md)

- Configure Databus
- Configure OPC UA Connector
- Collect data in Flow Creator and calculate KPIs
- Create custom data source (new metadata, publish data to new topic)
- Install and configure OPC UA connector 

## Usage

When previous steps are configured correctly, data are available in OPC UA Application. Use UA Expert to connect to OPC UA Application at end point `opc.tcp://Ip-Address-of-Edge-Device:48010`. You can also use second IED. Then data is obtained via OPC UA Connector.

![/UAexpertopcuaPNG.PNG](docs/graphics/UAexpertopcuaPNG.PNG)

![uaexpertdatasource.PNG](docs/graphics/uaexpertdatasource.PNG)

## Documentation

- You can find further documentation and help in the following links

 - [Industrial Edge Hub]( https://iehub.eu1.edge.siemens.cloud/#/documentation)
 - [Industrial Edge Forum]( https://forum.mendix.com/link/space/industrial-edge)
 - [Industrial Edge landing page]( https://new.siemens.com/global/en/products/automation/topic-areas/industrial-edge/simatic-edge.html)
 - [Industrial Edge GitHub page]( https://github.com/industrial-edge)
 - [Industrial Edge documentation page]( https://docs.eu1.edge.siemens.cloud/index.html)

 
## Contribution

Thank you for your interest in contributing. Anybody is free to report bugs, unclear documentation, and other problems regarding this repository in the Issues section. Additionally everybody is free to propose any changes to this repository using Pull Requests.

If you haven't previously signed the [Siemens Contributor License Agreement](https://cla-assistant.io/industrial-edge/) (CLA), the system will automatically prompt you to do so when you submit your Pull Request. This can be conveniently done through the CLA Assistant's online platform. Once the CLA is signed, your Pull Request will automatically be cleared and made ready for merging if all other test stages succeed.
 


## License and Legal Information

Please read the [Legal information](LICENSE.txt).

## Disclaimer

IMPORTANT - PLEASE READ CAREFULLY:

 

This documentation describes how you can download and set up containers which consist of or contain third-party software. By following this documentation you agree that using such third-party software is done at your own discretion and risk. No advice or information, whether oral or written, obtained by you from us or from this documentation shall create any warranty for the third-party software. Additionally, by following these descriptions or using the contents of this documentation, you agree that you are responsible for complying with all third party licenses applicable to such third-party software. All product names, logos, and brands are property of their respective owners. All third-party company, product and service names used in this documentation are for identification purposes only. Use of these names, logos, and brands does not imply endorsement.




