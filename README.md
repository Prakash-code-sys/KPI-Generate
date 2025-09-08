# KPI-Generate
# Step1: To import dump from redmine to PSQL
1. download dump and remove unnecessary columns
2. Use below query to create table on PSQL
```
Create Table Mntools (
Ticket int primary key,	
Project	varchar (50),
Tracker	varchar (50),
Status varchar (50),
Priority varchar (50),
Subject	Text,
Author varchar (50),
Assignee varchar (50),
Updated Text,	
Start_date Text,	
Created	 Text,
Closed Text,	
Lastupdated_by	 varchar (50),
AI_BIT1_Tools varchar (50),
Task_Name Text,	
Circle_Project varchar (50),	
Resolvedby varchar (50),	
Resolution_Details Text, 	
Types varchar (20),
Type_Minutes varchar (20),	
IncidentTicket_Created varchar (10),	
Description Text,	
Last_notes Text
);
```
# Step 2:
1. Create table for template
2. import template to that table

```
Create table Projects (
 Tool_Name	varchar (50),
 Ticketing_system	varchar (50),
 Support_level	varchar (50),
 Team varchar (50),
 DU_Non_DU varchar (50),	
 Customer varchar (50),	
 Assignment_group varchar (50),	
 Week varchar (50),	
 Month varchar (50),	
 Total_issue_duration varchar (50), 	
 Actual_Working_hours varchar (50),	
 Support_Model varchar (50), 	
 Actual_Days_taken_to_complete_the_request varchar (50),	
 SLA_Status varchar (50),	
 app_IT varchar (50),
 initial_response_date_time varchar (50),
 initial_response_minutes varchar (50),
 initial_response_SLA varchar (50),
 monitoring_effectiveness varchar (50),
 issue_idnetified_time varchar (50),
issue_identified_mode varchar (50),
healthcheckapp_infra varchar (50),
healthcheck_category varchar (50),
ticket_category varchar (50),
incident varchar (50)
 );
```
# Step 3
1. Joining both mntools and projects using below query
2. Export the file and save as .csv
```
select * from projects
inner join mntools
on projects.tool_name = mntools.project
```
# Step 4:
1. Create table for final output
2. import the file which you exported from the step 3
```
Create table finalop(
 
 Tool_Name	varchar (50),
 Ticketing_system	varchar (50),
 Support_level	varchar (50),
 Team varchar (50),
 DU_Non_DU varchar (50),	
 Customer varchar (50),	
 Assignment_group varchar (50),	
 Week varchar (50),	
 Month varchar (50),	
 Total_issue_duration varchar (50), 	
 Actual_Working_hours varchar (50),	
 Support_Model varchar (50), 	
 Actual_Days_taken_to_complete_the_request varchar (50),	
 SLA_Status varchar (50),	
 app_IT varchar (50),
 initial_response_date_time varchar (50),
 initial_response_minutes varchar (50),
 initial_response_SLA varchar (50),
 monitoring_effectiveness varchar (50),
 issue_idnetified_time varchar (50),
issue_identified_mode varchar (50),
healthcheckapp_infra varchar (50),
healthcheck_category varchar (50),
ticket_category varchar (50),
incident varchar (50),
Ticket int primary key,	
Project	varchar (50),
Tracker	varchar (50),
Status varchar (50),
Priority varchar (50),
Subject	Text,
Author varchar (50),
Assignee varchar (50),
Updated Text,	
Start_date Text,	
Created	 Text,
Closed Text,	
Lastupdated_by	 varchar (50),
AI_BIT1_Tools varchar (50),
Task_Name Text,	
Circle_Project varchar (50),	
Resolvedby varchar (50),	
Resolution_Details Text, 	
Types varchar (20),
Type_Minutes varchar (20),	
IncidentTicket_Created varchar (10),	
Description Text,	
Last_notes Text
);
```
# Step 5:
  1. To get the final result use below query

```
Select tool_name,
ticketing_system,
support_level,
team,
du_non_du,
customer,
ticket,
status,
priority,
subject,
tracker,
author,
created,
assignment_group,
week,
month,
created,
updated,
updated,
description,
resolution_details,
total_issue_duration,
actual_working_hours,
support_model,
resolution_details,
actual_days_taken_to_complete_the_request,
sla_status,
type_minutes,
types,
author,
app_IT,
initial_response_date_time,
initial_response_minutes,
initial_response_SLA,
monitoring_effectiveness,
issue_idnetified_time,
issue_identified_mode,
healthcheckapp_infra,
healthcheck_category,
ticket_category,
IncidentTicket_Created,
incident,
case
when subject like 'Perform Health check in Rancher, Grafana SMTP%' then 'Monitoring'
when subject like 'WFO case handling process health check%' then 'Monitoring'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Monitoring'
when subject like 'NCIB open tickets validation%' then 'User Ticket'
when subject like 'NCIB- checking N-1 most recent%' then 'Monitoring'
when subject like 'NDP AI ML health check In Airflow & Postgres Pod utilization%' then 'Monitoring'
when subject like 'NDP AI ML health check for Precheck%' then 'Monitoring'
when subject like 'Health check of Smartapp Performance script for A1TA%' then 'Monitoring'
when subject like 'Perform CPU, Memory, Disk and Pod ADF%' then 'Monitoring'
when subject like 'insights NDPD AIML Smart Scheduling health%' then 'Monitoring'
when subject like 'insights for SWS - MR%' then 'Monitoring'
when subject like 'WFO Powerbi dashboard health chec%' then 'Monitoring'
when subject like 'Perform Health check of insights for Elasticsearch Audit report in%' then 'Monitoring'
when subject like 'Perform Health check of insights for Elasticsearch auditlog%' then 'Monitoring'
when subject like 'NDP AI ML health check for Precheck, Airflow DA%' then 'Monitoring'
when subject like 'Perform Health Check in Grafana%' then 'Monitoring'
when subject like 'insights NDPd A1 Austria, Mwingz, TEFSpain and Perfectum%' then 'Monitoring'
when subject like 'insights SWS dataflow and dataset case table%' then 'Monitoring'
when subject like 'Attend AI BI T1-T2 Weekly Internal%' then 'Meeting'
when subject like 'Smartapp_TEMS Discovery Device%' then 'User Ticket'
when subject like 'Perform Health check of insights for Care SWS reports date%' then 'Monitoring'
end as monit_effect,

CASE
when subject like 'Perform Health check in Rancher, Grafana SMTP%' then 'HC Report'
when subject like 'WFO case handling process health check%' then 'Health check'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Health check'
when subject like 'NCIB open tickets validation%' then 'User Mail'
when subject like 'NCIB- checking N-1 most recent%' then 'HC Report'
when subject like 'NDP AI ML health check In Airflow & Postgres Pod utilization%' then 'Health Check'
when subject like 'NDP AI ML health check for Precheck%' then 'Health Check'
when subject like 'Health check of Smartapp Performance script for A1TA%' then 'Health Check'
when subject like 'Perform CPU, Memory, Disk and Pod ADF%' then 'Health Check'
when subject like 'insights NDPD AIML Smart Scheduling health%' then 'HC Report'
when subject like 'insights for SWS - MR%' then 'HC Report'
when subject like 'WFO Powerbi dashboard health chec%' then 'HC Report'
when subject like 'Perform Health check of insights for Elasticsearch Audit report in%' then 'HC Report'
when subject like 'Perform Health check of insights for Elasticsearch auditlog%' then 'HC Report'
when subject like 'NDP AI ML health check for Precheck, Airflow DA%' then 'Health Check'
when subject like 'Perform Health Check in Grafana%' then 'Health Check'
when subject like 'insights NDPd A1 Austria, Mwingz, TEFSpain and Perfectum%' then 'HC Report'
when subject like 'insights SWS dataflow and dataset case table%' then 'HC Report'
when subject like 'Attend AI BI T1-T2 Weekly Internal%' then 'Meeting'
when subject like 'Smartapp_TEMS Discovery Device%' then 'User Mail'
when subject like 'Perform Health check of insights for Care SWS reports date%' then 'HC Report'
end as issue_iden_mode,

CASE
when subject like 'Perform Health check in Rancher, Grafana SMTP%' then 'HC Report'
when subject like 'WFO case handling process health check%' then 'Health Check'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Health Check'
when subject like 'NCIB open tickets validation%' then 'Ticket Validation'
when subject like 'NCIB- checking N-1 most recent%' then 'HC Report'
when subject like 'NDP AI ML health check In Airflow & Postgres Pod utilization%' then 'Health Check'
when subject like 'NDP AI ML health check for Precheck%' then 'Health Check'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Health Check'
when subject like 'Health check of Smartapp Performance script for A1TA%' then 'Health Check'
when subject like 'Perform CPU, Memory, Disk and Pod ADF%' then 'Health Check'
when subject like 'insights NDPD AIML Smart Scheduling health%' then 'HC Report'
when subject like 'insights for SWS - MR%' then 'HC Report'
when subject like 'WFO Powerbi dashboard health chec%' then 'HC Report'
when subject like 'Perform Health check of insights for Elasticsearch Audit report in%' then 'HC Report'
when subject like 'Perform Health check of insights for Elasticsearch auditlog%' then 'HC Report'
when subject like 'NDP AI ML health check for Precheck, Airflow DA%' then 'Health Check'
when subject like 'Perform Health Check in Grafana%' then 'Health Check'
when subject like 'insights NDPd A1 Austria, Mwingz, TEFSpain and Perfectum%' then 'HC Report'
when subject like 'insights SWS dataflow and dataset case table%' then 'HC Report'
when subject like 'Attend AI BI T1-T2 Weekly Internal%' then 'Meeting'
when subject like 'Smartapp_TEMS Discovery Device%' then 'User Mail'
when subject like 'Perform Health check of insights for Care SWS reports date%' then 'HC Report'
end as issue_iden_mod1,

CASE
when subject like 'Perform Health check in Rancher, Grafana SMTP%' then 'Infra'
when subject like 'WFO case handling process health check%' then 'Application'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Application'
when subject like 'NCIB open tickets validation%' then 'Application'
when subject like 'NCIB- checking N-1 most recent%' then 'Application'
when subject like 'NDP AI ML health check In Airflow & Postgres Pod utilization%' then 'Infra'
when subject like 'NDP AI ML health check for Precheck%' then 'Application'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Application'
when subject like 'Health check of Smartapp Performance script for A1TA%' then 'Application'
when subject like 'Perform CPU, Memory, Disk and Pod ADF%' then 'Infra'
when subject like 'insights NDPD AIML Smart Scheduling health%' then 'Application'
when subject like 'insights for SWS - MR%' then 'Application'
when subject like 'WFO Powerbi dashboard health chec%' then 'Application'
when subject like 'Perform Health check of insights for Elasticsearch Audit report in%' then 'Infra'
when subject like 'Perform Health check of insights for Elasticsearch auditlog%' then 'Application'
when subject like 'NDP AI ML health check for Precheck, Airflow DA%' then 'Application'
when subject like 'Perform Health Check in Grafana%' then 'Infra'
when subject like 'insights NDPd A1 Austria, Mwingz, TEFSpain and Perfectum%' then 'Application'
when subject like 'insights SWS dataflow and dataset case table%' then 'Application'
when subject like 'Attend AI BI T1-T2 Weekly Internal%' then 'Application'
when subject like 'Smartapp_TEMS Discovery Device%' then 'Application'
when subject like 'Perform Health check of insights for Care SWS reports date%' then 'Application'
end as healthchckapp_infra,

CASE
when subject like 'Perform Health check in Rancher, Grafana SMTP%' then 'Pod Metrics'
when subject like 'WFO case handling process health check%' then 'Similar case id test'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Nifi SDB blocks health check'
when subject like 'NCIB open tickets validation%' then 'Ticket Validation'
when subject like 'NCIB- checking N-1 most recent%' then 'Data Monitoring'
when subject like 'NDP AI ML health check In Airflow & Postgres Pod utilization%' then 'Pod Metrics'
when subject like 'NDP AI ML health check for Precheck%' then 'Precheck usecase'
when subject like 'Perform Nifi health check for NDPDeploy SDB%' then 'Nifi SDB blocks health check'
when subject like 'Health check of Smartapp Performance script for A1TA%' then 'Data Monitoring'
when subject like 'Perform CPU, Memory, Disk and Pod ADF%' then 'Pod Metrics'
when subject like 'insights NDPD AIML Smart Scheduling health%' then 'Data Monitoring'
when subject like 'insights for SWS - MR%' then 'Data Monitoring'
when subject like 'WFO Powerbi dashboard health chec%' then 'Data Monitoring'
when subject like 'Perform Health check of insights for Elasticsearch Audit report in%' then 'Pod Metrics'
when subject like 'Perform Health check of insights for Elasticsearch auditlog%' then 'Elasticsearch Auto trigger validation'
when subject like 'NDP AI ML health check for Precheck, Airflow DA%' then 'Precheck usecase'
when subject like 'Perform Health Check in Grafana%' then 'Pod Metrics'
when subject like 'insights NDPd A1 Austria, Mwingz, TEFSpain and Perfectum%' then 'Data Monitoring'
when subject like 'insights SWS dataflow and dataset case table%' then 'Data Monitoring'
when subject like 'Attend AI BI T1-T2 Weekly Internal%' then 'Meeting'
when subject like 'Smartapp_TEMS Discovery Device%' then 'Software Upgrade Activity '
when subject like 'Perform Health check of insights for Care SWS reports date%' then 'Data Monitoring'
end as healthcheckcategory

from finalop
order by ticket
```

