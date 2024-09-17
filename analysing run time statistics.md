### **Analyzing Runtime Statistics of APIs: Theoretical Explanation**

Runtime statistics refer to the monitoring, logging, and analysis of data generated when APIs are invoked and utilized by users or applications. Monitoring runtime statistics is crucial for understanding API performance, diagnosing issues, and making data-driven decisions to optimize and scale API services.


### **Practical Example: Analyzing API Runtime Statistics in WSO2 API Manager**

WSO2 API Manager provides detailed runtime statistics for API performance, traffic analysis, error rates, and other metrics. You can use the **WSO2 API Analytics Dashboard** to monitor these statistics in real-time.

#### **Step-by-Step Practical Example**

##### **1. Enable Analytics in WSO2 API Manager**
To analyze runtime statistics, you need to enable analytics in WSO2 API Manager.

1. **Open the Deployment Configuration**:
   - In the WSO2 API Manager installation directory, open the `deployment.toml` file (typically found in `repository/conf`).
   
2. **Enable Analytics**:
   - Ensure that the following configuration is enabled to collect statistics:
     ```toml
     [apim.analytics]
     enable = true
     ```
   - Configure the connection to the analytics server if using an external analytics server.

3. **Start the Analytics Service**:
   - If using WSO2’s inbuilt analytics, start the analytics component by executing:
     ```bash
     ./wso2am-analytics/bin/wso2server.sh start
     ```

4. **Log into the Analytics Dashboard**:
   - Navigate to `https://<WSO2-API-Manager>:9444/analytics-dashboard` to access the Analytics Dashboard.
   - Log in using your administrator credentials.

##### **2. Accessing API Runtime Statistics**

Once the analytics feature is enabled, you can view real-time and historical statistics about the API.

1. **Traffic and Usage**:
   - Navigate to the **Analytics Dashboard** and go to the **API Traffic** section.
   - You’ll see the total number of API requests made, response times, request count by users, and request distribution across endpoints.

2. **Latency and Throughput**:
   - The **Latency Overview** panel shows the average response time for API calls.
   - **Throughput** data reveals how many API calls are being processed per second, allowing you to gauge the efficiency of your APIs under load.

3. **Error Analysis**:
   - Under **Error Analysis**, you’ll see the percentage of requests that resulted in errors, grouped by status codes (`4xx`, `5xx`).
   - This helps you pinpoint common issues, such as misconfigured client requests or server-side problems.

4. **Throttling and Rate Limiting**:
   - Check the **Throttling Data** to see if API consumers are exceeding their allowed usage limits.
   - You can view how many times users were throttled and analyze traffic spikes to adjust your rate limiting policies if needed.

5. **Cache Performance**:
   - View **Cache Hits and Misses** for APIs that use caching. A higher cache hit rate indicates effective caching mechanisms, reducing the load on backend systems.

6. **API Response Codes**:
   - Monitor the response codes for each API invocation to identify issues. For example, a surge in `404 Not Found` or `500 Internal Server Error` indicates either routing issues or backend failures.

##### **3. Generating Custom Reports**

You can generate custom reports or visualizations based on runtime statistics, such as daily or weekly API performance summaries.

1. **Custom Dashboard**:
   - Use the WSO2 API Analytics Dashboard to create custom views that track specific metrics, such as traffic volume, latency, or response codes.
   - Create dashboards for different user groups, such as API developers, to help them monitor specific APIs.

2. **Export Data**:
   - Export runtime data to external tools or databases for long-term analysis, custom reporting, or integration with other business intelligence platforms.

---

#### **Practical Example: Using External Monitoring Tools**

You can integrate external monitoring tools like **Prometheus**, **Grafana**, or **ELK (Elasticsearch, Logstash, Kibana)** stack to collect and visualize runtime statistics of APIs.

##### **Step-by-Step Example: Monitoring API with Prometheus and Grafana**

1. **Install Prometheus and Grafana**:
   - Set up **Prometheus** for collecting metrics and **Grafana** for visualizing data.
   - Prometheus scrapes metrics from WSO2 API Manager and stores them in a time-series database.

2. **Expose Metrics in WSO2 API Manager**:
   - To expose runtime statistics in WSO2 API Manager, enable a metrics exporter like Prometheus.
   - Configure the Prometheus exporter in the `deployment.toml` file:
     ```toml
     [apim.prometheus]
     enable = true
     ```

3. **Configure Prometheus to Scrape Metrics**:
   - In Prometheus, add a job configuration to scrape metrics from WSO2 API Manager:
     ```yaml
     scrape_configs:
       - job_name: 'wso2_apim'
         static_configs:
           - targets: ['<WSO2-API-Manager>:9090']
     ```

4. **Visualize Metrics in Grafana**:
   - Use **Grafana** to create dashboards visualizing API traffic, latency, throughput, error rates, and other metrics.
   - Connect Grafana to Prometheus as a data source and create visualizations for API statistics.

5. **Custom Alerts**:
   - Set up custom alerts in Prometheus or Grafana for specific thresholds (e.g., high error rates or latency spikes). Alerts can notify administrators when APIs are underperforming or experiencing high error rates.
