# 04 - Lab: Estimating Costs using the Azure Pricing Calculator

## Lab Objective

This hands-on exercise is designed to demonstrate an understanding of Azure's pricing models and key cost drivers by using the official [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).

The goal is to estimate the monthly cost of a basic internal web application when migrating it from an on-premises datacenter to Azure.

## Azure Services Used

The estimated architecture represents a Hybrid IaaS/PaaS solution: [Image of Cloud Service Models comparison IaaS PaaS SaaS]

| Category | Azure Service | Role in the Architecture | Service Model |
| :--- | :--- | :--- | :--- |
| **Compute** | **Virtual Machines (VMs)** | Hosting the ASP.NET web application (2 instances). | **IaaS** |
| **Databases** | **Azure SQL Database** | Managed PaaS database holding inventory and pricing information. | **PaaS** |
| **Networking** | **Application Gateway** | Layer 7 Load Balancer, including Web Application Firewall (WAF) functionality. | **PaaS** |

## Configuration and Cost Factors

The following parameters, based on the Lab requirements, were applied in the Pricing Calculator:

| Setting | Key Parameter | Value | Cost Impact Observation |
| :--- | :--- | :--- | :--- |
| **Virtual Machines** | Instance / Count / Hours | D2 v3 / 2 VMs / 730h (24/7) | VM type and size directly dictate the compute cost. |
| **Azure SQL DB** | Service Tier / vCore / Storage | General Purpose / Gen 5 / 8 vCore / 32 GB | **The main PaaS cost driver**, determined by required performance and service level. |
| **Application Gateway** | Size / Hours / Data Processed | Medium / 2 Instances / 730h / 1 TB | Fixed instance cost plus variable cost based on data volume processed. |
| **Backup** | Storage Tier | RA-GRS (Read-Access Geo-Redundant) | Additional cost for high data durability and disaster recovery capability. |

## Estimation Result (Based on your Spreadsheet)

The total estimation shows the cost breakdown according to the chosen configuration:

| Service | Estimated Monthly Cost (USD) | Observations |
| :--- | :--- | :--- |
| **Azure SQL Database** | **$1,567.39** | The dominant cost component due to the "General Purpose" Service Tier and 8 provisioned vCores. |
| **Virtual Machines** | $305.14 | Standard cost for two D2 v3 Windows VMs running 24/7. |
| **Application Gateway** | $206.04 | Cost based on Medium instance size and 1 TB of processed data. |
| **Total Estimated Cost** | **$2,078.56 USD** | **Total monthly cost based on Pay-As-You-Go pricing.** |

## AZ-900 Concepts Demonstrated

* **Pay-As-You-Go Pricing**: Billing based on the consumption of resources measured per hour.
* **Virtual Machine Cost Drivers**: Region, size, operating system, and uptime hours.
* **PaaS Cost Drivers**: Performance (vCore) and Service Tier (General Purpose) are the main drivers for Azure SQL Database costs.
* **Cost Optimization (Theory)**: To reduce this cost, one should consider **Azure Reservations (Reserved Instances)** for VMs (up to 72% discount) or choosing a lower Service Tier for the database.
