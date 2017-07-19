# SmarTIE Manual

## Introduction

SmarTIE is the first monitoring solution that effectively combines active and passive techniques to offer a unique visibility on usage, performance and security of network infrastructures and applications.

This platform implements an intermediate approach between DPI-based and flow-based traffic inspections, providing a highly-interactive web interface with information-dense real-time charts, maps and data, all based upon a high-performance classification core.

SmarTIE relies on 3 main components:

*   **SmarTIE controller**: A logically centralized Management and Control System coordinates all the probes to perform the measurements on the network and collects flow-level reports produced by the agents and other network devices. This module performs analytics on such results, in order to derive customizable views with various graphical representations (pie charts, stacked area charts, line charts, horizontal bar charts). The controller is also able to perform anomaly detection, immediately notifying the user if something unexpected happens. All the observed traffic is maintained at different granularities for a configurable period of time (up to years) in order to offer interactive historical views and generate reports, which can be exported in different formats.
*   **SmarTIE probes**: Lightweight elements that classify the network traffic captured at strategical observation points and send periodical reports to the controller.
*   **Netflow/IPfix probes**: Standard network devices configured to send periodical traffic records in Netflow/IPfix format to the controller.

SmarTIE is based upon mature open-source projects, bleeding-edge research outcomes and patented technology, and built on a stable and malware-resistant UNIX platform.

## Login

Once the controller is activated, to access the Web Dashboard, users simply need to enter their username and password at the private URL of their SmarTIE controller.

![login](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/login.png?style=centerme)

Fields available:

*   an input box to insert the username
*   an input box to insert the password
*   the "Recovery" button allows a user to recover the authentication credentials
*   the "Login" button starts the authentication process

If the username or the password are wrong, one of the following messages is shown.

![login-error](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/login-error.png?style=centerme)

If the credentials are correct the user is redirected to the [dashboard](#dashboard) page.

## Passive Side
### Home
After logging in, the user arrives at the Home tab, which contains a map and a number of boxes that are designed to give a quick overview on the controller status.

The map is the most prominent object in the home tab and it shows where the probes, connected to the controller, are geographically located. It is possible to zoom in and out on the map using the "+" and "-" buttons placed in the top-left corner of the tab. The blue points on the map represent the probes belonging to the platform and the number in the icon shows the amount of probes placed in that location. When zooming out on the map two or more nearby probes are collapsed in one point.

![home](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/home.png?style=centerme)

The top-right box shows to the user few indicators regarding the status, in the last 5 minutes, of all the probes associated to the controller and an historical view of the active monitoring performed on the network by the platform.

Last 5 minutes

*   **Online probes**: number of probes, connected to the controller, that have been active in the last 5 minutes
*   **Measuring probes**: number of probes that have performed at least a measurement in the last 5 minutes
*   **Measurements**: amount of measurements performed in the last 5 minutes

Summary

*   **Overall period**: platform utilization interval
*   **Active probes**: number of probes performing active measurements connected to the controller
*   **Campaigns**: total number of campaigns created on the platform
*   **Experiments**: total number of experiments created on the platform
*   **Measurements**: amount of measurements performed since activation

#### **Details view**

Clicking on a probes cluster on the map opens a details view on the bottom of the tab. The details table lists all the probes placed around that location giving a general overview on their status.

![home-probes-details-view](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/home-probes-details-view.png?style=centerme)

The globe icon, placed on the top-left corner of the details view, gives an hint on the shown list. If the icon is green, the view only shows the probes available in a specific location. When the user clicks on the icon, it turns grey and the table shows all the probes associated to the controller.

Clicking on a row in the details view opens a side panel showing information regarding the active and passive sides of a probe. The passive tab shows the data collected by the probe in a time based format aggregated by application (for more info on the section, please refer to [time based](#time-based)) and clicking on the eye icon opens the full time based view for the probe. The active tab displays information regarding the active measurements campaign started on the probe and clicking on its eye icon the user is brought to a new window with a full view on the active measurements campaign started on the probe.

![home-passive-view](images/passive/home-passive-view.png?style=centerme)

![home-active-view](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/home-active-view.png?style=centerme)

Using the input boxes on the top bar of the details table, the user can filter the probes by every field available:

*   **Name**: Name of the probe
*   **Serial number**: Unique identifier for each probe
*   **Group**: Name of the group associated to the probe
*   **Private IP address**: Private IP address assigned to the probe in the network that it is monitoring
*   **Public IP address**: Public IP address used by the probe to communicate with the controller
*   **Last activity**: Last time the controller received a log from the selected probe
*   **Active status**: Status of the active side of the probe. Clicking on the eye icon opens the active tab of the side panel
*   **Passive status**: Status of the passive side of the probe. Clicking on the eye icon opens the passive tab of the side panel

### Common features
Features common to several sections of the user interface are described in the following.

#### **Pause and change interval**

All the graphs reported on the SmarTIE user interface refer to a well-defined time interval. The time interval is reported into an orange box.

![interval](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/general-interval.png?style=centerme)

By default, all graphs show live data about the last two hours. When new data is received, all the graphs are immediately updated and the reference interval advances in time accordingly. In order to focus on a specific time interval, it is necessary to interrupt live reporting (i.e., by clicking on the pause button). When in pause mode, it is also possible to change the interval to have access to the historical data.

By clicking on the pause button, a different interval can be chosen as shown in the next figure.

![interval-change](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/general-change-interval.png?style=centerme)

![interval-selector](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/general-interval-selector.png?style=centerme)

Clicking on the play button brings the interval back to the last two hours and re-enables live reporting.

#### **Probe selection**

Some sections allow to look at data collected by one probe or an aggregate in turn. The choice is done using the selector shown in the following example.

![probes-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/probes-list.png?style=centerme)

The selector lists the probes divided in three groups depending on their type:

*   **Aggregate (A):** a virtual probe aggregating data collected by different probes all belonging to the same group. The list contains an aggregate for each defined group. The "Aggregate" virtual probe includes data from ALL the probes.
*   **SmarTIE (S):** a physical or virtual SmarTIE probe.
*   **Netflow/IPfix (N):** a Netflow/IPfix enabled network device.

Moreover, each probe in the selector also reports its status:

*   **Active (green):** the probe is up and running and periodically reports collected data to the controller
*   **Warning (yellow):** the probe hasn't reported collected data at the expected time for less than 5 minutes
*   **Critical (red):** the probe hasn't reported collected data at the expected time for more than 5 minutes
*   **Disabled (grey):** the probe was explicitly disabled, thus no new data is collected from it

#### **Aggregation criterion selection**

The SmarTIE user interface reports depend on the aggregation criteria applied to the collected raw data. Some user interface sections allow to look at the aggregated data using only one criterion per time. The choice can be done using the selector shown in the following example.

![add-monitor-details](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/aggregation-criteria-list.png?style=centerme)

The available aggregation criteria are listed below:

*   **Application:** aggregates traffic flows depending on source applications
*   **Category:**  aggregates traffic flows depending on the category of source applications
*   **Source/Destination IP:** aggregates traffic flows depending on source/destination IP addresses
*   **Source/Destination AS:** aggregates traffic flows depending on source/destination Autonomous Systems
*   **Source/Destination Company:** aggregates traffic flows depending on source/destination Companies
*   **Source/Destination Country:** aggregates traffic flows depending on source/destination Countries
*   **Source/Destination City:** aggregates traffic flows depending on source/destination City

#### **Ordering and local filtering**

Clicking on the cog icon (see the next example image), a window pops up and allows to choose a subset of data sources to show in the charts for the selected aggregation criterion:

*   **Top 10** data sources based on traffic volume
*   **Bottom 10** data sources based on traffic volume
*   **Custom subset** (of up to 10 items) of data sources (e.g., a user can be interested in looking at HTTP and HTTPS traffic only)

![view-selection-options](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/selection-top-n.png?style=centerme)

![view-selection-options](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/filters-options.png?style=centerme)

#### **Global filtering**

Clicking on any label on the charts, showing the data sources for an aggregation criterion, a global filter will be applied to all the reports to include only data from the selected source. For instance, the user can aggregate data by application, filter by a specific application (e.g., clicking SKYPE on the legend) and then change the aggregation criterion to _source cities_ to see from which cities that application traffic is mostly generated. The list of enabled filters is displayed on the top bar, as shown in the image.

![view-filters-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/applied-filters.png?style=centerme)

All the reports are subject to filters, in the sense that only data matching all the filters is taken into account for generating them.

### Dashboard
The dashboard panel allows a user to view a customizable list of charts, saved on a per-user basis. It is always accessible by clicking on the corresponding icon of the navigation bar.

![dashboard](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/dashboard-icon.png?style=centerme)

When a user logs in for the first time, the dashboard is empty and a new chart, also called performance monitor, can be added by clicking on the _"add a new performance monitor button"_.

![add-monitor](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/dashboard-add-monitor.png?style=centerme)

Clicking on the add button opens an overlay window, which allows to configure a new monitor using the options listed below:

*   **Metric:** the metric of interest to observe (e.g., Throughput Out)
*   **Probe:** the probe from which the network traffic of interest is observed
*   **Aggregation criterion:** the criterion to use to aggregate traffic flows (e.g., by Application, by Source IP, by Destination Country)
*   **Graph Type:** the type of chart to use for the report (e.g., a pie chart)

![add-monitor-details](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/add-performance-monitor.png?style=centerme)

Clicking on the cancel button aborts the operation, thus no chart is added to the dashboard. Clicking on the add button appends a new performance monitor to the dashboard.

![monitor-example](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/performance-monitor.png?style=centerme)

The chart above shows the top 10 average throughputs observed from the selected probe towards specific destination IPs.

![monitor-example-hover](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/tooltip-performance-monitor.png?style=centerme)

By hovering on each item of the chart, it is possible to see the average, minimum and maximum values assumed by the selected metric in the considered time interval ( the default configuration shows data of the last two hours).

IP addresses shown in the graph are sorted by average throughput: the IP address that has the highest average throughput is displayed on the top of the chart. Then, moving clockwise, there are IP addresses with lower values, in a higher to lower order. It is possible to reverse the sorting by clicking on the sort icon. A dashboard monitor can be removed from the dashboard section by clicking on the trash icon.

![monitor-example-sort](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/sort-icon-performance-monitor.png?style=centerme)

![monitor-example-remove](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/remove-icon-performance-monitor.png?style=centerme)

### Time based

The time-based section displays graphs that show the evolution of the network traffic on the SmarTIE platform over time. It's particularly useful in showing spikes of abnormal network traffic. This view features the following types of graphs:

*   **Stacked area chart:** a graph used to represent cumulated totals over time. It shows trends over time among related attributes
*   **Line chart:** a graph used to represent average values of QoS metrics over time

This view depends on which probe and aggregation criterion have been chosen.
The time-based view shows six charts based on the selection of probes and aggregation criteria used. These charts can be classified in:

*   **Volume:** three stacked area charts that show the volume of observed network traffic, in both directions (upstream and downstream), in terms of bytes, packets and flows per aggregation criterion value (e.g. applications) during the considered interval.
*   **Round Trip Time:** a line chart that shows the average round trip time per aggregation criterion value over time during the considered interval.
*   **Throughput:** two line charts that show the average upstream and downstream throughput over time per aggregation criterion value during the considered interval.

As shown in the following images, data resolution is reported on the top bar of each graph. The resolution directly depends on the chosen time interval and it becomes higher as the time interval becomes wider. In the images below it is available an example of a stacked area chart (Traffic Volume) and a line chart (Round Trip Time).

![stacked-area-example](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/stacked-area.png?style=centerme)

![line-chart-example](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/line-chart.png?style=centerme)

A click on the pause button enables the focus feature, which allows to zoom in on a particular subinterval of the considered interval. The zoom is applied to all the charts shown in the view.

![focus-example](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/zoom-chart.png?style=centerme)

![focus-example-zoom](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/zoom-chart-window.png?style=centerme)

![stacked-area-example-zoom](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/stacked-area-zoomed.png?style=centerme)

### Top N
Similarly to the Time based charts, this section presents the the main metrics (i.e. traffic volume, round-trip time) using horizontal bars. The value for each bar is the aggregation for a single metric in the considered interval. This representation is useful to quickly identify the most used data sources per aggregation criterion (e.g. IP address, application) on the network. The number of data sources displayed per aggregation criterion can be set in the [settings](#settings) section.

The view strictly depends on which probe and aggregation criterion have been chosen, showing six charts classified in:

*   **Volume:** three horizontal bar charts that show the volume of observed network traffic, in both directions (upstream and downstream), in terms of bytes, packets and flows, per data source based on the aggregation criterion (e.g. application), during the considered interval.
*   **Round-Trip Time:** a horizontal bar chart that shows the average round-trip over time, per data source based on the aggregation criterion, during the considered interval.
*   **Throughput:** two horizontal bar charts that show the upstream and downstream throughput over time, per data source based on the aggregation criterion, during the considered interval.

![view-selection-options](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/horizontal-bar.png?style=centerme)

### Anomalies
#### **What is anomaly detection**

The objective of anomaly detection is to reactively detect any anomalous traffic on the monitored network. SmarTIE anomaly detector  analyzes the volume of network traffic in terms of bytes, packets and flows. In order to work properly, it requires at least two days of observed network traffic: if not enough data has been collected, a warning message is displayed. The anomaly detector takes into account at most the traffic observed during the last two weeks, performing a new detection every time new data is received from a SmarTIE probe.

#### **Notification**

When a new anomaly is detected, if the user is displaying a section other than "_Anomalies_", he receives a notification in the form of a popup message, containing a link to the anomaly section. The number of unattended anomalies is reported in red on the anomaly topbar menu icon.

![anomaly-details](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-warning.png?style=centerme)

![anomaly-details](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-new-anomalies-number.png?style=centerme)

#### **Anomalies view**

The anomaly section includes a timeseries graph and a table. The graph shows the traffic volume in terms of bytes for each probe. The chart also includes the aggregate volume represented by the mean value observed across all the probes. By clicking on a probe name in the legend, it is possible to highlight the respective line in the plot.

When an anomaly is detected, a warning icon is reported in correspondence of the timestamp over the plot. If the anomaly has not been already analyzed, the icon appears in yellow, otherwise it appears in gray-scale.

![anomaly-graph](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-graph-anom-new.png?style=centerme)

More details about the anomalies are available in the table below the graph. Each row refers to a single anomaly event, containing:

*   **ID**: an unique identifier for the anomaly
*   **Type**: type of anomaly detected
*   **Detection time**: when the anomaly was detected
*   **Duration**: duration of the anomaly (in seconds)
*   **Details**: details about the anomaly, including the related SmarTIE probe, the metric (bytes/packets/flows) and the anomalous value detected.

![anomaly-table](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-table.png?style=centerme)

Each row also includes two buttons. The eye button opens a view reporting fine grained details about all the flows detected by the probe during the anomaly. An example of such view is reported below.

![anomaly-details](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-details.png?style=centerme)

The other button allows the user to archive the anomaly and classify it as true or false. Once the anomaly has been archived, the warning icon becomes gray.

![anomaly-archive](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-archive-anomaly.png?style=centerme)

![anomaly-table-archived](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/anomalies-table-analyzed.png?style=centerme)

### Report
The report section is opened by clicking on the _report_ button on the topbar menu. This section allows the user to get a concise report about the platform status and a specific probe for a customizable time interval. It may be particularly useful to investigate the network traffic classified during an attack performed by a malicious host.

It is possible to choose a start and an end date for the report.

![interval](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/report-interval.png?style=centerme)

The report can be customized choosing the quadruplet:

*   **Metric:** the metric the user is interested to report (e.g. _Throughput Out)_
*   **Probe:** the source probe of the network traffic to include in the report
*   **Aggregation criterion:** the classification category the user is interested to view (e.g. _Applications_ or _IP Source_)
*   **Sorting**: the sorting criterion to use in the report (_top first_ or _bottom first_)

![content](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/report-content.png?style=centerme)

More than one quadruplet can be added to a report. A summary of the items to report is shown on the _report preview_ subsection.

![preview](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/report-preview.png?style=centerme)

Clicking on the _Generate > Report_ button creates the report; moreover, the chosen quadruplets is saved and it will preselected the next time the report section is opened.

For each item the report shows:

*   a table reporting the minimum/maximum/average value per data source;
*   a pie graph, that is useful to compare the average values for each data source;
*   a time-based graph, that allows the user to see the usage of the network during the whole interval for each data source.

![example](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/report-example.png?style=centerme)

Clicking on the printer icon on the topbar is possible to print the report or export it as PDF.

### Settings
The _settings_ section allows the administrator to customize the configuration of the SmarTIE platform. It is divided into the following subsections:

#### **Controller Settings**

This subsection allows the admin to set up options that affect only the controller.

*   **IP address**: sets the IP address of the web interface of the controller
*   **Netmask**: sets the netmask (CIDR notation) associated to the IP address of the web interface of the controller
*   **Gateway**: sets the IP address of the default gateway of the controller

![controller](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/controller-settings.png?style=centerme)

#### **Platform Settings**

The options modified in this subsection affect the controller and the probes alike.

*   **Max number of displayed elements**: max number of elements considered in report lists and graphs, e.g. a value of _10_ causes the _top-n_ graph to show the results of the top-10 ranking elements (aggregated according to the filtering and drill-down criteria)
*   **Remote assistance**: this toggle button allows the administrator to enable/disable the remote assistance module
*   **Anomaly notification**: this toggle is used to enable/disable the notification by email when an anomaly is detected
*   **Go to active dashboard**: link to the active measurements dashboard

![platform](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/platform-settings.png?style=centerme)

If anything changes, on the top bar are displayed:

*   the number of modified elements
*   two buttons that allow the administrator to save the changes or restore the controller to the previous state

![modified](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/modified-settings-fields.png?style=centerme)

If the _Apply_ button is clicked, the changes are saved and a notification informs the admin on whether the operation was successful or an issue occurred.

![error-probe](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/error-message-settings.png?style=centerme)

![success-probe](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/settings-success-probe.png?style=centerme)

![success-platform](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/settings-success-platform.png?style=centerme)

#### **Manage Groups**

This subsection allows the administrator to create new groups or delete existing ones. Furthermore, it gives the ability to add or remove probes from groups.

![manage-groups](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/manage-groups.png?style=centerme)

When adding a new group, the information required to complete the registration is shown in the following image.

![manage-groups](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/add-new-customer.png?style=centerme)

#### **Probes List**

This table lists all the probes linked to the controller giving a general overview on their status. A probe can be associated to one or multiple groups, there is a row for every group it belongs to. For each probe the following fields are available:

*   **Serial number**: unique identifier for each probe
*   **Group**: name of the group associated to the probe
*   **Private IP address**: private IP address assigned to the probe in the network that it is monitoring
*   **Public IP address**: probe public address used to communicate with the controller
*   **Last activity**: last time the controller received a log from the selected probe
*   **Active status**: status of the active side of the probe
*   **Passive status**: status of the passive side of the probe
*   **Registration status**: toggle button used to enable/disable network passive monitoring on the probe

![probes-list-settings](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/passive/probes-list-settings.png?style=centerme)

## Active Side

### Home
The Home tab is the first page shown to the users when they reach the active dashboard of the platform. It contains a summary of the measurements in progress on the platform.

*   **Interval**: time interval considered for the statistics (e.g., last day, last month, etc.)
*   **Active agents**: number of active agents in the considered interval
*   **Access networks**: number of monitored access networks in the specific interval
*   **Measurements**: measurements performed during the interval

![enter image description here](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/active-home.png?style=centerme)

### Agents
An agent is a software tool running on a probe, it is in charge of all the active measurements performed on an access network.  The measurements to perform are defined in a list of experiments that the probe periodically requests to the controller.
According to the SmarTIE paradigm, every probe can only have one agent running and an agent can only monitor one access network per time. A probe and, consequently, an agent may also be moved to a different location to monitor a distinct access network.

![agents-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/agents.png?style=centerme)

The agents panel lists all the agents connected to the controller reporting the following info:

*   **Probe S/N**: serial number of the probe hosting the agent
*   **Version**: agent's software version number
*   **Registration time**: the date in time when the agent was connected to the controller for the first time
*   **Measurements**: number of measurements performed by the agent in its lifetime
*   **Failures**: total number of failed measurements
*   **Last measurement**: date of the last measurement executed by the agent
*   **Last activity**: agent's last activity date
*   **Agent status**: the controller reports the status of each agent:

	*  **Active (green)**: the agent is up and running and periodically reports to the controller
    *   **Warning (yellow)**: the agent hasn't reported at the expected time for less than 5 minutes
    *   **Critical (red)**: the agent hasn't reported at the expected time for more than 5 minutes
*   **Actions**: there are three actions available for each agent:

	* **Delete**: clicking on the icon disconnects the agent from the controller. When disconnected, the agent performs the rest of experiments on its list and enters an idle mode. It won't be available until the next reboot of the probe
    *   **User**: a click on the button shows all the info about the customer who owns the agent
    *   **Network**: it brings the user to a detailed view of the access network monitored by the agent

### Customers
A customer is the owner of a probe, every customer is allowed to own one or more probes. A probe can be used to monitor only one access network per time, but it may be moved from one location to another, during its lifetime, to monitor a different network.

![customers-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/customers.png?style=centerme)

Under the customers tab, the administrator is able to see the list of all the users registered on the platform and some useful information regarding each account:

*   **Id**: unique identification number given to every customer
*   **E-mail**: customer's email address
*   **Registration time**: customer registration date
*   **Access Networks**: number of monitored access networks, a click brings the administrator to a detailed view of the networks
*   **Agents**: number of agents owned by the customer, clicking on the icon shows the full list
*   **Last measurement**: date of the last measurement executed by any of the customer's agents
*   **Actions**: clicking on the icon deletes the account

### Plans
The plans page lists all the plans defined by the administrator. From this tab is possible to create, edit and delete a plan. Every plan can be associated to one or more access networks.

![plans-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/plans.png?style=centerme)

The dashboard shows the information shown in the image above for each plan:

*   **Plan Id**: unique identification number given to every plan
*   **ISP name**: internet service provider name
*   **Plan name**: commercial name of the plan
*   **Technology**: network technology type
*   **Nominal Download **: network's full-rated download speed in Mbps
*   **Nominal Upload **: network's full-rated upload speed in Mbps
*   **Access Networks**: number of access networks that have been associated to this plan
*   **Actions**: there are two actions available for each plan:

	*   **Delete**: clicking on the icon deletes the plan
    *   **Edit**: a click on the icon opens a new window where it is possible to acquire a temporary exclusive [lock](#locks) to edit the plan

Clicking on the link on the bottom-left of the page allows the administrator to create a new plan.

![create-plan](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/create-plan.png?style=centerme)

### Access networks
An access network is a type of telecommunications network which connects subscribers to their immediate service provider. The access networks tab lists all the networks of this type that are or were monitored using SmarTIE. The networks are automatically detected by the agents and they are uniquely identified with the MAC and IP address of the gateway interface visible to the agent.

![access-networks-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/access-networks.png?style=centerme)

From this view, the user has access to the following parameters:

*   **ID**: unique identification number given to the plan
*   **Plan**: commercial name of the plan in use on the access network
*   **Throughput DL**: average download throughput (in kbps) measured across all the experiments on the network
*   **Throughput UL**: average upload throughput (in kbps) measured across all the experiments on the network
*   **Delay**: average delay (in ms) of the access network across all the experiments
*   **Jitter**: average jitter (in ms) of the access network across all the experiments
*   **Packet loss**: average packet loss (pps) measured across all the experiments on the network
*   **Measurements**: number of measurements performed on this network across all the agents
*   **Failures**: total number of failed measurements on this network
*   **Last measurement**: date of the last measurement executed on the network
*   **Location**: information about the geographical position of the network
*   **Actions**: there are three actions available for each network:

    *  **Delete**: clicking on the icon deletes the network
    *   **Edit**: a click on the icon opens a new window where it is possible to edit the network
    *   **Agents**: clicking on the icon shows the full list of agents monitoring the network

![edit-access-network](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/edit-access-network.png?style=centerme)

### Results
Once an experiment has been successfully run, its results are avaible in the results page. In this page, the user has access to the results of all the experiments performed on the platform. The list of results can be filtered by multiple otions:

*   **Probe**: results of the experiments run by a specific probe
*   **Location**: it filters the results based on the location of the monitored network
*   **Campaign**: it only shows the results of the experiments associated to the selected campaign
*   **Experiment**: it lists the results belonging to the specific experiment type
*   **Metric**: it shows the results of the experiments giving in output the selected metric

![results-filters](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/results-filters.png?style=centerme)

Every row shows the following info:

*   **Timestamp**: the date in time when the experiment was performed
*   **Inputs**: list of input parameters used for the experiment
*   **Agent IP**: public ip address of the agent performing the experiment
*   **Server IP**: ip adddress of the cooperative counterpart used for the experiment. It can be the address of a measure server or a publicly accessible server suitable for the aim
*   **Experiment**: name of the experiment
*   **Output name**: list of outputs produced by the experiment
*   **Stats**: most common statistics on the produced output

![results-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/results.png?style=centerme)

### Metrics
There are many different ways to measure the performance of a network and several metrics are often considered important, like bandwidth, throughput, latency, etc. This section lists all the metrics defined on the platform which can be used for an experiment. From this tab the user is allowed to create, edit and delete a metric.

![metrics-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/metrics.png?style=centerme)

For each metric, the platform reports:

*   **ID**: unique identification number given to the metric
*   **Metric Name**: name of the metric
*   **Unit**: unit of measurement to be used for the metric
*   **Description**: general description of the metric
*   **Actions**: there are two actions available for every metric:

	*  **Delete**: clicking on the icon deletes the plan
    *   **Edit**: a click on the icon opens a new window where it is possible to acquire a temporary exclusive [lock](#locks) to edit the metric

![edit-metric](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/edit-metric.png?style=centerme)

Clicking on the link on the bottom-left of the page opens a separate view to add a new metric.
When a metric is deleted, all the experiments that depend on it stop working.

### Measure servers
For certain experiments a cooperative counterpart is needed to perform a measurement, in these circumstances an agent uses a measure server. A user can add, edit or delete a measure server from the "Measure Servers" page.

![measure-servers-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/measure-servers.png?style=centerme)

For each server the following parameters are available:

*   **ID**: unique identification number given to the server
*   **Server IP**: server public IP address
*   **Http Port**: port number used by the controller to communicate with the server and check its status
*   **Last Active**: server's last activity date
*   **Status**: the controller reports the status of each server:

    * **Active (green)**: the server is up and running and periodically reports to the controller
    *   **Warning (yellow)**: the server hasn't reported at the expected time for less than 5 minutes
    *   **Critical (red)**: the server hasn't reported at the expected time for more than 5 minutes
*   **Bandwidth**: the user can set the bandwidth (in Mbps) available on the server to be used for the measurements. The controller schedules the experiments on the agents and assigns the measure server to use accordingly with the available resources
*   **Actions**: there are two actions available for every server:

    * **Delete**: clicking on the icon deletes the measure server
    *   **Edit**: a click on the icon opens a new window where it is possible to edit the server settings

### Experiments
To actively measure the performance of an access network, a user can define a list of experiments that will be part of a monitoring campaign. The experiments tab lists the experiments created on the platform:

![experiment](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/experiments.png?style=centerme)

*   **ID**: unique identification number given to the experiment
*   **Experiment Name**: name of the experiment
*   **Description**: short description of the experiment
*   **Actions**: there are four actions available on an existing experiment:

    * **Delete**: clicking on the icon deletes the experiment, removes it from every campaign and cancels all its schedules
    *   **Open**: a click on the icon opens a new window where it is possible to have a full view of the experiment and, if it is needed, acquire a temporary exclusive [lock](#locks) to edit it by clicking on the "Modify Experiment" link
    *   **Duplicate**: selecting this option the platform walks the user through the creation of a duplicate of the selected experiment
    *   **Schedule**: a click on the icon opens a new tab showing all the experiment's schedules across different campaigns

Using the link on the bottom-left of the page it is possible to create a new experiment from a separate view, as shown in the image below.

![create-experiment](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/create-experiment.png?style=centerme)

#### **General details**

General details that are shown in the experiments summary table mentioned above.

*   **Experiment Name**: name of the experiment
*   **Description**: short description of the experiment

#### **Experiment specification**

In addition to the general details parameters, the user has to fill in 4 other compulsory fields in the experiment specification area:

*   **Duration**: experiment duration in seconds
*   **Retry**: max number of retries in case the experiment fails
*   **Do not re-schedule before**: minimum time interval (in seconds) to wait before a new schedule of the experiment after a successful run
*   **Measurement module**: module to use for the experiment execution, picked from the ones available on the platform

#### **Inputs**

Depending on the module chosen for the experiment, a list of input parameters is available in this subsection. The user is not allowed to change the name of the parameters, he can only insert the values to be used as inputs. The input value can be a constant or, checking the tickbox "IsFunction", one of the "Function Parameter" available in the platform. Currently the platform supports two functions:

*   **GetBandwidthDw**: returns the nominal download speed of the plan in use
*   **GetBandwidthUp**: returns the nominal upload speed of the plan in use

#### **Outputs**

An experiment produces one or more outputs listed under this box. As it happens with the inputs list, the user cannot edit the name of the output parameters. It is only possible to specify the sampling rate to use to produce the result.

### Campaigns
The NM-2 suite enables any user to create a monitoring campaign on one or more access networks to evaluate the performances. A campaign executes a set of experiments on all the involved networks producing a list of objective metrics. An experiment can only be scheduled and executed on an access network if it is part of a monitoring campaign.

![campaigns-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/campaigns.png?style=centerme)

For each campaign the following parameters are available in the general view:

*   **ID**: unique identification number given to the experiment
*   **Campaign Name**: name of the campaign
*   **Description**: short description of the campaign
*   **Actions**: there are two actions available on an existing campaign:

   *   **Delete**: clicking on the icon deletes the campaign and removes the schedules of all the experiments belonging to it
    *   **Open**: a click on the icon opens a new window where it is possible to have a full view on the campaign and, if it is needed, acquire a temporary exclusive [lock](#locks) to edit it by clicking on the "Modify Campaign" link

Using the link on the bottom-left of the page it is possible to create a new campaign from a separate view, as shown below.

![create-campaign](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/create-campaign.png?style=centerme)

#### **General details**

*   **Campaign Name**: name of the campaign
*   **List timeout**: amount of time, in minutes, an agent has to wait before asking an update to the controller for the list of experiments to execute as part of the campaign. When an agent is running experiments for more than one campaign, it uses the minimum timeout value across all of them
*   **Description**: short description of the campaign

#### **Involved access networks**

In this box the user defines the criteria to select the access networks that will be monitored during the campaign:

*   **Selection criterion**: list of the available criteria to select the access networks involved in the campaign. Currently, the suite supports 3 different criteria:
	* **Agent**: the user can select an access network based on the agent that is monitoring it
	* **Location**: it selects all the access networks placed in a specific location
	* **Plan**: it selects all the access networks with the selected plan
*   **Inputs**: based on the chosen selection criterion, it lists one or more tabs to select the location, the agent or the plan to use to identify the networks
*   **Delete**: it deletes the current criterion

#### **Exported metrics**

From this area, the user can define a list of metrics to be exported at the end of the campaign using the available filters:

*   **Name**: name for the exported metric
*    **Experiment ID**: the user can decide to isolate the results reported by the runs of a single experiment within the set of selected experiments
*   **Metric ID**: metric to export in the results between those produced by the selected experiment
*   **Delete**: it deletes the current selection

#### **Experiments list**

This box lists the experiments defined on the platform and the user can tick those to use for the monitoring campaign.

### Schedules
Once the experiments and the campaings are created, a user needs to define one or more schedules for each experiment belonging to a campaign, otherwise they are never executed.

![schedules-list](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/schedules.png?style=centerme)

The schedules page lists all the schedules defined on the platform and the main information for each of them:

*   **Campaign Name**: name of the campaign
*   **Experiment Name**: name of the experiment
*   **Day of week**: day of the week selected to run the experiment. Values range is between 1 and 7, where 1 is Monday
*   **Day of month**: day of the calendar month selected to run the experiment. Values range is between 1 and 31
*   **Month of year**: month of the year selected to run the experiment. Values range is between 1 and 12, where 1 is January
*   **Start time**: start time of the allowed interval, within a day, to run an experiment. Values range is between 00:00 and 23:59
*   **Stop time**: stop time of the allowed interval, within a day, to run an experiment. Values range is between 00:00 and 23:59 and higher than the start time
*   **Repetitions**: number of repetitions defined for the experiment, 0 means infinite. To reduce the overhead introduced on an access network, if there are time overlapping schedules of the same experiment, it is just run once but the controller decrements the counters of all the schedules involved
*   **Actions**: there are three actions available on an existing schedule:
    
    *   **Delete**: clicking on the icon deletes the campaign and removes the schedules of all the experiments belonging to it
    *   **Edit**: a click on the icon opens a new window where it is possible to acquire a temporary exclusive [lock](#locks) to edit the schedule
    *   **Open**: clicking on the icon opens a new window to create a new schedule starting from the duplicate of the current one

Clicking on the link on the bottom-left of the page brings the user to a new page, where it is possible to create a new schedule.

#### **General details**

This box allows the user to select an experiment, contained in one of the campaigns, to schedule and the number of repetitions for its schedule.

#### **Time details**

From this area, the user can select a day of the week (e.g. every Monday), a day of the month (e.g. every 1st) or a full month of the year to indicate the usual interval when the scheduled activity may be run. At the same time, the user can use start and stop time to run the activity at certain intervals on the specific days.

![create-schedule](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/create-schedule.png?style=centerme)

### Locks
To prevent concurrent changes to sensitive entities in the platform, the NM-2 suite uses a lock mechanism. It helps to prevent circunstances where multiple users try to edit the same resource at the same time.

When a user opens the edit tab for a sensitive entity, a temporary lock is acquired and a countdown is shown on the top-left corner of the page. By default the lock lasts for 10 minutes, during this time the user can decide to release it and discard all the changes, extend it for other 10 minutes or release the lock and save the changes.

If a lock expires while a user is editing an entity, all the changes are saved and the user is forced to exit the page. The variations are only saved if they leave the platform in a consistent state.

![lock](https://raw.githubusercontent.com/NM2/smartie-doc/master/images/active/lock.png?style=centerme)

