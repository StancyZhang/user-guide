## Managing Jobs
The Slurm job scheduler provides several command-line tools for checking on the status of your jobs and for managing them.

### Checking Job Status
Use the `squeue` (slurm queue) command to check on the status of jobs. Running `squeue` with no flags will show the full queue (all pending and running jobs.)


 
To view only the jobs that you have submitted, use the ```--user``` flag.
```
squeue --user=<CNetID>
```
???+ note
    Any job with 0:00 under the TIME column is still waiting in the queue.

To get information about all jobs that are waiting to run on the bigmem2 partition, enter:
```
squeue --state=PENDING --partition=bigmem2
```

To get information about all your jobs that are running on the bigmem2 partition, type:
```
squeue --state=RUNNING --partition=bigmem2 --user=<CNetID>
```

???+ tip
    You can customize the output of `squeue` and `sacct` by configuring your slurm environment. An example configuration bash file `set_slurm_env.sh` can be found [here](https://github.com/rcc-uchicago/R-large-scale/blob/master/set_slurm_env.sh){:target="_blank"}. With the configuration file in your current directory (and job/s running), simply run:
    ```bash
        source set_slurm_env.sh
        squeue -u cnetid
    ```

For more information, consult the command-line help by typing ```squeue --help```, or visit the [official online documentation](https://slurm.schedmd.com/documentation.html){:target="_blank"}.

### Canceling your jobs
To cancel a job you have submitted, use the ```scancel``` command. This requires you to specify the id of the job you wish to cancel. 

For example, to cancel a job with id 8885128, do the following:
```
scancel 8885128
```
If you are unsure what is the id of the job you would like to cancel, see the JOBID column from running ```squeue --user=<CNetID>```.

To cancel all jobs you have submitted that are either running or waiting in the queue, enter the following:
```
scancel --user=<CNetID>
```

### Monitoring Job Memory
You can monitor your job by connecting to the compute node it is running on via SSH and using the ```htop``` command.

To do this, run the following to see your running jobs and which compute nodes your jobs are running on:
```
squeue --state=RUNNING --user=<CNetID>
```
The last column of the output tells us which nodes are allocated for each job. You can connect to the compute node using the following command, where for example we are connecting to compute node midway2-0172.
```
ssh midway2-0172
```
Finally run:
```
htop
``` 
To view processes running on the node, including your job's process which will be listed under your CNetID in the USER column.
