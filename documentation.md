I am not able to create a testable and good monitoring stack with the tools I have, so for this last step I will just state my approach to monitoring on all stages.

Stage 1 of monitoring: Ingestion and Raw Events
- This is what has been demoed in the first part. We need to be able to define governance and see if events are coming in according to what our stack expects.
- Typical and open-source monitoring tool to be implemented: Prometheus
- Alerts to be configured:
   - volume of failed events (alerts based on threshold)
   - failed events per error type
   - volume of events in the DLQ
 
Stage 2 of monitoring: Data Pipelines
- The second stage involves monitoring the orchestration of data that has been ingested, either through events or through direct sourcing from other systems (APIs, SQL or from tools like Fivetran).
- Typical and open-source tool for the orchestration is Airflow, with each step exporting data to Prometheus.
- Alerts to be configured:
    - total events ingested per DAG
    - total

Stage 3 of monitoring: Data Quality
- This one ensures that the data being processed is ready to be consumed and activated. Ensures validation when it comes to volume, expected fields, and overall data quality and data structure problems.
- Typical and open-source tool for this is to configure Great Expectations over the entire project, or create a set of SQL tests for each main data pipeline. Also valid to implement a data lineage tool, and understand where each data point is coming from.

  What We're Looking For
● Do you monitor the right things (business-critical metrics)?
● Is your detection methodology sound?
● Are your thresholds sensible (catching real issues without alert fatigue)?
● Can you implement working detection logic?
● Is this practical for daily operations?

1. Do you monitor the right things (business-critical metrics)?
The monitoring is not only for business-critical metrics, but to ensure that the entire infrastructure that processes them is ready to be used and detect issues in real time. 

2. Is your detection methodology sound?
The proposed stack is based on latest tech that I have used and continue to be relevant in the industry. There are definitely better paid solutions and also these same ones provided as SaaS for easier configuration.

3. Are your thresholds sensible (catching real issues without alert fatigue)?
As mentioned above, the alerts should be based on threshold, but logging should be there for all of them. Using the dataset provided as an example, a lot of events are missing the client-id and this could break pipelines downstream.

4. Can you implement working detection logic?
I am not too well-versed in implementing the tech stack myself for this, but am well versed in configuring alerts in similar timeseries systems like the ones mentioned.

5. Is this practical for daily operations?
It requires a good stack configured, and scale accordingly. With the proposed Stack: Airflow, Prometheus, Grafana and Great Expectations, it is very ready for daily operations.




