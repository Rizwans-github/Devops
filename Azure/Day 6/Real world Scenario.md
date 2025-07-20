## 🧠 Overview / Real‑World Scenario

* Example: a company has 2 web servers, 2 app servers, 2 DBs
* Goal: secure and structure them using Azure networking

## Virtual Network (VNet)

* Think of it as your private data center in Azure
* Divided using **subnets**
* Use CIDR (Classless Inter-Domain Routing) for IP allocation

## Subnets & CIDR

* Break the VNet into rooms (subnets)
* CIDR helps assign IP range to each room
* Eg: 10.0.0.0/16 for VNet, subnets like 10.0.1.0/24, 10.0.2.0/24

## Route Table

* Like GPS for data packets
* By default, Azure creates system routes
* Can override with UDR (User Defined Routes)

## Network Security Groups (NSGs)

* Like firewall rules for subnets/VM NICs
* Inbound & outbound rules (allow/deny)
* Eg: allow port 80/443 from internet to web subnet

## Application Security Groups (ASGs)

* Group VMs logically (e.g. WebGroup, DBGroup)
* Create NSG rules targeting ASGs instead of IPs
* Easier to manage as infra scales

## Application Gateway + WAF

* Load balances traffic at Layer 7 (HTTP/HTTPS)
* Has Web Application Firewall (WAF) to block attacks like SQL injection

## Azure Load Balancer

* Layer 4 load balancer (TCP/UDP)
* Public and internal options
* No SSL termination or path-based routing

## Azure DNS

* Host custom DNS zone like abhishek.com
* Map domain to Azure IPs (A, CNAME records)

## Azure Firewall

* Stateful firewall across subnets/VNets
* Supports app rules (FQDN) + network rules
* Central logging and high availability

## VNet Peering

* Connect two VNets like bridge
* Low latency, high bandwidth, no public internet
* Can be regional or global

## VPN Gateway

* Site-to-site: connect on-prem to Azure securely
* Point-to-site: connect laptop to Azure
* Uses IPsec/IKE, needs gateway subnet
