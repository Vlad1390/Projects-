# Investigating with ELK

## Overview
This project demonstrates how to use the ELK (Elasticsearch, Logstash, and Kibana) stack for cybersecurity investigations. The goal is to collect, analyze, and visualize security-related logs to identify potential threats.

## Scenario
A US-based company  CyberT has been monitoring the VPN logs of the employees, and the SOC team detected some anomalies in the VPN activities. Our task as SOC Analysts is to examine the VPN logs for January 2022 and identify the anomalies. Some of the key points to note before the investigation are:

All VPN logs are being ingested into the index # vpn_connections.
The index contains the VPN logs for January 2022.
A user # Johny Brown was terminated on 1st January 2022.
We observed failed connection attempts against some users that need to be investigated.

![Investigating with ELK](https://github.com/Vlad1390/Projects-/blob/main/93bf216574fb435bef51b890a741e4cb.png?raw=true)

## ElasticStack Overview

Elastic stack is the collection of different open source components linked together to help users take the data from any source and in any format and perform a search, analyze and visualize the data in real-time.

![Elastic Stack Image](https://raw.githubusercontent.com/Vlad1390/Projects-/fadd80e67c14592ec90bd7018e1dc46d82d45ef5/elastic%20stack.png)

﻿Let's explore each component briefly and see how they work together.

## Elasticsearch

Elasticsearch is a full-text search and analytics engine used to store JSON-formated documents. Elasticsearch is an important component used to store, analyze, perform correlation on the data, etc. Elasticsearch supports RESTFul API to interact with the data.

## Logstash

Logstash is a data processing engine used to take the data from different sources, apply the filter on it or normalize it, and then send it to the destination which could be Kibana or a listening port. A logstash configuration file is divided into three parts, as shown below.

The input part is where the user defines the source from which the data is being ingested. Logstash supports many input plugins as shown in the reference https://www.elastic.co/guide/en/logstash/8.1/input-plugins.html

The filter part is where the user specifies the filter options to normalize the log ingested above. Logstash supports many filter plugins as shown in the reference documentation https://www.elastic.co/guide/en/logstash/8.1/filter-plugins.html

The Output part is where the user wants the filtered data to send. It can be a listening port, Kibana Interface, elasticsearch database, a file, etc. Logstash supports many Output plugins as shown in the reference documentation https://www.elastic.co/guide/en/logstash/8.1/output-plugins.html

## Beats

Beats is a host-based agent known as Data-shippers that is used to ship/transfer data from the endpoints to elasticsearch. Each beat is a single-purpose agent that sends specific data to the elasticsearch. All available beats are shown below.


![The Beats Family](https://github.com/Vlad1390/Projects-/blob/main/The%20Beats%20Family.png?raw=true)



## Kibana

Kibana is a web-based data visualization that works with elasticsearch to analyze, investigate and visualize the data stream in real-time. It allows the users to create multiple visualizations and dashboards for better visibility.
## How they work together:

![Kibana Image](https://github.com/Vlad1390/Projects-/blob/main/Kibana.png?raw=true)

- Beats is a set of different data shipping agents used to collect data from multiple agents. Like Winlogbeat is used to collect windows event logs, Packetbeat collects network traffic flows.
- Logstash collects data from beats, ports or files, etc., parses/normalizes it into field value pairs, and stores them into elasticsearch.
- Elasticsearch acts as a database used to search and analyze the data.
- Kibana is responsible for displaying and visualizing the data stored in elasticsearch. The data stored in elasticseach can easily be shaped into different 
  visualizations, time charts, infographics, etc., using Kibana.

  As we already covered a brief intro of Kibana. In this Lab, we will explore different Kibana features while investigating the VPN logs. Kibana is an integral component of Elastic stack that is used to display, visualize and search logs. Some of the important tabs we will cover here are:

- Discover tab
- Visualization
- Dashboard

  ![Dashboard Image](https://github.com/Vlad1390/Projects-/blob/main/Dashboard.png?raw=true)

 ## Discover Tab

Discover tab within the Kibana interface contains the logs being ingested manually or in real-time, the time-chart, normalized fields, etc. Analysts use this tab mostly to search/investigate the logs using the search bar and filter options.

![Discover Tab Image](https://github.com/Vlad1390/Projects-/blob/main/New%20folder/Discover_tab.png?raw=true)

Some key information available in a dashboard interface are

- Logs (document): Each log here is also known as a single document containing information about the event. It shows the fields and values found in that document.
- Fields pane: Left panel of the interface shows the list of the fields parsed from the logs. We can click on any field to add the field to the filter or remove it from the search.
- Index Pattern: Let the user select the index pattern from the available list.
- Search bar: A place where the user adds search queries / applies filters to narrow down the results.
- Time Filter: We can narrow down results based on the time duration. This tab has many options to select from to filter/limit the logs.
- Time Interval: This chart shows the event counts over time.
- TOP Bar: This bar contains various options to save the search, open the saved searches, share or save the search, etc.
Each important element found in the Discover tab is briefly explained below:

## Time Filter

The time filter allows us to apply a log filter based on the time. It has many options to choose from.

![Time Filter Image](https://github.com/Vlad1390/Projects-/blob/main/New%20folder/Time_Filter.png?raw=true)

## Quick Select
The Quick Select tab is another useful tab within the Kibana interface that provides multiple options to select from. The Refresh, Every option at the end will allow us to choose the time to refresh the logs continuously. If 5 seconds is set, the logs will refresh every 5 seconds automatically.

![Quick Select Image](https://github.com/Vlad1390/Projects-/blob/main/New%20folder/Quick_select.png?raw=true)

## Timeline

The timeline pane provides an overview of the number of events that occurred for the time/date, as shown below. We can select the bar only to show the logs in that specified period. The count at the top left displays the number of documents/events it found in the selected time.

![Timeline Image](https://github.com/Vlad1390/Projects-/blob/main/New%20folder/Timeline.png?raw=true)

This bar is also helpful in identifying the spike in the logs. We got an unusual spike on 11th January 2022, which is worth investigating.

## Index Pattern

Kibana, by default, requires an index pattern to access the data stored/being ingested in the elasticsearch. Index pattern tells Kibana which elasticsearch data we want to explore. Each Index pattern corresponds to certain defined properties of the fields. A single index pattern can point to multiple indices.

Each log source has a different log structure; therefore, when logs are ingested in the elasticsearch, they are first normalized into corresponding fields and values by creating a dedicated index pattern for the data source.

In the attached lab, we will be exploring the index pattern with the name vpn_connections that contains the VPN logs.

![Index Image](https://github.com/Vlad1390/Projects-/blob/main/Index.png?raw=true)

## Left Panel - Fields

The left panel of the Kibana interface shows the list of the normalized fields it finds in the available documents/logs. Click on any field, and it will show the top 5 values and the percentage of the occurrence.

We can use these values to apply filters to them. Clicking on the + button will add a filter to show the logs containing this value, and the - button will apply the filter on this value to show the results that do not have this value.



