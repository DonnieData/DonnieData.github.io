---
title: "Database Normalization"
excerpt: Modeling data to reduce redundancy and provide scalabilty for reporting
classes: wide
categories:
  - Post
header:
  overlay_image: /assets/images/norm1.jpeg
  actions:
    - label: "View the Repo" 
      url: ""
author_profile: True 
---
How can we utilize database normalization to assist with analysis. 

### Purpose 
Perform database normalization to optimze data storage, which will aloow for analysis of meter data.


### Steps of normalizaiton 

#### Review Data 
where can we reduce redundancy 
- payment type
- street block
- meter post id 
- payment ammount 
- timestamps 


#### Model Data 
- ERD  


#### Database 
- create schema 
- load data 


Testing on transaction data for 1 day: 

```SQL 
SELECT NORMALIZED_SCHEMA "Normalized Schema",
	NON_NORMALIZED_TABLE " Non-normalized Table",
	ROUND(((NON_NORMALIZED_TABLE - NORMALIZED_SCHEMA) / NON_NORMALIZED_TABLE) * 100,
		2) "Difference (%)"
FROM
	(SELECT SUM(PG_RELATION_SIZE(QUOTE_IDENT(SCHEMANAME) || '.' || QUOTE_IDENT(TABLENAME))) NORMALIZED_SCHEMA
		FROM PG_TABLES
		WHERE SCHEMANAME = 'sf_ticket_trans') STAT1,

	(SELECT PG_RELATION_SIZE('public.data_08012022') NON_NORMALIZED_TABLE) STAT2
```
| Normalized Schema  | Non-normalized Table | Difference (%) |
| ----------- | ----------- | ----------- |
| 6979584      | 7733248       | 9.75 |


  






