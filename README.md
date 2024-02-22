# Data warehouse and ETL best practice
A catalogue of best practices for managing data

As a long-time end user of data (for dashboarding, analytics and machine learning), I've catalogued here a [list of data management inefficiencies that have repeatedly wasted a lot of my time](#common-struggles-as-a-data-consumer), and [a list of good practices for negating them](#data-warehouse-best-practices)

# Common Struggles as a Data Consumer

| Problem                                                    | Solution(s)
|------------------------------------------------------------|---------------------
| What do the fields in the data mean? How are they defined? Where does the data come from? | [Keep a data dictionary](#data-dictionary) 
|                                                            | [Each data field owned by a specific person or team](#data-ownership) 
|                                                            | [Document the ETL process](#document-the-etl-process)
| I can't find the data that I want                          | [Keep a data dictionary](#data-dictionary)
|                                                            | [Data in relational databases should be normalised](#data-normalisation) 
| Data format inconsistent (e.g. datetime format not consistent over time) | 
| Data requires cleaning (e.g. datetimes stored as strings)  | 

# Data Warehouse Best Practices

| Good Practice                                        | Description            |Reason
|------------------------------------------------------|------------------------|--------------
| <a id=access-controls>Access controls</a>            |                        |
| <a id=alerting>Alerting</a>                          |                        |
| <a id=data-dictionary>Keep a data dictionary</a>            | To document:           |
|                                                      | * unit of measurement  |
|                                                      | * formula defining calculated field | 
| <a id=data-normalisation>Data relational databases should be normalised</a> | A widely-used relational database organisation standard proposed by Edward Codd | * Protects against duplication and redundancy
|                                                      | | * Consistent and organized data
|                                                      | | * Protects against anomalies arising during INSERT, DELETE or UPDATE
| <a id=document-the-etl-process>Document the ETL process</a> | 
| <a id=data-ownership>Data ownership</a>              |   
| <a id=failure-response>Failure response</a>          | 
| <a id=log-everything>Log everything</a>              | 
| <a id=observability-and-monitoring>Observability and monitoring</a> |  
| <a id=structured-logging>Structured Logging</a> | 
| <a id=timestamp-every-data-point>Timestamp every data point</a> | 

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
