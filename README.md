# AWS VPC Peering

**Student:** Lavanya Dasari  
**Institution:** Vignan's Institute of Engineering for Women  
**Program:** B.Tech, Electronics and Communication Engineering  
**Batch:** 2023–2027  
**Internship area:** AWS Cloud Computing

## Project overview
This project documents a network design for communication between two Amazon Virtual Private Clouds (VPCs) using VPC peering. It covers CIDR planning, subnet design, route tables, security groups, bastion-host access, connectivity validation, and resource cleanup.

## Network design
- **VPC A:** `10.10.0.0/16`
  - Public subnet: `10.10.1.0/24` for the bastion host
  - Private subnet: `10.10.2.0/24` for App-A
- **VPC B:** `10.20.0.0/16`
  - Private subnet: `10.20.1.0/24` for App-B
- Planned private addresses: bastion `10.10.1.10`, App-A `10.10.2.10`, App-B `10.20.1.10`

The two VPC CIDR ranges do not overlap, allowing a peering connection to be configured between them.

## Routing and security
The route tables must include routes to the remote VPC CIDR through the peering connection. VPC A's public route table also needs a default route through its internet gateway for bastion access. SSH access should be limited to the user's current public IPv4 `/32` at the bastion and to the bastion's private IP for the private instances. ICMP should be limited to the peer application instance rather than opened to all IPv4 addresses.

## Validation procedure
Connectivity can be validated by testing traffic before and after peering and route configuration, checking both traffic directions, accessing the private instance through the bastion, and temporarily removing then restoring the relevant ICMP rule. Record actual observations from the AWS environment when carrying out these steps; this repository's architecture and procedure are not a substitute for live AWS console or terminal evidence.

## Files
- `docs/PROJECT_REPORT.pdf` — formatted project report
- `docs/PROJECT_REPORT.md` — editable report source
- `diagrams/architecture.mmd` — Mermaid architecture diagram source

## Cleanup
After testing, remove the EC2 instances and other resources created for the lab, including any remaining volumes or Elastic IPs, then remove the peering connection, routes, security groups, subnets, route tables, internet gateway, and VPCs as applicable. Check the account for any remaining billable resources.
