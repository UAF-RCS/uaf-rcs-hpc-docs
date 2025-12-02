# Available Partitions

| Name | Node Count | Max Walltime | Nodes | Other rules | Purpose |
| :--- | :--- | :--- | :--- | :--- | :--- |
| debug | 2 | 1 hour | 1-2 |  | For debugging and trying job scripts |
| t1small | 123 | 2 days | 1-2 |  | For shorter, smaller jobs with quick turnover |
| t1standard | 123 | 4 days | 3+ | Default, always uses 3 nodes. If you need less than 3 nodes use the small partitions. | General-purpose partition |
| t2small | 123 | 4 days | 1-2 | [Tier 2](../community-condo-model/community-condo-model.md#tier2) users only. Increased priority and walltime. | Tier 2 version of t1small |
| t2standard | 123 | 7 days | 3+ | [Tier 2](../community-condo-model/community-condo-model.md#tier2) users only. Increased priority and walltime. | Tier 2 version of t1standard |

| Name | Node Count | Max Walltime | Cores | Other Rules | Purpose |
| :--- | :--- | :--- | :--- | :--- | :--- |
| analysis | 3 BigMem | 4 days | 1-7 | Shared node | For serial pre- and post-processing |
| bio | 3 BigMem | 14 days | 1-7 | Shared node | For high memory, low CPU jobs |
| transfer | 1 | 1 day | 1 | Shared node | Copy files between archival storage and scratch space |

Selecting a partition is done by adding a directive to the job submission script such as `#SBATCH --partition=t1standard`, or on the command line: `$ sbatch -p t1standard`

**Please note**: When running a job in the analysis or bio partition the --mem SBATCH directive **must** be set as to not affect other users' work. Adding: `#SBATCH --mem=214G` is the RCS recommendation

Anyone interested in gaining access to the higher-priority [Tier 2](../community-condo-model/community-condo-model.md#tier2) partitions \(t2small, t2standard\) by subscribing to support the cluster or procuring additional compute capacity should contact [uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu).

