# Sprint 1 - Homework - "Putting it into practice"

## Re-Cap Objectives

- Identify one service your team supports
- Identify a small group (4-8) that supports this service
- Create a list of indicators, objectives, and agreements for this service
- Create a GitHub page for this service with a readme outlining the service, team, SLIs, SLOs and SLAs
- Present your service in the sprint retrospective 3 weeks from now

note: The team and I do not support any production services directly and it would take too much time to delve into our primary project namely Kubernetes, so the selected project is a supporting module namely the Nginx Ingress component. For the rest of this task, I will speak for the on behalf of the consumer/operator.

## Overview

- Name: **terraform-lnrs-k8s-ingress-nginx** [Gitlab](https://gitlab.b2b.regn.net/terraform/official-modules/k8s/terraform-lnrs-k8s-ingress-nginx/)
- Kind: Terraform Module
- Summary: The module creates a NGINX Ingress Controller backed by a cloud load balancer on a Kubernetes cluster that has been created by using either the AWS or Azure Kubernetes modules.
- Support: Prikesh Patel, Dan Sossick, Peter Barr, Aydogan Osman and James Miller

```mermaid
graph TD
    A(End User/Internal Service/External Service) -->B(Cloud Load Balancer)
    B --> C{NGINX Ingress Controller}
    C -->E[Nginx default backend] & id1
    C -->F([service 1])
    C -->G([service 2])
    id1[(Ingress resource)]
    id1--Configured routes and routing rules -->C
```

The diagram is an abstract representation of the service.

## Continued

- Nginx is a cloud-agnostic service that includes an enterprise-grade service and addons that allow a clear line of sight to apps in development, test, or production. With per-app analytics, you the operator gain new insights into app performance and reliability. This allows you to  pinpoint performance issues before they impact production.
- The ingress controller specifically is responsible for fulfilling the ingress, usually with a load balancer, it may also configure your edge or additional frontends to help control the flow of traffic.
- Configuration examples include but not limited to;
  - Services externally with reachable URLs
  - Load balance traffic
  - Terminate SSL / TLS
  - Name-based virtual hosting.
  
# Example: Hosting an externally facing service with multiple sub-services with 6h of peek activity in two increments 24/7/365

## SRE Team: High Level Activities

- Reliability - Maintaining a high amount of system uptime and reliability
and measuring everything monitoring, peer-reviewing source code and benchmarking all key indicators for progress.
- Alerting - For quickly identifying and resolving issues and in outside of business hours.
- Leveraging automation - to eliminate manual tasks.
- Implement smaller more frequent changes - As to reduce downtime from changes.
- Embrace risk - A certain amount of downtime is tolerable. You have to accept a certain amount of risk of failure.

## Indicators

The parameters by which the nginx service is mesured

- Latency - The delay before a transfer of data begins following an instruction for its transfer.
- Throughput - The amount of items passing through nginx as a rate.
- Availability - The ability of a user to access information or resources in a specified location and in the correct format.
- Error rate - It is the ratio of the number of erroneous units of data to the total number of units of data transmitted.
- Budget Consumption - How much of the budget allotted to the nginx service is used during normal, high and low traffic periods
- Responsiveness - How quickly, appropriately, and efficiently employees follow up with those seeking assistance in or outside working hours.
- Esclations - From an internal or external capacity, the number of occasions we receive negative feedback about the service we are providing.

Measurements are collected over time a specified amount of time, such as one year.

| Metric       | Value [SLI] | Mesured in [Rate] | Notes                              | Upper Limit[SLO] | Lower Limit[SLO] | Customer Agreement[SLA] |
|--------------|-------------|-------------------|------------------------------------|------------------|------------------|-------------------------|
|              |             |                   |                                    |                  |                  |                         |
| Latency      | 75%         | ms                | 6h a day acceptable latency         | 100ms            | 10ms             |                         |
| Throughput   | 75%         | MBps              | 6h a day acceptable high throughput | 100MBps          | 1MBps            |                         |
| Availability | 99.70%      | Time              | 4min a days downtime 1days a year  | 5mins            | 1min             | 99.65%                  |
| Error Rate   | 99.45%      | E/ps              | 8mins a day 2 days a year          | 10mins           | 1min             |                         |

| Metric             | Value [SLI] | Mesured in [Rate] | Notes                           | Upper Limit[SLO] | Lower Limit[SLO] |
|--------------------|-------------|-------------------|---------------------------------|------------------|------------------|
| Budget Consumption | 85% of X    | Time/Scale/Cost   | "+-15% for scaling during peek" | 15%              | -15%             |

| Metric                 | Value [SLI] | Mesured in [Rate] |
|------------------------|-------------|-------------------|
|                        |             |                   |
| On-Call Responsiveness | 98%         | Time/Action       |
|                        |             |                   |
| External Escalations   | 98.00%      | Time/Action       |
