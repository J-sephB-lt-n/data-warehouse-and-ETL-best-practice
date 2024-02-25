# Data warehouse and ETL best practice
A catalogue of best practices for managing data

I've catalogued here a [list of common problems which hinder data analysis and machine learning](#common-problems-which-hinder-data-analysis-and-machine-learning), and [a list of good practices for negating them](#data-warehouse-best-practices).

# Common problems which hinder data analysis and machine learning

| Problem                                                    | Example(s) |Solution(s)
|------------------------------------------------------------|------------|--------
| What do the fields in the data mean? How are they defined? Where does the data come from? | | [Keep a data dictionary](#data-dictionary) 
|                                                            | | [Each data field owned by a specific person or team](#data-ownership) 
|                                                            | | [Document the ETL process](#document-the-etl-process)
| I can't find the data that I want                          | | [Keep a data dictionary](#data-dictionary)
|                                                            | | [Data in relational databases should be normalised](#data-normalisation) 
| Data is inconsistently formatted (e.g. different datetime formats in different parts of the database) | | [Perform automatic data validation at ingestion](#data-validation) 
| | | [Perform automatic data cleaning](#data-cleaning)
| There are duplicate records in the data                    | | Perform automated [data validation](#data-validation)
|                                                            | | [Data in relational databases should be normalised](#data-normalisation) 
| The database is very slow to query                         | | [Data should be indexed along the most common query dimensions](#data-indexing) 
| | | [Service each logical business unit with their own data mart](#data-marts)
| | | [Monitor system performance metrics](#system-performance-metrics) 
| Data is not stored in a tabular format                     | yaml, json, noSQL | [Service each logical business unit with their own data mart](#data-marts) 
| There are missing (NULL) values. How do I interpret them?  | | [Each data field owned by a specific person or team](#data-ownership) 
| | | [Keep a data dictionary](#data-dictionary) 
| | | [Perform automated data cleaning](#data-cleaning)
| | | Perform automated [data validation](#data-validation)
| | | [Add constraints to the data entry system](#constraints-at-data-entry)
| The same entity is recorded multiple times                 | The same customer has been registered multiple times under different customer IDs | Perform automated [data validation](#data-validation)
| | | [Add constraints to the data entry system](#constraints-at-data-entry)
| Spelling errors and inconsistent category labelling | e.g. the *gender* field contains "male", "M", "Male" etc. | [Perform automatic data validation at ingestion](#data-validation) 
| | | [Perform automatic data cleaning at ingestion](#data-cleaning)
| | | [Add constraints to the data entry system](#constraints-at-data-entry)
| Data types are incorrect or unorthodox | weight="5kg" (should be weightKg=5) | [Perform automated data cleaning](#data-cleaning)
| | | Perform automated [data validation](#data-validation)
| | | [Add constraints to the data entry system](#constraints-at-data-entry)
| There are data points which look obviously wrong | | [Perform routine anomaly detection](#anomaly-detection) 
|                                                  | | [Monitor data quality metrics](#data-quality-metrics)
| I can't access the latest data because the ETL process is too slow | | 
| Whoops - I deleted data by accident | | [Establish procedures for scheduled backup and disaster recovery](#scheduled-backup-and-recovery) 


# Data Warehouse and ETL Best Practices

| Good Practice                                        | Description            |Reason
|------------------------------------------------------|------------------------|--------------
| <a id=access-control>Access control</a>            |                        |
| <a id=alerting>Failures and worsening data quality metrics should raise an alarm</a>|Alerting means bringing issues quickly to the attention of the data administrators/engineers|In a data pipeline, data errors quickly propagate to downstream processes and data consumers, so quick response is important
| <a id=constraints-at-data-entry>Add constraints to the data entry system</a>| Limits on the types of data that can be input into the system allow direct control over the inflow of data into the system| This can be used to enforce data uniformity and quality can be enforced by limiting user options on data entry systems | 
| <a id=data-dictionary>Keep a data dictionary</a>     | A data dictionary is data documentation enabling a user to understand and use the data without the need for any other source of information i.e. describing what each data field means, how it is calculated, how it may be used etc.| Good data documentation enables end users (analytics, ML engineers etc.) to use the data without having to trawl through your organisation trying to piece together what the data means.  
| <a id=data-marts>Service each logical business unit with their own data mart</a> |A [data mart](https://en.wikipedia.org/wiki/Data_mart) is a subset (and/or transformation) of the full data designed to service the needs of a specific segment of data consumers (e.g. the marketing department)|Reduces computational load on the main data warehouse
||| Can make the data more accessible to data consumers (they are not overwhelmed with irrelevant data) 
||| Can be used to facilitate data access control 
| <a id=data-normalisation>Data in relational databases should be normalised</a> | Normalisation is a ubiquitous relational database organisation standard proposed by Edward Codd | Protects against data duplication and redundancy
|                                                      | | Results in consistent and organized data with a predictable format
|                                                      | | Protects against anomalies arising during INSERT, DELETE or UPDATE
| <a id=data-cleaning>Automated data cleaning</a> |Transformation of data into a more usable form by an automatic process (e.g. a scheduled process, or at ingestion time)| Avoids each data consumer having to do this themselves before being able to use the data 
| <a id=data-indexing>Data should be indexed along the most common query dimensions</a> |The data should be optimized for querying in the way in which it is expected to be most commonly queried| This can increase the speed at which data can be accessed by orders of magnitude
| <a id=data-validation>Automated data validation</a>|Verifying whether the data conforms to certain prespecified data quality rules in an automated fashion|Can be used to keep the data quality high, by rejecting low quality input, or use for monitoring input data quality. 
| <a id=document-the-etl-process>Document the ETL process</a> | The process by which data arrives in its final production state in the data warehouse should be clearly documented | Enables quick onboarding of new data administrators
| | | Gives contextual understanding of the data to data consumers like analysts and machine learning engineers
| <a id=data-ownership>Each data field owned by a specific person or team</a>|Each field in (or other logic partition of) the data should have a specific individual or team responsible for understanding and maintaining the quality of it. This contact person/team should be clearly documented alongside the data which they are responsible for|Without this, organisational knowledge can be permanently lost and data quality deteriorate.
| <a id=anomaly-detection>Anomaly detection</a> |New data not matching the historic or expected distribution of data should be identified and investigated|Anomalies are usually either data errors or unusual system phenomena, both of which are worthy of investigation  
| <a id=failure-response>Failure response</a>| 
| <a id=log-everything>Log everything</a>|Logs are persistent written records of the actions taken by the system (e.g. data pipeline)|When something goes wrong, logs tell us what happened  
| <a id=data-quality-metrics>Monitor [data quality metrics](#data-quality-metrics)</p>|Single number summaries of data quality (record counts, % null values, pipeline runtime etc.) should be recorded and watched closely|These metrics provide early warning that something in the data pipeline has gone wrong
| <a id=observability-and-monitoring>Observability and monitoring</a>|[Data quality](#data-quality-metrics) and other system performance metrics should be surfaced to data administrators/engineers in an interface or platform which makes the metrics easy to visualise, interrogate and explore|Can help provide early warning of errors in the data pipeline 
||| Can help with debugging, understanding and resolving errors in the data pipeline
| <a id=timestamp-every-data-point>Timestamp every data point</a> | 
| <a id=data-drift>Monitor data drift and concept drift</a>|Data drift is a change in the distribution of the data. Concept drift is a change in the relationships between fields | These kinds of changes are a powerful indicator of error or opportunity
| <a id=structured-logging>Use structured logging</a> | | | 
| <a id=scheduled-backup-and-recovery>Establish procedures for scheduled backup and disaster recovery</a>|| 
| <a id=data-lineage>Data lineage</a>| | | 
| <a id=system-performance-metrics>Monitor system performance metrics</a>| | |

# Security Principles

| Principle                | Explanation
|--------------------------|------------------
| Observability/monitoring |
| Incident response        |
| Defense in Depth         |
| Separation of Duties     |
| Data encryption          | In transit and at rest
| Least Privilege          | 
| Secure by Design         | 

# Data Quality Metrics
https://www.ibm.com/downloads/cas/W6BAW9MQ
