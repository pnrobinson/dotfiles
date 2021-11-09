============
synthea2OMOP
============

Set up an OMOP database with synthetic data and analyze it using postgreSQL.


synthea
=======

`synthea <https://github.com/synthetichealth/synthea/>`_ is a Synthetic Patient Population Simulator. Download the executable JAR file `synthea-with-dependencies.jar <https://github.com/synthetichealth/synthea/releases/download/master-branch-latest/synthea-with-dependencies.jar>`_ and run it as follows

.. code-block::
  :caption: Generate synthetic patient data with CSV output
  
  java -jar synthea-with-dependencies.jar -p 1000 --exporter.csv.export true


By default, it outputs FHIR and so the ``--exporter.csv.export true`` option is used to prepare data we can import to postgreSQL.
