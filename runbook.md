# RUNBOOK name


>## 0. :goal_net: Purpose 
A runbook is an operational reference which is used to describe an service in a deployed environment including Operational information, dependencies and infrastructure details. It should be easy to read, consistent across all applications, and accurate. 

>## 1. :bulb: Overview
`The overview section provides a general description of the application. It provides enough information for someone unfamiliar with the application to understand what it is used for and how to find additional information if necessary. It should provide additional links such as:`
- SLA Service Level Agreements (`What explicit or implicit expectations are there from users or clients about the availability of the service or system?`)
- Links to the application website
- Service presence or usage in environments (`Select from list, mark X if service is present`)
    - [x] env1
    - [ ] env2
    - [ ] envn
- Vendor information and vendor support contacts (`if applicable`) 
- General license information and renewal dates 
- Certificates and Frequency Rotation info or dates: 
- Links to any internal documentation or project pages: 

>## 2. :pager: Support Contacts
`A runbook should have contact information for at least one primary contact at each level of support. That “contact” might be a team of people or it might be a single individual, but the contact list should contain enough information to make initial contact or look up the full contact information in a company directory. If the application is supported by the team, contact information might be an e-mail alias, a ticket queue, or a support hotline. For individuals, it might be their cell phone.`
- Team Name: 
- Service Slack: 
- Email DL: 
- Service Owner:       
- Service Owner BackUp:    
- PagerDuty Incident Link:
- JIRA Project Name:
- Others (as deemed necessary)

>## 3. :crayon: Architecture
`The architecture diagram shows the hosts, VMs and services which compose the application environment. It should provide enough information to be useful for audiences like Devs or SRE Engineers need to troubleshoot an alert or outage. If Production setup is different across datacenters, have a separate diagram by datacenter. List supporting pieces (e.g. data stores) and up/down stream dependencies and document known “customer interactions” the service contributes to`

- Logical architecture describing the components of the system
- Physical representation of those components, for example make it obvious when components share hosts 
- Sequence diagrams for key transactions
 

>## 4. :electron: Infrastructure & Network
`The Infrastructure & Network table describes all of the network ports that are used by the application. At a minimum this should be provide a list of services and the ports and protocols that they listen on. This can be useful when working with the network team to define firewall rules, or when establishing external monitoring to check application health.`

Below is an example

| Service | Port | Protocol |
|----- | -----|----- |
| nginx | 443  | TCP - HTTPS |
| mysql | 3306 | TCP - mysql |
 
 
>## 5. :mega: Monitoring & Alerts (*if applicable*)
`The monitoring section should define all of the services and resources that need to be monitored. This can be used to ensure that monitoring is complete. For actions to be taken if an alert is triggered and its resolution steps. Please document those steps into the Service Playbook`



>## 6. :scroll: Transactions SLO Definitions 
`Please record identified Observability Key Transactions for the service`


>## 7. :no_entry: Security and Access Control
`The objective of this section is to make it quick and easy for SRE Engineer to identify what could have gone wrong with the system if someone complains that they are not able to authenticate or do not have access to the necessary resources. It should also identify what group of administrative users can be contacted if special permissions are needed to investigate an issue.`



>## 8. :arrows_counterclockwise: Backup and Recovery (*if applicable*)
`This runbook section describes the disaster recovery (DR) processes that are in place to ensure the system or data can be recovered in the event of an unexpected failure. At a minimum it should describe any automated backup procedures, the frequency and times they run, and the data retention policies for archived data. Be sure to provide information to any detailed DR plans which will be used to restore the system during a catastrophic outage or data loss.`
