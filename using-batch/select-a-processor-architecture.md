---
description: Choosing nodes for a job based on the processor micro-architecture.
---

# Select a Processor Architecture

Chinook currently has three types of standard compute nodes with differing Intel [micro-architectures](https://en.wikipedia.org/wiki/List_of_Intel_CPU_microarchitectures). It is possible to limit a job to run on just one or two processor types. This allows a binary built with more advanced [instruction sets](https://en.wikipedia.org/wiki/Category:X86_instructions) to be executed only on processors that support the instruction set. If a binary is not built for a specific instruction set, it will run on any of the three types.

The three micro-architectures which translate to a node type are:

1. [Haswell](https://en.wikipedia.org/wiki/Haswell_%28microarchitecture%29)
2. [Broadwell](https://en.wikipedia.org/wiki/Broadwell_%28microarchitecture%29)
3. [Skylake](https://en.wikipedia.org/wiki/Skylake_%28microarchitecture%29) / [Cascade Lake](https://en.wikipedia.org/wiki/Cascade_Lake_%28microarchitecture%29)

To select a specific node type, use the "--constraint" option of the `sbatch` or `srun` commands. Multiple choices may be specified with the OR operator. 

Example 1, request a job run only on Skylake/Cascade Lake nodes:

```text
sbatch --constraint="Skylake" jobScript.slurm
```

Example 2, request a job run only on Broadwell or Skylake nodes:

```text
sbatch --constraint="Broadwell|Skylake" jobScript.slurm
```

Example 3, request a job run only on a single node type, but either Broadwell or Skylake nodes may be used \(aka matching OR\):

```text
sbatch --constraint="[Broadwell|Skylake]" jobScript.slurm
```

By adding a constraint, the number of possible nodes a job can run on will be reduced. This means it may take more time for the scheduler to make those nodes available and launch the job.

