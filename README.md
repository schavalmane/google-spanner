# google-spanner
Migrating from MYSQL to Spanner is a journey and simplifying this migration is key for many organizations . I recently migrated a Large E-Commerce organization to Spanner ( and BigQuery ) and a writeup from my learning 

Spanner : GCP Spanner is google promise of most reliable , high performance reliable system . If you are a high transactional system and does not want to worry about all complexities of managing database then I feel Spanner is your choice .

If you ready to pay the Money then Spanner can 
  1) Provide you a distributed system 
  2) Back and recory ready
  3) tools to monitor 
  4) Good dashboards too see whats going on 

If you are apps owner then I would say this is all you need and it provides that comfort .  Again its your application design that will define scalability not DB alone

Some Considerations :

1) Gooogle has limited data Types and they are still evolving . Be prepared to modify the data Types . Eg : VarChar is all Strings . I feel its the right approach as we don't have to make decisions about what data types instead use these generic ones.
2) Google expects to have a Unique Key for Primary key . This is mainly to help their distribution but not always pssible . eg : Order_ID is primary key of orders table and google expects you to make its some alpha numeric is not going to work . So some suggestions are  good some should be ignored because there are downstream complexities .
3) No Application dependent code in DB .If you have procedures and functions be prepared to move away . The whole idea of stateless design 
4) Its expensive so try to keep transactional tables here and move the large historic tables to data warehouse ( Big Query )
5) Be prepared for your apps to do the type transformation . Also better move away from relatioinal DB design like  foreign key etc


To Migrate you need to do below steps at high level

1) If your column names have spanner reserved keys , modify those in Source DB ( MySQL)
2) Build Table DDL's from Mysql , Transform to Spanner format
3) Create the Tables on SPanner
4) Downlod the Data frm Mysql Into Disk ( cloud ) in AVRO format
5) Build a template for Data Flow Jobs
6) Copy the Avro Files to Google Bucket
7) Load the Data into Google Spanner using Data Flow Jobs
8) Compare the records to make sure you have all the data.


This can be done in parallel . We  moved about 1 TB is less than 2 hrs  and complete processes Automated .

Feel free to leave comments in case you have any questions . 

Thanks
