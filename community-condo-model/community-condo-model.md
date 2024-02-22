# Community Condo Model

Chinook is a community, condo model high performance computing \(HPC\) cluster. Common infrastructure elements such as the environmentally regulated data center, network connectivity, equipment racks, management and technical staff, and a small amount of CPUs provide subsidized resources to PIs that they may not be able to procure individually, and allows them to focus time and energy on research, rather than owning and operating individual clusters.

Participants in the condo service share unused portions or elements of the computational resources they add to Chinook with each other and non-invested users - such as students or occasional users - who may or may not pay a fee for access. A queue management system gives vested PIs top priority to the share he/she has purchased whenever the PI needs the resource. RCS also reserves the option to use manual or automated job preemption to interrupt community user jobs as needed to give vested PIs access to their share.

### Tier 1: Community Nodes <a id="tier1"></a>

This level of service is open to the UA research community using nodes procured for the community and unused portions of shareholder nodes. Users in this tier receive:

* Unlimited total compute node CPU hours
* Lower initial job priority
* 50 GB [$HOME](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/filesystems#home) quota 
* 1 TB per project shared Lustre storage quota \($CENTER1, unpurged\)
* Access to job queues with limited wall time
* Standard user support \(account questions, software requests, short job debugging and diagnosis assistance, ...\)

### Tier 2: Shareholder Shared Nodes <a id="tier2"></a>

This level of service is for the PI or project that requires CPUs beyond what can be offered by Tier 1 or requires priority access to HPC resources. Users in this tier are shareholders that procure equipment or support and receive:

* Unlimited total compute node CPU hours
* Higher initial job priority, weighted by number of shares procured
* 50 GB [$HOME](../available-filesystems/available-filesystems.md#home) quota 
* 1 TB + 1 TB/node project shared Lustre storage quota \($CENTER1, unpurged\)
* Access to job queues with limited wall times greater than Tier 1
* Short term reservations \(contact [uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu) to arrange\)
* Higher priority given to user support requests

### Tier 3: Shareholder Dedicated Nodes <a id="tier3"></a>

This level of service is for the PI or project that requires dedicated resources. RCS will manage and operate procured nodes for an additional service fee. Users interested in this level of service should contact RCS.

* Limited CPU to procured nodes and infrastructure components
* Limited Lustre \(equal to Tier 1 unless additional capacity procured by PI/project\) + DataDir storage \(pending\)
* No priority or preemption rights to Tier 1 or Tier 2
* Dedicated queue\(s\) with unlimited wall times

### Purchasing Chinook Shares <a id="purchase"></a>

Please contact RCS \([uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu)\) if you are interested in purchasing compute nodes or support and becoming a tier 2 or 3 shareholder. All node types include licenses for Scyld ClusterWare, Mellanox UFM, and Linux with a minimum 3-year service contract. The purchase price provides shares in Chinook that align with the warranty of the equipment purchased. When shares expire, the resources must be upgraded or the warranty must be renewed, otherwise the resources revert to the community pool and the project will be given a Tier 1 status.

For pricing see the [RCS Rates page](https://www.gi.alaska.edu/research-computing-systems/service-rates#chinook-shares)

### Lifecycle Management <a id="lifecycle"></a>

All compute nodes include factory support for the duration of the warranty period. During this time any hardware problems will be corrected as soon as possible. After the warranty expires, compute nodes will be supported on a best-effort basis until they suffer complete failure, are replaced, or reach a service age of 5 years. Once a node has reached end-of-life due to failure or obsolescence, it will be removed from service.

