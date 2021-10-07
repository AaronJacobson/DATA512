# DATA512
## Reproducing Analysis Steps
1. Modify relevant constant variables in the notebook cell with all the string variables so the files get output in the right place on your machine.
2. Run all cells in order from top to bottom. 

## Attributions and Provenance
I used Stack Overflow, API docs, course provided code and various google results to figure out the correct syntax for various method calls.

## Data Descriptions
### Pagecount/Legacy API data
This data comes from here: https://wikimedia.org/api/rest_v1/#!/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end

This data is saved in these files by default:
- legacy_desktop-site_2007123100-2016070100.json
- legacy_mobile-site_2007123100-2016070100.json

#### Data Attributes:

| Attribute | Description|
|-----------|------------|
| Project | The Wikipedia project that the data monitors. In this code we only look at the "en.wikipedia" project|
| Access-Site| The method of access, in this case either "desktop-site" for desktop views or "mobile-site" for mobile views|
| Granularity | The amount of time each data point represents. In this code we only look at monthly data. |
| Timestamp | The beginning of the time period the data point represents, for example 2007120100 represents 1 am on December 1st, 2007. |
| Count | The number of page views in the time period for the project. |

It documents the number of desktop and mobile page views for all of Wikipedia from December 2007 through July 2016.
### Pageview/Modern API data
This data comes from here: https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end

This data is saved in these files by default:
- pageviews_desktop_2015070100-2021091000.json
- pageviews_mobile-app_2015070100-2021091000.json
- pageviews_mobile-web_2015070100-2021091000.json

| Attribute | Description|
|-----------|------------|
| Project | The Wikipedia project that the data monitors. In this code we only look at the "en.wikipedia" project|
| Access | The method of access, in this case either "desktop" for desktop views, "mobile-web" for mobile web views or "mobile-app" for mobile app views.|
| Agent | The kind of view. In this code we only look at the "user" agent views. |
| Granularity | The amount of time each data point represents. In this code we only look at monthly data. |
| Timestamp | The beginning of the time period the data point represents, for example 2007120100 represents 1 am on December 1st, 2007. |
| Views | The number of page views in the time period for the project. |
It documents the number of desktop, mobile-web, and mobile-app pages views for all of Wikipedia from July 2015 to the present day.

### Processed Data

This intermediate processed data is used to organize the data before displaying it for analysis. This data exists in this file by default: en-wikipedia_traffic_200712-202108.csv

| Attribute | Description |
|-----------|-------------|
| Year | The year the data point is in. |
| Month | the month the data point is in. |
| pagecount_all_views | The total views observed through the legacy pagecount API. |
| pagecount_desktop_views | The number of views observed through the legacy pagecount API from desktop users. |
| pagecount_mobile_views | The number of views observed through the legacy pagecount API from mobile users. |
| pageview_all_views | The total views observed through the modern pageview API. |
| pageview_desktop_views | The number of views observed through the modern pageview API from desktop users. |
| pageview_mobile_views | The number of views observed through the modern pageview API from mobile users. |

### General Data Process
The code follows this general flow:
1. Pull the data from the Wikipedia APIs and save the data in raw JSON form.
2. Load the data from the JSON files, process it, and output the processed data to a CSV file.
3. Load the data from the CSV file, display it on a single graph, and save the graph as a PNG image.