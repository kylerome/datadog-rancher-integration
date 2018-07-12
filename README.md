# Datadog on Rancher 2.0

[Datadog](https://www.datadoghq.com/) is a popular monitoring solution for aggregating metrics and events for distributed systems.  From infrastructure integrations to collaborative dashboards, Datadog gives you a clean single pane view into the information that is most important to you.  To make Datadog easy to use with Rancher 2.0, we have modified the Datadog helm chart to make it a simple one click deployment through Rancher's catalog feature.

## Prerequisites
1. Datadog API Key (you can use an existing secret with your API key, or let the chart make one for you)
1. By default Rancher Kubernetes Engine (RKE) does not allow unauthenticated access to the kubelet API which Datadog relies on for many of its metrics.  When installing the cluster with RKE we need to provide extra arguments to the kubelet service.
   ```yaml
    services:
      kubelet:
        extra_args:
          read-only-port: 10255
   ```
1. NOTE: You should make sure this port is properly firewalled
1. A Kubernetes 1.8+ cluster attached to a Rancher installation
## Setup & Configuration
1. The Datadog chart (chart) is available through both Helm stable and the Rancher library, for ease of use we would suggest using the chart in Rancher Library.  The Rancher library is enabled by default, if disabled this setting can be modified under Global->Catalogs.
2. The charts values.yaml file configuration options have been made available through the UI in Rancher, to learn more about them please refer to the values.yaml file which has additional information and links describing the variables. (Link to chart)

## Dashboards
