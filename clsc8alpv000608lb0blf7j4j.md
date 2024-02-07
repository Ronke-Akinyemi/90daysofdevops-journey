---
title: "Connecting EC2 with Grafana"
datePublished: Wed Feb 07 2024 20:14:37 GMT+0000 (Coordinated Universal Time)
cuid: clsc8alpv000608lb0blf7j4j
slug: connecting-ec2-with-grafana
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707322767400/994c89f1-a3a6-4e2c-b776-ec571f2eb790.png
tags: aws, grafana, 90daysofdevops

---

## **Introduction to Monitoring EC2 Instances with Grafana, Loki, and Promtail**

In modern cloud-based environments like Amazon Web Services (AWS), monitoring the performance and health of your EC2 instances is crucial for maintaining system reliability and optimizing resource usage. Grafana, coupled with Loki and Promtail, offers a robust solution for visualizing metrics and logs from EC2 instances in a centralized and user-friendly manner.

### **Grafana**

Grafana is an open-source platform used for monitoring, visualization, and analytics of time-series data. It allows users to create customizable dashboards and visualizations to observe and analyze metrics from various sources, such as databases, monitoring systems, and applications.

### **Loki**

Loki is a highly-scalable log aggregation system designed to efficiently store and query logs from distributed systems. As a cost-effective and operationally simple solution, Loki seamlessly integrates with Grafana to provide powerful log monitoring capabilities for your EC2 instances.

### **Promtail**

Promtail serves as an agent responsible for collecting logs from local files on your EC2 instances and forwarding them to Loki for storage and analysis. Its lightweight nature and straightforward deployment make it an ideal tool for monitoring logs in cloud environments.

### Creating a dashboard using Grafana with the integration of Loki and Promtail

Steps involved:

Set up your EC2 instance. You can refer [HERE](https://ronke.hashnode.dev/grafana-setup).

**Install Docker:** We'll install Loki and Promtail using Docker, so Docker has to be installed first.

```basic
sudo apt-get update
sudo apt install docker.io
sudo usermod -aG docker $USER
sudo reboot
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707301213784/6eb4452e-2c33-4a19-81a9-2f42bb1f31aa.png align="center")

### **Download Loki Config file for Loki to run Loki in the Docker container**

Create a folder and download the yaml file that will contain the required configuration for running Loki.

```basic
mkdir grafana_configs
cd grafana_configs
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707302707383/1921ff69-a67a-47d4-8931-3b6e023483fa.png align="center")

Run the docker container using the following command.

```basic
sudo docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707310120276/b0024ae7-1202-4e85-96be-5aa8acde20e3.png align="center")

Open port 3100 in the security group to make the loki container running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707310272888/31ab7e95-de6d-45ef-8725-db36ff950ff0.png align="center")

Navigate to the public url of the EC2 instance, "public URL:3100/ready"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707310488438/da571b5f-5668-4f5b-b8a9-7f8b1ad9e901.png align="center")

You can also see the metrics which is the logs and the main purpose of Loki to collect and use "public URL:3100/metrics"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707310959062/4ac4730f-9c88-4742-b4c1-813dacd72b02.png align="center")

### **Download Promtail Config for Promtail to run in the Docker container**

```basic
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707303511238/48d74283-7835-4fd0-8bec-800823c61726.png align="center")

Run the Promtail docker container using the following command.

```basic
 sudo docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707311267527/a6a2915e-8d60-4700-81b2-12d5b6490764.png align="center")

### **Add Loki as a Data Source in Grafana**

In Grafana, click on "Data Sources".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707314041881/19588ac5-9c50-4d18-b716-25e19b25470e.png align="center")

Enter the URL of your Loki instance (e.g., `http://localhost:3100`).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707314909975/6653bc4f-1155-47b3-af84-a738681d0434.png align="center")

Click "Save & test" to ensure Grafana can connect to Loki.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707315524387/dd73e7cf-d3f5-4123-ad0d-e54276409dba.png align="center")

In the "Label filters" you can choose "job" and "varlogs" to show all the system logs. Then click "Run query".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707316117792/cb101fb8-dbfc-432d-ab0f-df61b109052d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707316364442/b0a5e171-d00a-4325-b13d-fbdecd73c882.png align="center")

### **Create a Dashboard**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707316450970/b2333c95-c324-45f0-ad74-c8cc4b68d889.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707317088265/e84f4ea7-003e-4059-94d6-d72568c07129.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707317224610/a5db3dbf-aef1-4a92-8e3c-07687a615d3a.png align="center")

In "Label filters" choose "job" and "varlogs" and "line contains" to "error" to show all the lines with error.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707317390371/81a6d20c-cf1c-4ec5-bdb0-14cb674bde40.png align="center")

Let's check the error lines in grafana log that is placed in ***/var/log/grafana/grafana.log***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707317564491/8e3ee635-9e3a-400d-ac83-eb519a996f01.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707317725394/df25b4da-9ecc-4df1-af47-d2f180cb8138.png align="center")

To fulfill the primary goal of displaying logs in Grafana, the path to the Grafana logs must be specified within the `targets` section of the Promtail configuration YAML file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707318378830/e21c4ed5-5c63-4f1c-b2ef-914cab88c16a.png align="center")

After editing the promtail\_config.yaml file, restart your Promtail Docker container."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707319052644/f7160c1a-c738-4b6b-913b-5d4570d22916.png align="center")

We can now choose the "Label filters" to set the "job" and "grafanalogs" with the line contains and visualization option to view in a graphical manner. We can add this to our dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707319590866/3743897e-47bf-468b-ab48-2a3f3023d1f3.png align="center")

Now, install nginx on the EC2 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707319770575/e7ba94c9-5abc-4adb-948b-caa145d17ce8.png align="center")

To count how often 'nginx' appears during installation, use 'varlogs' as the label filter.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707320779339/4c85a116-f950-4515-97f3-abbdb9ef990a.png align="center")

Here is the complete Grafana dashboard

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707320883186/9b41b53a-0dc7-4866-93b9-a40bc5021960.png align="center")

Thank you for reading.