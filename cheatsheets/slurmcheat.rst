################
SLURM cheatsheat
################



Interactive jobs
^^^^^^^^^^^^^^^^


Running an interactive job is done through the srun command. 

The following allocates 

1.  The -q flag specifies a QOS (quality of service), here ``batch''
2. --pty: pseudo terminal mode
3. -t 15:00: 15 minutes wall time


.. code-block:: bash
  :linenos:

  srun --pty -t 15:00 -q batch bash


Submitting job to cluster
^^^^^^^^^^^^^^^^^^^^^^^^^

The following command gives the foobar script 1 minute to run, 
allocates 1 CPU (-n 1) and 100 megabytes of RAM, and passes 
the arguments 7 and 42


.. code-block:: bash
  :linenos:

  sbatch -t 1:00 -n 1 --mem=100M foobar.sh 7 42


SLURM Options
^^^^^^^^^^^^^
* jobname

By default the name of a job in SLURM is the name of the script. 
This can be changed by specifying -J=[job name].

* output file

This can be specified using the -o option, and various variables are available, e.g.

``-o %u-%x-%j``

* %A Job array's master job allocation number.
* %a Job array ID (index) number.
* %J jobid.stepid of the running job. (e.g. "128.0")
* %j jobid of the running job.
* %N short hostname. This will create a separate IO file per node.
* %n Node identifier relative to current job (e.g. "0" is the first node of the running job) This will create a separate IO file per node.
* %s stepid of the running job.
* %ttask identifier (rank) relative to current job. This will create a separate IO file per task.
* %u User name.
* %x Job name.


Embedding SLURM Options in Scripts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Options can be passed on the command-line or embedded in scripts.

.. code-block:: bash
  :linenos:

  #!/usr/bin/env bash
  #SBATCH -J my_cool_job_name
  #SBATCH -t 1:00
  #SBATCH -n 1
  #SBATCH --mem=100M
  #SBATCH -o %u-%x-%j
  # the rest of the Bash script follows.
  # the script is called as sbatch foobar.sh 1 15