# Dynamic VM: A middle way between VM and Container

## Introduction 

Container is more lightweight than Virtual Machine(VM). One of the primary reasons is they manage free memory in different ways.

In VM world, Hypervisor is the real manager of physical resources. Each VM has an independent Guest OS to serve applications‘ allocate/free memory request. Currently, a lot if not all of Guest OS’s free memory is reserved rather than shared with other VM(s). That is because frequently talking to Hypervisor cost CPU heavily. On the other hand, Containers are sharing the same OS kernel with Hypervisor, so that they are naturally immune to this problem.

Different from Container, VM can use Guest OS to provide security, variety, failure isolation, but also tons of reserved memory as a cost.

Dynamic VM is a Para-Virtualization solution that allows Guest OS and Hypervisor to manage free memory pages together with little CPU cost. Any page freed to Guest OS can be recycled by Hypervisor in few seconds. A Guest OS can have this power by installing drivers. It is completely transparent to applications. The memory consumption can become rapidly closer to Container without losing merits of VM.

The solution includes two parts:

1.	`PPR` (Per Page Recycler) is based on a lockless recycling algorithm. Hypervisor PPR engine and guest PPR driver work together to reclaim free pages without triggering each other any interrupt.
2.	Because PPR, more VMs could be run in the same amount of physical memory. Moreover, they may produce more same-content pages. The benefit can be weakened if the page deduplication engine was overwhelmed. `PageONE` is a dedup-engine based on lockless tree algorithm. Any CPU can donate its spare time for more dedup power

Dynamic VM is a power up that can be easily ported to different OS architectures. Currently, the Hypervisor engine supports Linux KVM and the guest driver supports Linux and Windows.

Among resources of VMs, CPU and Ethernet are used dynamically all the way. The only thing had a “STATIC” flavor is memory. Removed this special case VMs become fully resources dynamic. Therefore, VMs can be deployed and billed according to real-time resources consumption. Softened VMs can make cloud more flow-able.

A detailed description and test report of both technologies could be found here.
        [PPR DESCRIPTION](https://github.com/lijiyong0303/test_readme/blob/master/ppr_info.txt)
        [PageONE DESCRIPTION](https://github.com/lijiyong0303/test_readme/blob/master/pageone_info.txt)
## Author
`Baiban_tech`:Hypervisor technologies. We believe cloud can behave quite differently as new resources manage methods applied.
Email us at <a href="mailto:dynamic@baibantech.com.cn">dynamic@baibantech.com.cn</a>
