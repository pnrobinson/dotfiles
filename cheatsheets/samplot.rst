
samplot
#######

`Samplot repo <https://github.com/ryanlayer/samplot>`_


Running

.. code:: bash

  srun --pty --time 01:00:00 --mem 2G bash
  module use /projects/.../software/modules
  module load samplot
  samplot --help
  
  samplot plot -n name1 name2 name3 -b name1.sorted.bam name2.sorted.bam name3.sorted.bam \
   -r GRCh38_primary_assembly_p13.fa -o output.pdf -c CM000681.2 -s 1903000 -e 1911300 -t DEL \
   --dpi 1000 -w 3000 -o TMP.png
  
  
