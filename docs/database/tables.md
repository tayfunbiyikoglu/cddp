# Tables

## Exception Customer Module

This is a simple module that has one table. This table is used to keep
the customers/applicants that are excluded from deletion.

Business registers their customers/applicants with their reason to keep. They should also provide a date that this exclusion is valid. After that date the first deletion procedure will pick this customer/applicant for deletion. 


### Module Tables

#### Main Table

{== MMS.DD_EXCEPTION_CUSTOMERS ==}

| COLUMN              	| DATATYPE    	| INFO           	|
|---------------------	|-------------	|-----------------	|
| OID                 	| NUMBER(16)  	|                 	|
| STATUS              	| NUMBER(1)   	|                 	|
| LASTUPDATED         	| NUMBER(15)  	|                 	|
| CUSTOMEROID         	| NUMBER(16)  	|                 	|
| APLICANTTYPE        	| VARCHAR2(5) 	| LOAN, DEPT     	|
| APPLICANTOID        	| NUMBER(16)  	|                 	|
| REGULARDELETIONDATE 	| NUMBER(8)   	|                 	|
| DELAYREASON         	| VARCHAR2(2) 	|                 	|
| DELAYEDDELETIONDATE 	| NUMBER(8)   	|                 	|

### Prm Tables

#### Delay Reasons Prm

{== PRM.PRM_CUST_DD_DELAY_REASONS ==}

| COLUMN              	| DATATYPE    	|
|---------------------	|-------------	|
| BASLANGIC             | CHAR(8)   	|
| BITIS              	| CHAR(8)   	|
| CODE         	        | VARCHAR2(2) 	|
| NAME         	        | VARCHAR2(100) |

Avaliable delay reasons

 * Fraud
 * Sold Loan
 * Collection Case
 * Legal Case
 * Dormant Account

## Destruction Execution Module

{== MMS.DD_DEFINITION ==}


| COLUMN           	| DATATYPE       	| INFO              	|
|------------------	|----------------	|-------------------	|
| OID              	| NUMBER(16)     	|                   	|
| STATUS           	| NUMBER(1)      	|                   	|
| LASTUPDATED      	| NUMBER(15)     	|                   	|
| RETENTION        	| VARCHAR2(5)    	| (2Y  ,10Y)          |
| ENTITY          	| VARCHAR2(5)    	| (CUST , DAP, LAP)   |
| TABLENAME        	| VARCHAR2(100)   	|                   |
| COLUMNS          	| VARCHAR2(1000) 	| (Comma separated) 	|
| SELECTQUERY      	| VARCHAR2(250)  	|                   	|
| DELETEQUERY     	| VARCHAR2(250)  	|                   	|


{== MMS.DD_DELETION_LOG ==}

| COLUMN           	    | DATATYPE       	| INFO              	|
|------------------	    |----------------	|-------------------	|
| OID              	    | NUMBER(16)     	|                   	|
| STATUS           	    | NUMBER(1)      	|                   	|
| LASTUPDATED      	    | NUMBER(15)     	|                   	|
| CUSTOMEROID           | NUMBER(16)    	|                     |
| APPLICANTTYPE         | VARCHAR2(5)   	|      LOAN, DEPT     |
| APPLICANTOID          | NUMBER(16)    	|                   	|
| RETENTION      	      | VARCHAR2(5)  	  |                   	|
| TABLENAME      	      | VARCHAR2(250)  	|                   	|
| DELETEREFERENCE       | VARCHAR2(50)  	|                   	|
| DELETIONDATE     	    | NUMBER(8)  	    |                   	|
| COLUMNS 	            | VARCHAR2(1000)  |                   	|
| DESTRUCTIONQUERYTEXT1 | VARCHAR2(4000)  |                     |
| DESTRUCTIONQUERYTEXT2 | VARCHAR2(4000)  |                     |


{== MMS.DD_DELETION_LOG_BACKUP ==}

| COLUMN           	    | DATATYPE       	| INFO              	|
|------------------	    |----------------	|-------------------	|
| OID              	    | NUMBER(16)     	|                   	|
| STATUS           	    | NUMBER(1)      	|                   	|
| LASTUPDATED      	    | NUMBER(15)     	|                   	|
| DDLOGOID              | NUMBER(16)    	|                       |
| DELETEDTALEOID        | NUMBER(16)    	|                   	|
| COLUMN      	        | VARCHAR2(50)  	|                   	|
| VALUE       	        | VARCHAR2(4000)  	|                   	|
