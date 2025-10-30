# Prerequisites

Before proceeding, verify that your environment meets the system  
requirements.

## Hardware requirements

The following hardware requirements outline the resources that must be  
available on the worker node to run MSR 4 services effectively.

| Resource | Minimum | Recommended |
|-----------|----------|-------------|
| **CPU** | 2 CPU | 4 CPU |
| **RAM** | 4 GB | 8 GB |
| **Disk** | 40 GB | 160 GB |

## Software requirements

The following software requirements must be met to run the MSR 4 workload  
successfully.

| Software | Version and Comment |
|-----------|--------------------|
| **Kubernetes** | 1.31+ (if using MKE 3.8.x or 4.x) |
| **HELM** | 3.7+ |
| **Redis** | If remote and not a part of the deployment |
| **PostgreSQL** | If remote and not a part of the deployment |

## Network requirements

Certain services will be exposed through the following ports. These ports must  
be accessible and configured correctly in the firewall.

| Port | Protocol | Description |
|------|-----------|-------------|
| **80** | HTTP | The Harbor portal and core API accept HTTP requests on  
this port. You can change this port in the configuration file. |
| **443** | HTTPS | The Harbor portal and core API accept HTTPS requests on  
this port. You can change this port in the configuration file. |

