# Accounting Integration PLAYBOOK

### _Rev: 2021-01-11_ 

sgsgsgsgsdfg 
>## Purpose 
Playbooks are documented processes to identify issues and recover from failure scenarios. Document the investigation process: 
* Step-by-step recovery process 
* Validation of service restoration 
* Document known issues and remediations

>## Recorded Known Issues
* [Expired Vault Token](#expired-vault-token): Application can't start due to problem with VaultReader class
* [Missing Vault Secret](#missing-vault-secret): Application can't start, JSON parsing error, missing property on VaultReader class
* [CouchBase Timeout](#couchbase-timeout): New Relic alerts on AIS timeout or CouchBase


### Expired Vault Token
- Did this incident/problem result in a P1 or P2 Situation in the past? 
  - [ ] Yes - OPI-[number1 ]; OPI-[number2 ]; OPI-[number3 ]; OPI-[number4 ] 
  - [x] No 
- Alerts and logs `Application will fail to start and healthCheck will be failing. Container logs will display exceptions from Spring Framework when trying to instantiate VaultReader.java, errors trying to fetch or parse vault data. Now that AIS has moved to Kraken, vault tokens are renewed automatically by the vault-agent container which should avoid this problem from happening.`
- User experience: `AIS will continue working if pods are not restarted. If pods are restarted with expired tokens, nothing will work for the customer.`
- Procedural steps:
  1. A new user should be obtained from Thycotic and used to SSH into the environment or one of the containers in the pod should be accessed using kubectl
  2. A new Vault Token should be generated using `curl`
  3. The new token should bee populated in k8s as a secret
- Expected outcome:  `Application should run as expected after a restart.`
- Verification process `Wait for application to start and check the healthCheck.`
- Time-bound escalation policy `PagerDuty incident creation: https://concur.pagerduty.com/service-directory/P3TJK0L`

### Missing Vault Secret
- Did this incident/problem result in a P1 or P2 Situation in the past? 
  - [ ] Yes - OPI-[number1 ]; OPI-[number2 ]; OPI-[number3 ]; OPI-[number4 ] 
  - [x] No 
- Alerts and logs `Application will fail to start and healthCheck will be failing. Container logs will display exceptions from Spring Framework when trying to instantiate VaultReader.java, errors will mention a missing property in JSON. Now that AIS has moved to Kraken, vault secrets are renewed automatically by the vault-agent container which should avoid this problem from happening.`
- User experience `AIS will continue working if pods are not restarted. If pods are restarted with expired secrets, nothing will work for the customer.`
- Procedural steps:
  1. Check which property is missing from the vault JSON based on the exception description
  2. Connect to vault and insert the missing data
- Expected outcome `Application should run as expected after a restart.`
- Verification process `Wait for application to start and check the healthCheck.`
- Time-bound escalation policy `PagerDuty incident creation: https://concur.pagerduty.com/service-directory/P3TJK0L`

### CouchBase Timeout
- Did this incident/problem result in a P1 or P2 Situation in the past? 
  - [ ] Yes - OPI-[number1 ]; OPI-[number2 ]; OPI-[number3 ]; OPI-[number4 ] 
  - [x] No 
- Alerts and logs `New Relic alerts with AIS timeout exception.`
- User experience `Customer's requests to AIS will fail.`
- Procedural steps:
  `Usually this happens when CE APIs behaves differently like increase in response time, API call failures etc. We have to use New relic/Kibana tools to narrow down the issues by check the metrics, error logs and collect information to create support ticket with CE.`
- Expected outcome `Application should go back to normal automatically as soon as the issue resolved.`
- Verification process `New relic alerts should stop and application should be recovered from the issue.`
- Time-bound escalation policy... `We need to create support ticket with CE with correct priority. Then we need to escalate the support ticket with CE account manager via Michelle Schmetzer.`
