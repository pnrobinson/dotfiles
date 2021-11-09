============
synthea2OMOP
============

Set up an OMOP database with synthetic data and analyze it using postgreSQL.


synthea
=======

`synthea <https://github.com/synthetichealth/synthea/>`_ is a Synthetic Patient Population Simulator. Download the executable JAR file `synthea-with-dependencies.jar <https://github.com/synthetichealth/synthea/releases/download/master-branch-latest/synthea-with-dependencies.jar>`_ and run it as follows

.. code-block::
   
     java -jar synthea-with-dependencies.jar -p 1000 --exporter.csv.export true


By default, it outputs FHIR and so the ``--exporter.csv.export true`` option is used to prepare data we can import to postgreSQL. The ``-p`` option controls the number of generated patients.

Downloading the OMOP CDM data
=============================

Go to the `Athena <https://athena.ohdsi.org> site, register if necessary, and download the complete vocabulary (the server will ask you for a name for the downloaded data, enter omop5 - and download version 5). Note that Athena will send a download link to the email with which you registered.


postgreSQL
==========

We will set up a postgreSQL server to hold the data.

