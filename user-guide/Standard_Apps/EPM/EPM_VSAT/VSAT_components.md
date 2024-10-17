---
uid: VSAT_components
---

# DataMiner EPM VSAT Components

## Connectors

### EPM Connectors
EPM connectors constitute the core of the EPM Solution. They carry out the necessary logic to aggregate and display the information of the different topology levels. EPM connectors rely on collectors and system connectors to feed information into the EPM engine.

Compatible connectors ship with the EPM Solution package and are shown below.
  -[Skyline EPM Platform VSAT GEO](https://catalog.dataminer.services/details/11f62997-a866-4c02-9f64-03dcfcac96ed)

### Collector Connectors
Collector connectors interface with the main data sources (iDirect Evolution, iDirect Dialog, SES Skala, Intelsat Flex, etc.). For example, we use collector connectors to poll an iDirect Evolution NMS and obtain the necessary information needed to present remote information data throughout the EPM topology. While these connectors ship out with the solution packages, they need to be contracted separately as necessary.

Compatible connectors are shown below, are available for trial and require additional licensing requirements. Please contact your sales representative for assistance or additional information.
  -[iDirect Evolution Platform VSAT](https://catalog.dataminer.services/details/67205de6-f339-43ea-9f1f-511c99d66337)
  -[Newtec Dialog Platform VSAT](https://catalog.dataminer.services/details/cd6febc7-9b01-4a5d-bf28-9346d873da86)

## Peripherals
Peripherals are optional but not required as part of a standard deployment.

### Sun Outage
With the "Generic Sun Outage" connector, a sun outage schedule can be made that predicts sun outages and the impact these may have on the signal and tracking of a VSAT terminal. DataMiner is capable of detecting sun outage events and offering the current state details of each remote in the VSAT system. Sun outages usually occur twice a year during the equinox in March and September.

The "Skyline EPM Platform VSAT DSM SO" serves two main functions which compliments the collector.
  -User defined ES & Sat subscriptions which provides a way for users to map technology specific parameters against the common set of parameters.
  -Exports the resulting dataset following the format required by the collector for further processing.

Compatible connectors ship with the EPM Solution package and are shown below.
  -[Generic Sun Outage](https://catalog.dataminer.services/details/ada6ebaf-26a5-45d0-90d1-1025b1adda15)
  -[Skyline EPM Platform VSAT DSM SO](https://catalog.dataminer.services/details/67205de6-f339-43ea-9f1f-511c99d66337)

> [!TIP]
> For more general information on sun outage events, see [VSAT Sun Outages & Sun Fade Information](https://satoms.com/vsat-sun-outages/).

### Weather
DataMiner has flexibility of integration with any weather forecast service as it considers this variable a key factor capable of degrading and temporarily interrupting the signal delivery for VSAT Terminals. Operators receive automated detailed descriptions of any outages and/or degradation to the service because of weather conditions (e.g. rain fade).

Compatible connectors ship with the EPM Solution package and are shown below.
  -[Skyline Universal Weather](https://catalog.dataminer.services/details/6664b1b8-6975-4990-bb97-6df0b0239e2e)

## Automation Scripts
The DataMiner EPM VSAT Solution uses the following Automation scripts:
- **SkylineCommunications_SLC-AS-EPM_VSAT_Subscription_Manager**: Automation script in charge of updating and triggering the logic to keep...
- **EPM GEO BE Handler**: Automation script in charge of handling EPM back-end messages. It is used by the [collector](#collector-connectors) that triggers the initial *EPM Message Handler* script.
- **EPM GEO FE to BE**: Operates within the messaging system domain taking care of communication about the collector and entity the processed data originated from, between EPM front-end elements and the back-end elements. It is used by the [collector](#collector-connectors) that triggers the initial *EPM Message Handler* script.
- **EPM Message Handler**: Automation script in charge of handling EPM messages and is triggered from the collector after the ID request files for the entities are exported. It tells the EPM front end to ingest the request files.

## Visual Overview
The DataMiner EPM VSAT solution would not be complete without a visual overview that consolidates and organizes the topology and configuration into a collection of visio pages.
-[Skyline Universal Weather](https://catalog.dataminer.services/details/e7217e7f-02e6-48ce-85a3-f02298921333)
