# Destruction Execution

So we have selected the customers and applicants that should be deleted according to their retention, completed all flows and approvals and finally we are ready to delete the customers.

The approved list is inserted to a BCH table. For every row in the BCH table we check the definition table and get the list of tables to be deleted according to entity and retention.

Suppose that it is a Customer and it is in our radar due to a 10Y retention.

One example definition that matches these conditions would be the following :

RETENTION 	| ENTITY  |  TABLENAME           	| COLUMNS                              	| SELECTQUERY          	|  DELETEQUERY     	|
|-----------	|--------- |---------------------	|--------------------------------------	|----------------------	|	----------------------	|
10Y       	| CUST |MMS.MUSTERI_ADDRESS 	| LOCATIONNAME,ADRESSATIR1,ADRESSATIR2 	| QE_DD_SELECT_ADDRESS 	 	| QE_DD_DELETE_ADDRESS 	|

We will start by executing the select query with providing the customeroid that is coming from BCH table. This query is the select version of delete query.
It will be used to backup the columns that are subject to deletion.

{== QE_DD_SELECT_ADDRESS ==}

``` sql
SELECT
  OID,
  MA.LOCATIONNAME,
  MA.ADRESSATIR1,
  MA.ADRESSATIR2
FROM
  MMS.MUSTERI_ADRES MA
WHERE
   MA.MUSTERIOID = ?;
```

Suppose our select query returned 2 rows . With the information coming from BCH table and the result set of above query we will fill our log and backup table and execute the delete query.

``` sql
UPDATE MMS.MUSTERI_ADRES MA
   SET
   MA.LASTUPDATED = GETLASTUPDATED,
       MA.LOCATIONNAME = NULL,
       MA.CAREOF = NULL,
       MA.FLAT = NULL,
       MA.BUILDING = NULL,
       MA.HOUSE = NULL,
       MA.POSTAKODU = NULL,
       MA.ADRESSATIR1 = NULL,
       MA.ADRESSATIR2 = NULL,
       MA.ADRESSATIR3 = NULL
 WHERE
    MA.MUSTERIOID = ?
    AND exists (select null from MMS.DD_DELETION_LIST l
                   where l.CUSTOMEROID = MA.CUSTOMEROID
                     AND l.status = "APPROVED");
  ```

It will be similar two the following:
