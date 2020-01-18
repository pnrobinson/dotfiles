==============
awk cheatsheet
==============

Sundry awk one-liners and tips

filter TSV document according to presence of string in specific field
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following command checks the 11th field of a tab-separated document for the string 'core' and prints 
fields 1 and 11 from all matching lines. ::

  awk -F'\t' '$11 ~ "core" {print $1,$11}' hpocitations.txt 

The following command checks whether the 11th field is equivalent to "core". ::

  awk -F'\t' '$11 == "core" {print $1,$11}' hpocitations.txt 
