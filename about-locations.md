---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-13"

keywords: satellite, hybrid, multicloud, location, locations, control plane

subcollection: satellite

---

{{site.data.keyword.attribute-definition-list}}


# Understanding Satellite locations
{: #about-locations}

A location in {{site.data.keyword.satellitelong}} is a representation of an environment in your infrastructure provider, such as an on-prem data center or public cloud, that you want to bring {{site.data.keyword.cloud_notm}} services to so that you can run workloads in your own environment. You create the location by attaching host machines from across at least 3 zones in your infrastructure. 
{: shortdesc}

To set up a Satellite location, you must first create the location, attach hosts to it, and then create the location control plane. 

In order to use [Red Hat CoreOS (RHCOS)](/docs/satellite?topic=satellite-infrastructure-plan#infras-plan-os) for a maanged service such as worker nodes, you must enable it in your location. You can only enable new locations for RHCOS; you cannot migrate an existing location. For more information, see [Creating a location](/docs/satellite?topic=satellite-locations). Red Hat CoreOS is available only in the `us-south` and `eu-de` regions and for only {{site.data.keyword.redhat_openshift_notm}} version 4.9 and 4.10. Want to verify if your location is enabled for Red Hat CoreOS? See [Is my location enabled for Red Hat CoreOS?](/docs/satellite?topic=satellite-locations#verify-coreos-location).
{: note}

## Satellite location control plane
{: #loc-control-plane}

The location control plane runs resources that are managed by Satellite to help manage the hosts, clusters, and other resources that you attach to the location.

When you set up the {{site.data.keyword.satelliteshort}} location control plane, keep in mind the following host considerations.	

- Hosts must meet the [minimum requirements](/docs/satellite?topic=satellite-host-reqs). For more information about how to configure hosts in other cloud providers to meet these minimum requirements, see [Cloud infrastructure providers](/docs/satellite?topic=satellite-locations).	
- Your host infrastructure setup must have a low latency connection of less than or equal to 100 milliseconds (`<= 100ms`) round-trip time (RTT) between the hosts that are used for the {{site.data.keyword.satelliteshort}} location control plane worker nodes and the hosts that are used for other resources in the location, like clusters or [{{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} service](/docs/satellite?topic=satellite-managed-services). For example, in cloud providers such as AWS, this setup typically means that all the hosts in the {{site.data.keyword.satelliteshort}} location are from the same cloud region, like `us-east-1`. As latency increases, you might see impacts to performance, including provisioning and recovery times, reduced worker nodes in the cluster, [{{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} service](/docs/satellite?topic=satellite-managed-services) degradation, and in extreme cases, failures in your cluster applications.	
- Plan to keep **at least 3 extra hosts** attached and unassigned to your location. When you have extra hosts, then {{site.data.keyword.IBM_notm}} can automatically assign hosts when clusters or the {{site.data.keyword.satelliteshort}} location control plane request more capacity.

{{site.data.keyword.satelliteshort}} uses {{site.data.keyword.cos_short}} to store data about your location and backups for your location's clusters. You can choose to have a bucket created automatically when you create your location or specify an existing bucket. If you want to use an existing bucket, it must have cross-regional resiliency.

## Sizing your {{site.data.keyword.satelliteshort}} location
{: #location-sizing}

Because your {{site.data.keyword.satelliteshort}} location represents your own data center and infrastructure resources, the size of the location can be flexible according to what you want. You are not limited in the number of hosts that you attach to a location. However, as you plan your {{site.data.keyword.satelliteshort}} strategy, keep in mind the following sizing considerations.
{: shortdesc}

1. Set up a highly available {{site.data.keyword.satelliteshort}} location control plane with enough compute capacity to manage the resources in your {{site.data.keyword.satelliteshort}} location.
    Minimum size
    :    To get started, you must attach and assign hosts that meet the [minimum requirements](/docs/satellite?topic=satellite-host-reqs). For testing purposes such as a proof of concept, you can have a minimum of 3 hosts assigned to the control plane, but for production purposes, you must have a minimum of 6 hosts. As you continue to use your location, [you might need to scale the {{site.data.keyword.satelliteshort}} location control plane](#control-plane-attach-capacity) in multiples of 3, such as 6, 9, or 12 hosts.
    
    High availability
    :    When you assign hosts to the {{site.data.keyword.satelliteshort}} location control plane, assign the hosts evenly across each of the 3 available zones of your {{site.data.keyword.cloud_notm}} multizone metro that you selected during location creation. To make the control plane highly available, make sure that the underlying hosts are in separate zones in your physical infrastructure environment. For example, you might assign 2 hosts each that run in 3 separate availability zones in your cloud provider, or that run in 3 separate physical systems in your own data center. You do not have to meet specific requirements for a "zone," but the separate zones must provide availability for system maintenance operations. For example, if 1 zone becomes unavailable due to a failure, or if 1 host becomes unavailable due to updating, the remaining 2 zones are still available to run control plane operations. A poor high availability setup is 2 hosts that are virtual machines on the same hypervisor, because servicing the underlying hardware such as to update the machine would make both hosts become unavailable. For more information, see [High availability for {{site.data.keyword.satellitelong_notm}}](/docs/satellite?topic=satellite-ha).
    
    Compute capacity
    :    {{site.data.keyword.satelliteshort}} monitors the available compute capacity of your location. When the location reaches 70% capacity, you see a warning status to notify you to attach more hosts to the location. If the location reaches 80% capacity, the status changes to **critical** and you see another warning that tells you to attach more hosts to the location.
    
2. Plan to keep **at least 3 extra hosts** attached and unassigned to your location. When you have extra hosts, then {{site.data.keyword.IBM_notm}} can assign the hosts to your {{site.data.keyword.satelliteshort}} location control plane automatically when the location reaches the warning capacity threshold or an unhealthy host needs to be replaced.

3. To decide on the size and number of hosts to attach to your clusters, consider the workloads that you want to run in the location. Review the [{{site.data.keyword.openshiftlong_notm}} documentation](/docs/openshift?topic=openshift-strategy#sizing) for guidance about the following considerations:
    - How many resources does my app require?
    - What else besides my app might use resources in the cluster?
    - What type of availability do I want my workload to have?
    - How many worker nodes (hosts) do I need to handle my workload?
    - How do I monitor resource usage and capacity in my cluster?
    
## How do I know when to attach capacity to the {{site.data.keyword.satelliteshort}} location control plane?
{: #control-plane-attach-capacity}

When you list locations, such as with the `ibmcloud sat location ls` command or in the [{{site.data.keyword.satelliteshort}} console](https://cloud.ibm.com/satellite/locations){: external}, the location enters an `Action required` health state. You see warning messages similar to the following example.

```sh
Hosts in the location control plane are running out of disk space.

Hosts in the location control plane have critical CPU or memory usage issues.

The location control plane is running at max capacity and cannot support any more workloads.
```
{: screen}

## How do I scale up my {{site.data.keyword.satelliteshort}} location control plane to be highly available?
{: #control-plane-scale-up}

See [Highly available control plane worker setup](/docs/satellite?topic=satellite-ha#satellite-ha-setup). Make sure to attach hosts to the control plane location in each zone, in multiples of three. For example, you might have 6 hosts that are assigned to your control plane location that is managed from the {{site.data.keyword.cloud_notm}} `wdc` region, with 2 hosts each zone (`us-east-1`, `us-east-2`, and `us-east-3`).

To scale up your control plane, you can follow the same steps to [Set up the {{site.data.keyword.satelliteshort}} location control plane](/docs/satellite?topic=satellite-locations#setup-control-plane).

## How many {{site.data.keyword.openshiftlong_notm}} clusters can I run before I need to attach capacity to the location control plane?
{: #control-plane-how-many-clusters}

The number of clusters depends on the size of your clusters and the size of the hosts that you use for the {{site.data.keyword.satelliteshort}} location control plane. You must scale up the control plane hosts in multiples of 3, such as 6, 9, or 12.

The following tables provide examples of the number of hosts that the control plane must have to run the masters for various combinations of clusters and worker nodes, for informational purposes only. 

- The size of the hosts that run the control plane, **4 vCPU and 16GB RAM** or **16 vCPU and 64GB RAM**, affect the numbers of clusters and worker nodes that are possible in the location. Keep in mind that actual performance requirements depend on many factors, such as the underlying CPU performance and control plane usage by the applications that run in the location.
- You can assign hosts to the control plane in groups of 3. The table presents examples up to 12 hosts as common configurations to give you an idea of how you might size the control plane for your host and application environment. Note that you can add more than 12 hosts to your control plane in groups of 3. For example you might create a control plane with 18 or 27 hosts.

 Note that while you can deploy a cluster to a location with only 3 control plane hosts, upgrading and other management operations might not work with bare minimum setups.
 {: note}

| Number of control plane hosts | Max clusters in location | Example of max worker nodes in location | Max cluster size |
| --- | --- | --- | --- |
| 3 hosts | 1 cluster, for demonstration purposes. | Up to 20 workers | 20 workers per cluster |
| 6 hosts | Up to 5 clusters  | 20 workers across 5 clusters, or 80 workers across 2 clusters | 60 workers per cluster |
| 9 hosts |  Up to 8 clusters | 40 workers across 8 clusters, or 140 workers across 3 clusters | 60 workers per cluster |
| 12 hosts |  Up to 11 clusters | 60 workers across 11 clusters, or 200 workers across 4 clusters | 60 workers per cluster |
{: caption="Sizing guidance for example numbers of hosts that the {{site.data.keyword.satelliteshort}} location control plane requires to run the master components for various combinations of clusters and worker nodes in the location." caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the number of clusters that you want to run in the location. The second column describes the number of hosts that the location control plane must have to run the masters for those clusters."}
{: class="simple-tab-table"}
{: #4cpu-16ram}
{: tab-title="4 vCPU, 16GB RAM"}
{: tab-group="loc-size"}

| Number of control plane hosts | Max clusters in location | Example of max worker nodes in location | Max cluster size |
| --- | --- | --- | --- |
| 3 hosts | 1 cluster, for demonstration purposes | Up to 100 workers | 100 workers per cluster |
| 6 hosts | Up to 20 clusters | 200 workers across 20 clusters, or 550 workers across 2 clusters | 300 workers per cluster |
| 9 hosts  | Up to 26 clusters | 400 workers across 26 clusters, or 850 workers across 3 clusters | 300 workers per cluster |
| 12 hosts  | Up to 36 clusters | 520 workers across 26 clusters, or 1150 workers across 4 clusters | 300 workers per cluster |
{: caption="Sizing guidance for example numbers of hosts that the {{site.data.keyword.satelliteshort}} location control plane requires to run the master components for various combinations of clusters and worker nodes in the location." caption-side="top"}
{: summary="The rows are read from left to right. The first column describes the number of clusters that you want to run in the location. The second column describes the number of hosts that the location control plane must have to run the masters for those clusters."}
{: class="simple-tab-table"}
{: #16cpu-64ram}
{: tab-title="16 vCPU, 64GB RAM"}
{: tab-group="loc-size"}
