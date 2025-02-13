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

![Left Panel Image](https://github.com/Vlad1390/Projects-/blob/main/Left_Panel.png?raw=true)

## Add Filter Option

Add filter option under the search bar allows us to apply a filter on the fields as shown below.

![Add GIF](https://github.com/Vlad1390/Projects-/blob/main/Add.gif?raw=true)

## Create Table
By default, the documents are shown in raw form. We can click on any document and select important fields to create a table showing only those fields. This method reduces the noise and makes it more presentable and meaningful.

![Create Table GIF](https://github.com/Vlad1390/Projects-/blob/main/Create_Table.gif?raw=true)
Don't forget to save the table format once it is created. It will then show the same fields every time a user logs into the dashboard.

## KQL Overview
 KQL (Kibana Query Language) is a search query language used to search the ingested logs/documents in the elasticsearch. Apart from the KQL language, Kibana also supports Lucene Query Language. We can disable the KQL query as shown below.

[![KQL Query](https://github.com/Vlad1390/Projects-/blob/main/KQL/Query.png?raw=true)](https://github.com/Vlad1390/Projects-/blob/main/KQL/Query.png?raw=true)

In this task, we will be exploring KQL syntax. With KQL, we can search for the logs in two different ways.

- Free text search
- Field-based search

## Free text Search

Free text search allows users to search for the logs based on the text-only. That means a simple search of the term security will return all the documents that contain this term, irrespective of the field.

Let us look at the index, which includes the VPN logs. One of the fields Source_Country has the list of countries from where the VPN connections originated, as shown below.

[![KQL Free Text](https://github.com/Vlad1390/Projects-/blob/main/KQL/Free_text.png?raw=true)](https://github.com/Vlad1390/Projects-/blob/main/KQL/Free_text.png?raw=true)

Let's search for the text United States in the search bar to return all the logs that contain this term regardless of the place or the field. This search returned 2304 hits, as shown below.

![KQL Image](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG3.png?raw=true)

What if we only search for the term United Will it return any result?

![KQL Image](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG4.png?raw=true)

It didn't return any result because KQL looks for the whole term/word in the documents.

## WILD CARD

KQL allows the wild card * to match parts of the term/word. Let's find out how to use this wild card in the search query.

Search Query: United*

![KQL Image](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG5.png?raw=true)

We have used the wildcard with the term United to return all the results containing the term United and any other term. If we had logs with the term United NationsIt would also have returned those as a result of this wildcard.

## Logical Operators (AND | OR | NOT)

KQL also allows users to utilize the logical operators in the search query. Let us see the examples below.

### 1- OR Operator

We will use the OR operator to show logs that contain either the United States or England.

Search Query: "United States"    OR     "England"

![KQL Image](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG6.png?raw=true)


### 2- AND Operator

Here, we will use AND Operator to create a search that will return the logs that contain the terms "UNITED STATES" AND "Virginia."

Search Query: "United States" AND "Virginia"

![KQL Image](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG7.png?raw=true)

### 3- NOT Operator

Similarly, we can use NOT Operator to remove the particular term from the search results. This search query will show the logs from the United States, including all states but ignoring Florida.

Search Query: "United States" AND NOT ("Florida")


![KQL Image](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG8.png?raw=true)

## Field-based search

In the Field-based search, we will provide the field name and the value we are looking for in the logs. This search has a special syntax as FIELD : VALUE. It uses a colon : as a separator between the field and the value. Let's look at a few examples.

Search Query: Source_ip : 238.163.231.224    AND     UserName : Suleman

Explanation: We are telling Kibana to display all the documents in which the field Source_ip contains the value 19.112.190.54 and UserName as Suleman as shown below.

![KQL GIF](https://github.com/Vlad1390/Projects-/blob/main/KQL/IMG9.gif?raw=true)

As we click on the search bar, we will be presented with all the available fields that we can use in our search query. To explore the other options of KQL, look at this official reference https://www.elastic.co/guide/en/kibana/7.17/kuery-query.html

The visualization tab allows us to visualize the data in different forms like Table, Pie charts, Bar charts, etc. This visualization task will use multiple options this tab provides to create some simple presentable visualizations.

## Create Visualization

There are a few ways to navigate to the visualization tab. One way is to click on any field in the discover tab and click on the visualization as shown below.

