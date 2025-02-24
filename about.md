---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-12"

keywords: satellite, hybrid, multicloud, about

subcollection: satellite

---

{{site.data.keyword.attribute-definition-list}}



# About {{site.data.keyword.satelliteshort}}
{: #about}

Learn about {{site.data.keyword.satellitelong}} terminology, service architecture, and components.
{: shortdesc}

With {{site.data.keyword.satellitelong_notm}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud. To achieve this distributed cloud architecture, {{site.data.keyword.satelliteshort}} provides an API-based suite of tools that you can use to represent your on-premises data center, a public cloud provider, or an edge network as a {{site.data.keyword.satelliteshort}} location. You fill the {{site.data.keyword.satelliteshort}} location with your own host machines that meet the [minimum host requirements](/docs/satellite?topic=satellite-host-reqs). Then, these hosts provide the compute power to run {{site.data.keyword.cloud_notm}} services, such as workloads in managed {{site.data.keyword.redhat_openshift_notm}} clusters or data and artificial intelligence (AI) tools like {{site.data.keyword.watson}}.

Your {{site.data.keyword.satelliteshort}} location includes tools such as {{site.data.keyword.satelliteshort}} Link and {{site.data.keyword.satelliteshort}} Config to provide additional capabilities for securing and auditing network connections in your location and consistently deploying, managing, and controlling your apps and policies across clusters in the location.

For more information, see the [{{site.data.keyword.satelliteshort}} product page](https://www.ibm.com/cloud/satellite){: external}.

## Benefits of using {{site.data.keyword.satelliteshort}}
{: #about-benefits}

Review some key benefits for using {{site.data.keyword.satellitelong_notm}}.
{: shortdesc}

|Benefits|Description|
|----------|----------------------------------|
|Bring your own infrastructure to {{site.data.keyword.cloud_notm}}.|With {{site.data.keyword.satellitelong_notm}}, you can bring your own infrastructure that is in your on-premises data center, in public cloud providers, or in edge environments to {{site.data.keyword.cloud_notm}} by creating a {{site.data.keyword.satelliteshort}} location. With this setup, you can run your workloads in the physical location of your choice to meet legal requirements, compliance standards, data speeds, and network latency requirements while securely using {{site.data.keyword.cloud_notm}} services. For more information, see [Setting up {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations). |
|Securely access {{site.data.keyword.cloud_notm}} services.|Every {{site.data.keyword.satelliteshort}} location is securely connected to {{site.data.keyword.cloud_notm}} through an encrypted TLS tunnel that is provided with the {{site.data.keyword.satelliteshort}} Link component. By using this TLS tunnel, you can securely access {{site.data.keyword.cloud_notm}} services in your location and use them with the same security and compliance standards as in {{site.data.keyword.cloud_notm}}.  For more information, see [Connecting {{site.data.keyword.satelliteshort}} locations with services outside of locations by using endpoints](/docs/satellite?topic=satellite-link-location-cloud).  |
|Control and monitor network traffic to services.|With {{site.data.keyword.satelliteshort}} Link, you can control network access to apps, services, and servers that run in {{site.data.keyword.cloud_notm}}, public cloud providers, or in your on-premises data center. Configure these apps, services, and servers as sources for your {{site.data.keyword.satelliteshort}} endpoints. All network traffic that is sent through an endpoint is automatically captured and can be reviewed by the user.  |
|Consistently deploy Kubernetes resources across multiple locations.|Use a single dashboard to manage the deployment of Kubernetes resources across cloud, on-premises, and edge environments with {{site.data.keyword.satelliteshort}} Config and gain global visibility into your apps and Kubernetes operations. For more information, see [Deploying Kubernetes resources across clusters](/docs/satellite?topic=satellite-setup-clusters-satconfig). |
|Centralize your monitoring and logging.|{{site.data.keyword.satellitelong_notm}} is integrated with {{site.data.keyword.mon_full_notm}}, {{site.data.keyword.la_full_notm}}, and {{site.data.keyword.at_full_notm}}. You can view the metrics and logs for the apps that run in your location, the {{site.data.keyword.cloud_notm}} services that you use, or the events that happen in your location from a single location. |
{: caption="Reasons to use Satellite." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the benefit of using Satellite. The second column is a description of the benefit."}

For more information about {{site.data.keyword.satelliteshort}}, how it works and the service benefits, see the [{{site.data.keyword.satelliteshort}} product page](https://www.ibm.com/cloud/satellite){: external}.

## {{site.data.keyword.satelliteshort}} components
{: #components}

Review the following {{site.data.keyword.satelliteshort}} components.
{: shortdesc}

| Component | Description |
| --- | --- |
| {{site.data.keyword.satelliteshort}} Config | Based on the [Razee open source project](https://github.com/razee-io/Razee){: external}, {{site.data.keyword.satelliteshort}} Config is a continuous delivery tool that you can use to consistently roll out versions of your apps across clusters in {{site.data.keyword.satelliteshort}} locations. For more information, see [Deploying {{site.data.keyword.redhat_openshift_notm}} resources across clusters with {{site.data.keyword.satelliteshort}} configurations](/docs/satellite?topic=satellite-setup-clusters-satconfig).|
| {{site.data.keyword.satelliteshort}} hosts | Hosts are machines that reside in your infrastructure provider, across at least three separate zones, and must [meet the minimum host requirements](/docs/satellite?topic=satellite-host-reqs). After attaching the hosts to a {{site.data.keyword.satelliteshort}} location, you assign the hosts to [{{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} services](/docs/satellite?topic=satellite-managed-services) such as clusters to provide the computing power to run the service workloads. For more information, see [Setting up {{site.data.keyword.satelliteshort}} hosts](/docs/satellite?topic=satellite-host-concept). |
| {{site.data.keyword.satelliteshort}} Link | {{site.data.keyword.satelliteshort}} Link securely connects your {{site.data.keyword.satelliteshort}} location to the {{site.data.keyword.cloud_notm}} region that your location is managed from. All communication that leaves and enters your location is proxied by the Link tunnel server, and network traffic on this connection can be monitored and audited. For more information, see [Connecting {{site.data.keyword.satelliteshort}} locations with external services using Link endpoints](/docs/satellite?topic=satellite-link-location-cloud).|
| {{site.data.keyword.satelliteshort}} location | A location is a representation of an environment in your infrastructure provider, such as an on-prem data center or cloud, that you want to bring {{site.data.keyword.cloud_notm}} services to so that you can run workloads in your own environment. You create the location based off at least three separate zones of your backing infrastructure environment, and attach host machines from across these zones in your infrastructure to the location. The [{{site.data.keyword.satelliteshort}} console](https://cloud.ibm.com/satellite/locations){: external} provides a single pane of glass to manage the workloads that run across the infrastructure in your locations. For more information, see [Planning your infrastructure environment for {{site.data.keyword.satelliteshort}}](/docs/satellite?topic=satellite-infrastructure-plan) and [Setting up {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations).|
| {{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} services | An {{site.data.keyword.cloud_notm}} service that you can set up in a {{site.data.keyword.satelliteshort}} location, such as a {{site.data.keyword.openshiftlong_notm}} cluster. The service is managed from the {{site.data.keyword.cloud_notm}} region that your location is managed from, but you provide the infrastructure hosts to run the service's resources in your location. For more information, see [{{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} services](/docs/satellite?topic=satellite-managed-services). |
| {{site.data.keyword.satelliteshort}} storage | {{site.data.keyword.satelliteshort}} storage uses {{site.data.keyword.satelliteshort}} Config to provide a convenient way to install various storage drivers in {{site.data.keyword.openshiftlong_notm}} clusters across your {{site.data.keyword.satelliteshort}} locations, by using storage templates. The storage templates are provided and tested by the vendors. After you install {{site.data.keyword.satelliteshort}} storage, your cluster users can use Kubernetes persistent volume claims (PVCs) to order and save their application data in persistent storage. For more information, see [Understanding {{site.data.keyword.satelliteshort}} storage templates](/docs/satellite?topic=satellite-sat-storage-template-ov). |
{: caption="Satellite terms" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the component. The second column is a brief description of the component."}
