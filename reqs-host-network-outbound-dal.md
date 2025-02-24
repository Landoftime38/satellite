---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-11"

keywords: satellite, hybrid, multicloud, hypershift, core os

subcollection: satellite

---

{{site.data.keyword.attribute-definition-list}}

# Dallas
{: #reqs-host-network-outbound-dal}

Before creating region specific firewall rules, make sure to create the general firewall rules for hosts in any region.
{: shortdesc}


To check your host set up, you can use the `satellite-host-check` script. For more information, see [Checking your host set up](/docs/satellite?topic=satellite-host-network-check).
{: tip}


## Allow control plane worker nodes to communicate with the control plane master
{: #host-out-cp-dal}



{{site.data.keyword.satelliteshort}} control plane hosts in Red Hat CoreOS enabled locations
* Destination IPs: 169.46.43.146,169.48.236.58,169.60.150.218
* Destination hostnames: `c131.us-south.satellite.cloud.ibm.com`, `c131-1.us-south.satellite.cloud.ibm.com`, `c131-2.us-south.satellite.cloud.ibm.com`, `c131-3.us-south.satellite.cloud.ibm.com`, `c131-e.us-south.satellite.cloud.ibm.com`
* Protocol and ports: TCP 30000 - 32767

{{site.data.keyword.satelliteshort}} control plane hosts in locations without Red Hat CoreOS enabled

* Destination IPs: 52.117.39.146, 169.48.134.66, 169.63.36.210
* Destination hostnames: `c119.us-south.satellite.cloud.ibm.com`, `c119-1.us-south.satellite.cloud.ibm.com`, `c119-2.us-south.satellite.cloud.ibm.com`, `c119-3.us-south.satellite.cloud.ibm.com`, `c119-e.us-south.satellite.cloud.ibm.com`
* Protocol and ports: TCP 30000 - 32767 and UDP 30000 - 32767

## Allow control plane worker nodes to back up control plane etcd data to {{site.data.keyword.cos_full_notm}}
{: #host-out-worker-dal}

{{site.data.keyword.satelliteshort}} control plane hosts
* Destination IPs: N/A
Destination hostnames: `s3.us.cloud-object-storage.appdomain.cloud`
* Protocol and ports: HTTPS

## Allow Link connectors to connect to the Link tunnel server endpoint
{: #host-out-link-dal}

You can find the hostnames or IPs by running the `dig c-<XX>-ws.us-south.link.satellite.cloud.ibm.com +short` command. Replace `<XX>` with `01`, `02`, and so on, until no DNS results are returned.
{: tip}

{{site.data.keyword.satelliteshort}} control plane hosts
* Destination IPs: 169.48.139.210, 169.48.188.146, 169.59.239.66, 169.60.2.74, 169.61.140.18, 169.61.156.226, 169.61.31.178, 169.61.38.178, 169.62.221.10
* Destination hostnames: `c-01-ws.us-south.link.satellite.cloud.ibm.com`, `c-02-ws.us-south.link.satellite.cloud.ibm.com`, `c-03-ws.us-south.link.satellite.cloud.ibm.com`, `c-04-ws.us-south.link.satellite.cloud.ibm.com`
* Protocol and ports: TCP 443

## Allow hosts to be attached to a location and assigned to services in the location
{: #host-out-services-dal}

All {{site.data.keyword.satelliteshort}} hosts
* Destination IPs: 52.116.223.52, 169.48.141.13, 169.61.50.28  
* Destination hostnames: `origin.us-south.containers.cloud.ibm.com`
* Protocol and ports: TCP 443

## Allow Akamai proxied load balancers for {{site.data.keyword.satelliteshort}} Config and Link API
{: #host-out-akamai-dal}

{{site.data.keyword.satelliteshort}} control plane hosts
* Destination IPs: [Akamai's source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} 
* Destination hostnames: `api.us-south.link.satellite.cloud.ibm.com`, `config.us-south.satellite.cloud.ibm.com`, `us-south.containers.cloud.ibm.com`
* Protocol and ports: TCP 443

## Allow hosts to communicate with {{site.data.keyword.registrylong_notm}}
{: #host-out-cr-dal}

All {{site.data.keyword.satelliteshort}} hosts
* Destination IPs:   N/A
* Destination hostnames: `icr.io`, `us.icr.io`, `registry.bluemix.net`,
* Protocol and ports: TCP 443

## Allow hosts to communicate with {{site.data.keyword.monitoringlong_notm}}
{: #host-out-mon-dal}

All {{site.data.keyword.satelliteshort}} hosts
* Destination IPs and hostnames: [{{site.data.keyword.monitoringshort_notm}} endpoints](/docs/monitoring?topic=monitoring-endpoints)
* Protocol and ports: TCP 443 and 6443

## Allow hosts to communicate with {{site.data.keyword.loganalysislong_notm}}
{: #host-out-la-dal}

All {{site.data.keyword.satelliteshort}} hosts
* Destination IPs and hostnames: [{{site.data.keyword.loganalysislong_notm}} endpoints](/docs/log-analysis?topic=log-analysis-endpoints#endpoints_api_public)
* Protocol and ports: TCP 443
