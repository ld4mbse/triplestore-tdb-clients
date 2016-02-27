#Automatic syncing of data between Subversion, OSLC adapters and RDF triplestore





##Instructions to demo syncing scenario 

Last updated by Axel Reichwein (axel.reichwein@koneksys.com) 				February 26, 2016



### 1. Before the demo

1. In Windows Explorer, perform a checkout operation of the MagicDraw repository using Tortoise.
2. In MagicDraw: Open MagicDraw model named Wired_Camera_Example  from the local working directory which was just checked out
3. In Eclipse: Launch MagicDraw adapter (Maven configuration named oslc adapter for magicDraw tomcat run)
4. In Eclipse: Launch Simulink adapter (Maven configuration named oslc adapter for simulink)
5. In Eclipse: Launch AMESim adapter (Maven configuration named oslc4jamesim-wink tomcat run)
6. In Eclipse: In project triplestore in package tdb.clients.sync.magicdraw.withrevision, run Java application **MagicDrawAdapterAndTDBSubversionSyncClientWithRevision.java**
7. In Browser: have tabs already open with following URLs

-	[http://localhost:8080/oslc4jmagicdraw/services/svnfilepublisher](http://localhost:8080/oslc4jmagicdraw/services/svnfilepublisher)
-	[http://localhost:8181/oslc4jsimulink/services/svnfilepublisher](http://localhost:8181/oslc4jsimulink/services/svnfilepublisher)
-	[http://localhost:8282/oslc4jamesim/services/svnfilepublisher](http://localhost:8282/oslc4jamesim/services/svnfilepublisher)
-	[http://localhost:8080/oslc4jmagicdraw/services/catalog/singleton](http://localhost:8080/oslc4jmagicdraw/services/catalog/singleton) 
-	[http://localhost:8181/oslc4jsimulink/services/catalog/singleton](http://localhost:8181/oslc4jsimulink/services/catalog/singleton) 
-	[http://localhost:8282/oslc4jamesim/services/catalog/singleton](http://localhost:8282/oslc4jamesim/services/catalog/singleton) 
-	postman client already with prerecorded request (in the history tab) for MagicDraw value property resource with Accept header equal to application/rdf+xmlRDF/XML and same request but with Accept header equal to application/json


### 2. Start the demo

####Demo OSLC adapters supporting Subversion

1. In Browser: Show Subversion repository with MagicDraw files. Example: https://koneksys1:18080/svn/repository3/
2. In Browser: Show revision of Subversion repository containing Magicdraw files
3. In Browser: Show MagicDraw files published by MagicDraw adapter [http://localhost:8080/oslc4jmagicdraw/services/subversionfiles](http://localhost:8080/oslc4jmagicdraw/services/subversionfiles) 
4. In Browser: Show revision of a specific MagicDraw file published by MagicDraw adapter. Example:  http://localhost:8080/oslc4jmagicdraw/services/subversionfiles/httpskoneksys118080svnmagicdrawrepository---Wired_Camera_Example.mdzip 
5. In MagicDraw: show value of a MagicDraw value property
6. In Browser: show how you browse from OSLC Service Provider Catalog to a specific MagicDraw value property 
7. In Browser: show value of MagicDraw value property as OSLC resource in HTML format 
8. In Browser: show with postman rest client value of MagicDraw value property as OSLC resource in RDF/XML and JSON
9. In Eclipse: In project triplestore, explain that your local triplestore (RDF database) is saved in the folder **mytriplestore** and that it can be queried using SPARQL, which is similar to SQL. Explain that the triplestore has been populated with the resources from the running OSLC adapter (step #6 in last section). Explain that you will perform a SPARQL query to retrieve the MagicDraw value property saved in the triplestore
10.	In Eclipse: In project triplestore in package tdb.clients.sync.magicdraw.withrevision, run Java application **QueryTriplestoreForMagicDrawValuePropertyOfSpecificModelWithRevision.java**
11.	and show value of MagicDraw value property saved in the triplestore in the Eclipse console window. 


####Demo automatic syncing between Subversion, adapters and triplestore

1. In MagicDraw: change value of MagicDraw value property
2. With your SVN client, perform a commit operation. Wait for logging statement indicating correct commit operation. If you do not have a SVN commit client, update and run the Java application **MagicDrawCommitClient.java** located in the edu.gatech.mbsec.subversion.client project of the subversion-client repository.
3. In Browser: Show Subversion repository with MagicDraw files. Example: https://koneksys1:18080/svn/repository3/
4. In Browser: Show revision of Subversion repository containing Magicdraw files. Revision number should be +1
5. Wait for MagicDraw adapter to finish reloading files from Subversion server
6. In Browser: Show revision of specific MagicDraw file published by MagicDraw adapter. Example:  http://localhost:8080/oslc4jmagicdraw/services/subversionfiles/httpskoneksys118080svnmagicdrawrepository---Wired_Camera_Example.mdzip 
7. In Browser: show updated value of MagicDraw value property as OSLC resource in HTML format 
8. In Browser: show with postman rest client value of MagicDraw value property as OSLC resource in RDF/XML and JSON
9. In Eclipse: In project triplestore in package tdb.clients.sync.magicdraw.withrevision, run Java application **QueryTriplestoreForMagicDrawValuePropertyOfSpecificModelWithRevision.java**
and show value of MagicDraw value properties saved in the triplestore. 
10.	In Eclipse: In project triplestore, run batch file named run **fuseki.bat**
11.	In browser, go to page [http://localhost:3030/](http://localhost:3030/) 
12.	In Eclipse: In project triplestore, copy SPARQL query located in file get SysML value properties.txt in the folder example sparql queries
13.	In browser, at page [http://localhost:3030/](http://localhost:3030/), go to Query and enter SPARQL query text, and click on play. Query results will display MagicDraw SysML value properties saved in triplestore having different revision numbers and values
14.	In Eclipse: In project triplestore, copy SPARQL query located in file get all sysml blocks.txt in the folder example sparql queries
15.	In browser, at page [http://localhost:3030/](http://localhost:3030/), go to Query and enter SPARQL query text, and click on play. Query results will display all MagicDraw SysML blocks saved in triplestore having different revision numbers 


Note: after launching Fuseki, you can no longer perform SPARQL queries against the triplestore using the Java API. Every interaction with the triplestore has to go through the SPARQL HTTP endpoint of Fuseki. 


#RDF Triplestore and SPARQL HTTP endpoint

##Instructions to install and run RDF triplestore and  SPARQL HTTP endpoint


###1.	Downloading the triplestore-tdb-clients repository

1. Open the Git Repositories View (Window -> Show View -> type “Git Repositories” in the search field)
2. Click on the Clone Repository icon  
3. In the URI field, paste the following URL: https://github.com/ld4mbse/triplestore-tdb-clients.git
4. The Host and Repository fields will autofill.
5. Click Next, only select the master branch
6. Click Next until Finish.

###2.	Importing the triplestore project into the Eclipse workspace

1. In the Git repositories view, right-click triplestore and select “Import Projects”. Click Next until Finish. The triplestore project will be in the Eclipse workspace.
2. In Eclipse, open the Project Explorer view. (Window → Show View → Project Explorer)
3. Expand the triplestore project
4. Right click pom.xml -> Run As -> Maven clean
5. Right click pom.xml -> Run As -> Maven install 
6.	If there is a red error mark next to the triplestore project, select the project. Right-click->Maven->Update Project… and click OK 

###3.	Configuring triplestore location

1. In Eclipse, open the Project Explorer view. (Window → Show View → Project Explorer). By default, it is already visible at the left of the screen.
2. Select the just created triplestore project and expand it
3. Choose an empty folder as triplestore location, such as the mytriplestore folder located in the Eclipse triplestore project. Your user account needs to have read/write permission to that folder. 
4. In the Project Explorer view, expand the triplestore Eclipse project, and expand the triplestore configuration folder
5. Open the config.properties file 
6. Specify the location of the triplestore without trailing slash at the end, for example
 ```text
triplestoreDirectory = C:/Users/Axel/git/triplestore/triplestore/mytriplestore
```

###4.	Creating triplestore 

1. In Eclipse, open the Project Explorer view. (Window → Show View → Project Explorer)
2. Expand the triplestore project
3. Expand the src/main/java folder
4. Expand the tbd.clients package
5. Right click **CreateTriplestore.java** -> Run As -> Java Application
6. In the console view, you should see the statement “Triplestore created”
7. To manually verify that the triplestore was created, you can notice the addition of new files in your triplestore folder. If you are verifying the triplestore folder content in the Eclipse Project Explorer view, you may need to right-click on your triplestore folder, and click on Refresh before verifying its content. 
8. If you decide to later delete the triplestore and start from scratch, one option is to delete all the files in your triplestore folder and start off with a new empty triplestore folder. 

###5.	Populating triplestore with Simulink Blocks

1. In Eclipse, open the Project Explorer view. (Window → Show View → Project Explorer)
2. Expand the triplestore project
3. Expand the src/main/java folder
4. 2 Options
  1. Option A: Populate triplestore with Simulink Blocks described as RDF on file (no need to run Simulink adapter)
    1. Expand the tbd.clients package
    2. Right click PopulateTriplestoreWithSimulinkBlocksAsRDF.java-> Run As -> Java Application (the sample RDF file is located in the     folder named sample rdf)
  2. Option B: Populate triplestore with Simulink Blocks from running adapter 
    1. Run the OSLC Simulink Adapter as described in the “Instructions to install and run the OSLC Simulink Adapter”
    2. 2 Options
    3. Option B1: Retrieve Simulink Blocks from adapter and save them on file in RDF, and then populate triplestore based on RDF document 
      1.	Expand the adapter.clients package
      2.	Right click GETSimulinkBlocksAndSaveAsRDF.java.java-> Run As -> Java Application
      3.	In the console view, you should see the statement “Simulink blocks from adapter saved as RDF on file”
      4.	Expand the tdb.clients package
      5.	Right click PopulateTriplestoreWithSimulinkBlocksAsRDF.java-> Run As -> Java Application
    2.	Option B2: Retrieve Simulink Blocks from adapter and directly populate triplestore based on in-memory POJOs
      1.	Expand the tdb.clients package
      2.	Right click GETSimulinkBlocksAndPopulateTriplestoreWithPOJOs.java-> Run As -> Java Application
      2.	In the console view, you should see the statement “Simulink Blocks added to triplestore”

Warning: if you try to populate the triplestore using the TDB API while Fuseki is running, you will get the following exception:
Exception in thread "main" com.hp.hpl.jena.tdb.TDBException: Can't open database at location ... as it is already locked by the process with PID 7388.  TDB databases do not permit concurrent usage across JVMs so in order to prevent possible data corruption you cannot open this location from the JVM that does not own the lock for the dataset

Note: If Fuseki is running, you can only populate the triplestore through Fuseki.