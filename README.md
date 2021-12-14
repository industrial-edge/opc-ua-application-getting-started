# OPC UA Application example

This example shows how to use Industrial Edge OPC UA Application.

- [OPC UA Application example](#opc-ua-application-example)
  - [Description](#description)
    - [Overview](#overview)
    - [General Task](#general-task)
  - [Requirements](#requirements)
    - [Prerequisites](#prerequisites)
    - [Used components](#used-components)
  - [Installation](#installation)
  - [Usage](#usage)
  - [Documentation](#documentation)
  - [Contribution](#contribution)
  - [License and Legal Information](#license-and-legal-information)

## Description

### Overview

IE OPC-UA Application acts as OPC-UA server. It collects data from IE connector like Profinet IO, Simatic S7 connector, Modbus TCP Connector, Ethernet IP Connector. Then collected data, makes available for OPC-UA clients. In this example, data were collected from PLC and KPIs were calculated. Then 

### General Task

What is the general goal/task of this how-to/tutorial?

![task](docs/graphics/example_graphic.png)

## Requirements

### Prerequisites

- Access to an Industrial Edge Management System (IEM)
- Onboarded Industial Edge Device (IED) on IEM
- Installed System Configurators for Databus
- Installed System Apps Databus
- Installed and running all connectors and configurators (S7 conector, PROFINET IO, ModbusTCP) that App uses
- Installed OPC UA configurator and OPC UA Application
- Google Chrome (Version ≥ 72) or Firefox (Version ≥ 62)

### Used components

List the used software and hardware components that were tested with this how-to.
Add the used components here (e.g.)

* Industrial Edge App Publisher V1.0.8
* Docker Engine 18.09.6
* Docker Compose V2.4
* S7 Connector V 1.0.22
* S7 Connector Configurator V 1.0.9
* Industrial Edge Device V 1.0.0-34
* TIA Portal V16
* PLC: CPU 1511 FW 2.8.3

## Installation

How to install/run this application example? (i.e. how to deploy it to Industrial Edge device?) How to build this application? How to set up configurations in IE?

To keep the readme.md file as short as possible please add more detailed information in the docs folder.

* [Build application](docs/Installation.md#build-application)

## Usage

When the app is installed, how can I use it? Usually some basic UI description to prove that the app is working correctly.

## Documentation

Add links to documentation. Either on external URL or in the doc folder. Please use always link to a file not to a directory (it doesn't work with static site generator engines).

Add these links:

You can find further documentation and help in the following links

* [Industrial Edge Hub](https://iehub.eu1.edge.siemens.cloud/#/documentation)
* [Industrial Edge Forum](https://www.siemens.com/industrial-edge-forum)
* [Industrial Edge landing page](https://new.siemens.com/global/en/products/automation/topic-areas/industrial-edge/simatic-edge.html)
* [Industrial Edge GitHub page](https://github.com/industrial-edge)

## Contribution

Thank you for your interest in contributing. Anybody is free to report bugs, unclear documentation, and other problems regarding this repository in the Issues section. Everybody is free to propose any changes to this repository using Pull Requests.

## License and Legal Information

Please read the [Legal information](LICENSE.md).
