# Quick Start with Prometheus and Server Monitoring Dashboards

![](./imgs/grafana-prometheus-archi.svg)

- So, as clear from the diagram, the user interacts with the Grafana UI.
- The Web interface fetches data from Grafana Server. Here, the grafana services are running, we can play around with configuration, do SMTP configuration, etc...
- Also, when we are creating a new dashboard, we will have to connect to a data source.
- For example, we want to build a dashboard that uses data from Prometheus Server. In that case we are going to create a data source in Grafana, and connect to Prometheus Server.
- So, we will be giving IP Address of Prometheus Server, followed by the port which is `9090` by default.
- Once, that is done Grafana is going to pull the data from Prometheus Server, adn will show the visualization.
- So, where prometheus Server gets data from?? It pulls the data from different exporters.
  - For example, if you want server utilization o server related details, in that case you are going to make use of node exporter.
- The Node Exporter is like an agent which is going to pull system matrix like utilization disk utilization, and it also creates an endpoint, like an API. So, we can hit that API to get the data. And, the API is going to run on IP Address followed byt the port which is `9100` by default.
- So, all the servers which we want to monitor, we will have to install node exporter on all those servers. And, than in the prometheus server configuration file you define how often you want to pull the data from the node exporter.
  - So, let's say in the Prometheus Configuration file we set it to 10s that we want to pull data from node exporter every 10s.
  - In that case, every 10s Prometheus Server is going to initiate a connection and going to connect to eachod the different node exporters, and it will use `<ip_address>:port/metrics`. This is the API or endpoint we were talking about. So, Prometheus is going to initiate the connection to these endpoints.
  - All the data which is pulled by the Prometheus Server is kept in the database which is Prometheus Database, which is a time-series database, which is than utilized by the Grafana Server.

- On MacOS, we can start the Grafana Server using the command `brew services start grafana`. Than you can access the Grafana at `127.0.0.1:3000`.

## Prometheus Setup and First Look

- Same way, after installing prometheus use the command `brew services start prometheus`. Than we access prometheus at `127.0.0.1:9090`.

![](./imgs/Screenshot%202024-02-02%20at%2011.25.02 AM.png)

- If we go into `status` and, than to `Targets`, here we can see all the target servers which prometheus is goign to scape.
- All the node manager/exporter which we are using, all of this should be shown here in the target.
- Initially the prometheus server is scraping itself.

![](./imgs/Screenshot%202024-02-02%20at%2011.29.52 AM.png)

-  And, fi we go to `127.0.0.1:9090/metrics`, we can see all the data which is being scraped.

![](./imgs/Screenshot%202024-02-02%20at%2011.32.34 AM.png)

- All the configuration related to prometheus is stored in `prometheus.yml` file.

![](./imgs/Screenshot%202024-02-02%20at%2011.59.35 AM.png)

- The `scrape_inteval` is the interval at which prometheus is going to scrape the data from the node exporter.
- There's soemthing called as `evaluation_interval` as well, which is required only when we are setting up some rules.
- Than we see, `scrape_configs`, here we have a `job_name` and, than we have `targets`, where all the targets are defined which are to be scraped.

## node_exporter Setup and First Look

- We can install node_exporter using the command `brew install node_exporter`.
- Once, installed `node_exporter`, can be accessed via `localhost:9100`.
- But, you won't see that directly visible on the prometheus server, because we haven't added it to the `prometheus.yml` file. So, we will have to add it to the `prometheus.yml` file.
- So, do the following:

  ```bash
  > cd ..
  > cd ..
  > cd /opt/homebrew/etc
  > cat prometheus.yml
  ```

  Make the following changes in the `prometheus.yml` file:

  ```yml
    global:
    scrape_interval: 15s

    scrape_configs:
    - job_name: "prometheus"
        static_configs:
        - targets: ["localhost:9090","localhost:9100"]
  ```

  Now save, and restart the prometheus.

  ![](./imgs/Screenshot%202024-02-05%20at%204.38.08 PM.png)

## Grafana Dashboard to Monitor Servers

- So, now we are going to create a dashboard in Grafana to monitor the servers.
  - Go to Grafana, and than goto `Connections`.
  - Than, go to `Data Sources` and, click on `Add Data Source`.
  - Search for `Prometheus`.
  - Provide the Prometheus URL.
  - Set HTTP Method to `GET`.
  - If it says succesfull, than it means we have successfully configured data source for Grafana.
  - Scroll up, and click on `Explore Data`.
  - Set metric to `go_gc_duration_seconds_sum` or anything you desire.
  ![](./imgs/Screenshot%202024-02-05%20at%204.44.49 PM.png)

- The otheer way is to import the dashboard from the <a href="https://grafana.com/grafana/dashboards/">Grafana Dashboard Repository</a>.
  - Go to `Dashboards` and, than click on `Manage`.
  - Click on `Import`.
  - Than, provide the dashboard URL or ID.
  - Than, click on `Load`.
  - Than, click on `Import`.
  - Than, click on `Save and Open`.
  - Than, click on `Dashboard

- You will see a dashbaord as follows (ID: 1860):
  - ![](./imgs/Screenshot%202024-02-10%20at%208.03.24 PM.png)