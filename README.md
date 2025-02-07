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



