# Getting Started with Grafana

## What is Grafana?

- Grafana is an open source visualization and analytics software. It allows you to query, visualize, alert on, and explore your metrics no matter where they are stored. In plain English, it provides you with tools to turn your time-series database (TSDB) data into beautiful graphs and visualizations.
- It is Open-Source.
- Supports all major databases in same dashboard
- It has dynamic dashbaords and filters.
- It gives us the ability to create alerts, and explore metrics and logs.

### Grafana Architecture

   ![](./imgs/grafana-architecture.svg)
   <br/>

- Grafan connects to various data sources and, let's you query, visualize and setup alerting on the data.
- While, creating these dashboards we connect to various data sources like Prometheus, InfluxDB, ElasticSearch, MySQL, Postgres, etc.
- And, these data is gonna come up from various servers, applications, build nodes, database servers etc... and we are going to monitor all of them collect the metrics from these servers and, than going to send them to varous available data sources.
- Now, in order to collect the metrics and send them to the data sources, there are various agents available like Telegraf, Prometheus, etc...
- Depending on the agent we use for collecting the data, we may use push or pull mechanism to send the data to the data sources.

## Grafana UI Walkthrough

- This is the first view of Grafana UI, when you login using the credentials `admin/admin`.

  ![](./imgs/Screenshot%202024-02-01%20at%2011.08.11 AM.png)

### Dashboard

- Playlist: Within, the dashboard option, we have playlist option which allows us to create a playlist of dashboards and, we can also set the time interval for each dashboard, giving control of how long each dashboard should be displayed.

- Snapshots: If we create a dashboard and we want to share it with someone, we can create a snapshot of the dashboard and, share the snapshot URL with the person.

- Library Panels: Grafana Dashboard consists of several panels, and if we have some reusable panel we might want to add them to the library panel. So, that panel can be used by anyone who is creating dashbaord.

- Public dashboards: Grafana has a public dashboards repository, where we can find dashboards created by other users and, we can import them into our Grafana instance.

![](./imgs/Screenshot%202024-02-01%20at%2011.30.47 AM.png)

### Explore

- Explore is a tool that allows us to query the data sources and, visualize the data in a table format or in a graph format.
- Here, we can select various data sources, apply various queries here.

![](./imgs/Screenshot%202024-02-01%20at%2011.38.41 AM.png)


### Alerting

- Grafana allows us to create alerts on the metrics and, we can send the alerts to various channels like Slack, PagerDuty, etc...
- We get many options like:
  - Alert Rules: Here, we can create alert rules. For example, how frequently we want to check the data, what should be the threshold value, etc...
  - Contact Points: Here, we can add the contact points like Slack, PagerDuty, etc...
  - Notification Policies: Here, we can create notification policies, like when to send the notification, etc... This will help us with trigeering or muting the alert.
  - Silences: Here, we can create silences, like if we don't want to get notified for a particular alert, we can create a silence for that alert.
  - Groups: Here, we can create groups of alerts, like if we want to create a group of alerts for a particular application, we can create a group for that application.
  - Admin: Here, we can see all the configurations related to the alerts created.

![](./imgs/Screenshot%202024-02-01%20at%2011.44.38 AM.png)

### Connections

- Here, we can add various data sources like Prometheus, InfluxDB, ElasticSearch, MySQL, Postgres, etc... using Grafana.

![](./imgs/Screenshot%202024-02-01%20at%2011.51.56 AM.png)

### Administration

- Plugins: Here, we can add various plugins to Grafana.
- Users: Here, we can add various users to Grafana, and we can also assign various roles to the users.
- Teams: Here, we can create various teams and, we can assign various roles to the teams, and than we can add users to the teams.
- Service Accounts: So, let's we want to interact with grafana using APIs, in that case we will use a service account and, a token. That token will be used to connect to Grafana.
- Default Preferences: Here, we can set the default preferences for the users. And, if user wants to change any preferences they wil be able to change it from here.
- Settings: Here, we can change the settings of Grafana. If we want to make any changes to the settings, we can make it in `grafana.ini` or `custom.ini` file.
- Organizations: Here, we can create various organizations and, each organization can have it's own set of users, teams, dashboards, etc...
- Statistics and Licensing: Here, we can see the statistics of Grafana and, we can also add the license for Grafana.

![](./imgs/Screenshot%202024-02-01%20at%2011.59.21 AM.png)