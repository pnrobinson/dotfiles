============
synthea2OMOP
============

Set up an OMOP database with synthetic data and analyze it using postgreSQL.


synthea
=======

`synthea <https://github.com/synthetichealth/synthea/>`_ is a Synthetic Patient Population Simulator. Download the executable JAR file `synthea-with-dependencies.jar <https://github.com/synthetichealth/synthea/releases/download/master-branch-latest/synthea-with-dependencies.jar>`_ and run it as follows

.. code-block::
   
     java -jar synthea-with-dependencies.jar -p 1000 --exporter.csv.export true

This outputs a file called ``output`` (we will need the path to the directory below).

By default, it outputs FHIR and so the ``--exporter.csv.export true`` option is used to prepare data we can import to postgreSQL. The ``-p`` option controls the number of generated patients.

Downloading the OMOP CDM data
=============================

Go to the `Athena <https://athena.ohdsi.org> site, register if necessary, and download the complete vocabulary (the server will ask you for a name for the downloaded data, enter omop5 - and download version 5). Note that Athena will send a download link to the email with which you registered.
This will download a file like ``vocabulary_download_v5_{4a96d00f-19ba-43d9-bdb1-e260d7f8c8df}_1636473814003.zip``
Unzipping this (which occurs in the same directory) produces CSVs of the CMD.


Install R package with OMOP common data model
=============================================


.. code-block::
   
   devtools::install_github("OHDSI/CommonDataModel", "v5.4")



Install postgreSQL
==================

We will set up a postgreSQL server to hold the data. First install the following packages. ::

   sudo apt-get install postgresql-12 
   sudo apt-get install postgresql-client-12

To install the pgadmin tool for working with posgreSQL, enter the following commands. ::

   curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add -
   sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/focal pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list' 
   sudo apt update
   sudo apt install pgadmin4

On my system, pgadmin4 did not get installed into PATH, but was available here. ::

   /usr/pgadmin4/bin/pgadmin4


Set up the schema/database for synthea
======================================

Start pgadmin4. Create a new server with name ``synthea10`` and set the server to ``localhost`` and keep the port 5432. You will need to enter the posgreSQL admin password for this step.


Import CSV data as OMOP
=======================

We do this step with the `ETL-Synthea <https://github.com/OHDSI/ETL-Synthea>`_ project. We follow the step-by-step example shown there (and R script) and need to set the following variables:

- syntheaFileLoc <- "/../csv" (path to the CSV file directory created by ``synthea-with-dependencies.jar``)
- vocabFileLoc   <- "/../omop5" (path to the downloaded OMOP CDM data from above)
- posgreSQL user name and password.


Note to install the package, you probably need to perform the following as sudo.

.. code-block::

   install.packages("devtools")
   devtools::install_github("OHDSI/ETL-Synthea")
   
If you get this error when installing the second package: ``configure: error: Java interpreter '/usr/lib/jvm/default-java/bin/java' does not work``, then run this command and try again.

.. code-block::

   sudo R CMD javareconf
   
When you run the R script, start with the following.
   
.. code-block::
   
     library(ETLSyntheaBuilder)
     cd <- DatabaseConnector::createConnectionDetails(
         dbms     = "postgresql", 
         server   = "localhost/synthea10", 
         user     = "postgres", 
         password = "lollipop", 
         port     = 5432
     )
      
This may lead to an error message, Error: The folder location pathToDriver = '' does not exist.Please set the folder to the location containing the JDBC driver.You can download most drivers using the `downloadJdbcDrivers()` function. If so, enter the following (adjust the path as needed).
  
.. code-block::
 
   downloadJdbcDrivers(pathToDriver='/home/user/path/', dbms='postgresql')
   
  
 This will download a file like ``postgresql-42.2.18.jar``.  Now adjust the previous code block as follows (note: the path is to the directory that contains the ``postgresql-42.2.18.jar`` file).
  
.. code-block::
 
  cd <- DatabaseConnector::createConnectionDetails(
      dbms     = "postgresql", 
      server   = "localhost/synthea10", 
      user     = "postgres", 
      password = "lollipop", 
      port     = 5432,
      pathToDriver = "/home/user/path/"
  )
  
This should not work with no errors.
Enter the following lines, but adjust the paths as described above.
  
.. code-block::  

   cdmSchema      <- "cdm_synthea10"
   cdmVersion     <- "5.4"
   syntheaVersion <- "2.7.0"
   syntheaSchema  <- "native"
   syntheaFileLoc <- "/tmp/synthea/output/csv"
   vocabFileLoc   <- "/tmp/Vocabulary_20181119"
 
 
The next command gives an error
 
 .. code-block::  
   ETLSyntheaBuilder::CreateCDMTables(connectionDetails = cd, cdmSchema = cdmSchema, cdmVersion = cdmVersion)
   Error in loadNamespace(x) : there is no package called ‘CommonDataModel’
   
Do we need to install something like this? https://github.com/OHDSI/CommonDataModel



