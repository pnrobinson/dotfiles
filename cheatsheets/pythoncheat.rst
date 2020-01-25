#################
Python cheatsheat
#################

Unit tests
~~~~~~~~~~

nosetests tests/

pydoc
~~~~~
Use to show/search/create documentation

  .. code-block:: python
  $ python -m pydoc   # show features of pydoc
  $ python -m pydoc -k sql # search all installed modules for 'sql'
  $ sudo python -m pydoc -p 3212  # start documentation browser on port 3212 (quit with q/ctrl-C)
    (...) 
    pydoc server ready at http://localhost:3212/
  $ python -m pydoc -w filename # create html documentation for filename.py 

pydoc must be able to find the file to create documentation. Options include starting the command in the same directory.
