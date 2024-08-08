# Available Partitions

| Name | Nodecount | Max walltime | Nodes/Threads per job \(min-max\) | Other rules | Purpose |
| :--- | :--- | :--- | :--- | :--- | :--- |
| debug | 2 | 1 hour | 1-2 nodes |  | For debugging job scripts |
| t1small | 118 | 2 days | 1-2 nodes |  | For short, small jobs with quick turnover |
| t1standard | 118 | 4 days | 3-48 threads | Default | General-purpose partition |
| t2small | 118 | 4 days | 1-2 threads | [Tier 2](../community-condo-model/community-condo-model.md#tier2) users only. Increased priority and walltime. | Tier 2 version of t1small |
| t2standard | 118 | 7 days | 3-48 threads | [Tier 2](../community-condo-model/community-condo-model.md#tier2) users only. Increased priority and walltime. | Tier 2 general-purpose partition |
| gpu | 2 | 2 days | 1-2 nodes | | For jobs using the GPUs |
| bio | 3 BigMem | 14 days | 1-7 threads per job |  | For high memory, low CPU jobs |
| analysis | 3 BigMem | 4 days | 1-7 threads per job |  | For serial, post-processing and data analysis |
| transfer | 1 | 1 day | 1 node | Shared use | Copy files between archival storage and scratch space |

Selecting a partition is done by adding a directive to the job submission script such as `#SBATCH --partition=t1standard`, or on the command line: `$ sbatch -p t1standard`

**Please note**: When running a job in the analysis or bio partition the --mem SBATCH directive **must** be set as to not affect other users' work. Adding: `#SBATCH --mem=214G` is the RCS recommendation

Anyone interested in gaining access to the higher-priority [Tier 2](../community-condo-model/community-condo-model.md#tier2) partitions \(t2small, t2standard\) by subscribing to support the cluster or procuring additional compute capacity should contact [uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu).

