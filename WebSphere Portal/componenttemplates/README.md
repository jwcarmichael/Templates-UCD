Example UrbanCode Deploy Component templates automating some of the typical tasks generated by the [Portal Configuration Wizard] (http://www.ibm.com/support/knowledgecenter/SSYJ99_8.5.0/config/cw_overview.html). Created on a Centos 7 x64 test bed so there are some Centos specific commands used.

Initial templates cater to the following scenrarios:
1. Database Transfer from Derby to DB2
2. Create a Cluster with remote Deployment Manager and node 

Be sure to go thorugh and check the component/environment/resource properties.

## Brief Description of Component Template Processes
1. **Portal+Configuration+Wizard_templ**
  - **Add Additional node to cluster with DB2 drivers**
    Run on an additional node after installing Portal Binaries only. Upload profileTemplates.zip (from a Portal installation), db2jcc4.jar, db2jcc_license_cu.jar to a version of this component

  - **Augment Deployment Manager for Portal**
    Run on Dmgr Server - adds Portal files to the DEployment Manager. Upload the filesForDmgr.zip from the Primary node to a version of this component
    
  - **Create a Cluster**
    Run on first portal server. Federate the node. This node then becomes a managed node in the deployment manager cell.

  - **Database Transfer DB2 Same Server**
Executes all the Database Transfer steps when Portal and DB2 on same server

  - **Database Transfer remote DB2 01 Setup DB2 JDBC jars backup-property-files-for-dbxfer**
Run on portal server. Setup DB2 JDBC jars and backup-property-files-for-dbxfer

  - **Database Transfer remote DB2 02 setup-database**
Run on portal server. setup-database. Db2 must be restarted after this step.

  - **Database Transfer remote DB2 03 validate transfer grant LOB
Run on Portal Server: validate database , transfer database , grant privileges, setup DB2 LOB

2. **Portal+Configuration+Wizard+DB_templ**
  - **Database Transfer DB2 01 Create users groups and database**
Run on DB2 Server. Creates Portal Groups for DB2 and createes DB2 database for portal. Needs DB2 user set in environment/wcm.DbUser password in environment/wcm.DbUser and environment/wcm.DbPassword environment/wcm.DbName
  - **Database Transfer DB2 02 Restart DB2**
Run on DB2 server. Restarts DB2
