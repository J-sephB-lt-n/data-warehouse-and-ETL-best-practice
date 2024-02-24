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
| | | [Perform automatic data cleaning at ingestion](#data-cleaning)
| There are duplicate records in the data                    | | 
| The database is very slow to query                         | | [Data should be indexed along the most common query dimensions](#data-indexing) 
| | | [Service each logical business unit with their own data mart](#data-marts)
| Data is not stored in a tabular format                     | yaml, json, noSQL | [Service each logical business unit with their own data mart](#data-marts) 
| There are missing (NULL) values. How do I interpret them?  | |  
| The same entity is recorded multiple times                 | The same customer has been registered multiple times under different customer IDs | [monitor data quality metrics](#data-quality-metrics) 
| Spelling errors and inconsistent category labelling | e.g. the *gender* field contains "male", "M", "Male" etc. | [Perform automatic data validation at ingestion](#data-validation) 
| | | [Perform automatic data cleaning at ingestion](#data-cleaning)
| | | [Add constraints to the data entry system](#constraints-at-data-entry)
| Data types are incorrect or unorthodox | weight="5kg" (should be weightKg=5) | 
| There are data points which look obviously wrong | | [Perform routine anomaly detection](#anomaly-detection) 
|                                                  | | [Monitor data quality metrics](#data-quality-metrics)
| I don't have the latest data                     | | [Failures and worsening data quality metrics should raise an alarm](#alerting)


# Data Warehouse Best Practices

| Good Practice                                        | Description            |Reason
|------------------------------------------------------|------------------------|--------------
| <a id=access-controls>Access controls</a>            |                        |
| <a id=alerting>Failures and worsening data quality metrics should raise an alarm</a>     |                        |
| <a id=constraints-at-data-entry>Add constraints to the data entry system</a> |Data uniformity and quality can be enforced by limiting user options on a data entry system| 
| <a id=data-dictionary>Keep a data dictionary</a>     | A data dictionary is documentation describing what each data field means, how it is calculated, how it may be used etc.| Good data documentation enables end users (analytics, ML engineers etc.) to use the data without having to trawl through your organisation trying to piece together what the data means.  
| <a id=data-marts>Service each logical business unit with their own data mart</a> | | 
| <a id=data-normalisation>Data in relational databases should be normalised</a> | Normalisation is a ubiquitous relational database organisation standard proposed by Edward Codd | * Protects against duplication and redundancy
|                                                      | | * Consistent and organized data
|                                                      | | * Protects against anomalies arising during INSERT, DELETE or UPDATE
| <a id=data-cleaning>Automated data cleaning</a> | | |
| <a id=data-indexing>Data should be indexed along the most common query dimensions</a> | | 
| <a id=data-validation>Automated data validation</a>  | | |
| <a id=document-the-etl-process>Document the ETL process</a> | 
| <a id=data-ownership>Each data field owned by a specific person or team</a> ||   
| <a id=anomaly-detection>Anomaly detection</a> | | 
| <a id=failure-response>Failure response</a>          | 
| <a id=log-everything>Log everything</a>              | 
| <a id=data-quality-metrics>Monitor [data quality metrics](#data-quality-metrics)</p> | |
| <a id=observability-and-monitoring>Observability and monitoring</a> |  
| <a id=structured-logging>Structured Logging</a> | 
| <a id=timestamp-every-data-point>Timestamp every data point</a> | 
| <a id=data-drift>Monitor data drift and concept drift</a>|Data drift is a change in the distribution of the data. Concept drift is a change in the relationships between fields | These kinds of changes are a powerful indicator of error or opportunity

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
