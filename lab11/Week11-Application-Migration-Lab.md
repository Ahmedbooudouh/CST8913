# Week11 – Application Migration Lab
### Tailwind Traders – Application Migration Plan

## Task 1 – Set Up Tooling for Discovery

### Discovery Approach
For Tailwind's hybrid environment, the best approach is to use both agentless and agent-based discovery:

- **Agentless** for WEB01, WEB02, and APP01 (VMware), as it provides fast initial mapping with minimal overhead.
- **Agent-based** for SQL01 (physical server) to capture deeper, low-latency dependencies required for database workloads.

### Number of Azure Migrate Appliances
Tailwind should deploy two appliances:

1. One **VMware appliance** for WEB01, WEB02, APP01.
2. One **Physical Server appliance** for SQL01.

### Credentials Required
| Activity | Required Credentials |
|---------|----------------------|
| Software Inventory | Domain credentials with local admin access |
| SQL Discovery | SQL admin or read-only credentials |
| Dependency Mapping | Domain account with rights to read firewall rules and install agents |

### Best Practices During Discovery
1. Allow 30 days of data collection.
2. Ensure firewall rules allow outbound traffic from appliance.
3. Validate credentials before scans.

---

## Task 2 – Perform Assessment Planning

### Assessment Type
Tailwind should perform **production** and **non-production** assessments separately.

### Region & Duration
- **Region:** Canada Central
- **Performance Duration:** 30 days

### Sizing Method
Use **performance-based sizing** to avoid oversizing and ensure realistic VM recommendations.

### Comfort Factor, Pricing & Licensing
- Comfort Factor: **20%**
- Pricing: **Pay-As-You-Go**
- Licensing: **Azure Hybrid Benefit**

---

## Task 3 – Dependency Analysis

### Application Components
- WEB01, WEB02  
- APP01  
- SQL01  
- LB01  
- Backup server
- firewall

### Technical Dependencies
| Dependency | Description |
|-----------|-------------|
| HTTP/HTTPS | WEB -> APP |
| SQL traffic | APP -> SQL |
| Health checks | LB01 -> WEB |
| Authentication | Servers -> AD |
| DNS | Name resolution |
| SMB backup | Backup over TCP 445 |
| Monitoring | Outbound traffic |
| Client access | External -> LB |

### Noise to Filter Out
- System processes  
- Windows Update  
- Public IP traffic unrelated to app  
- Background OS services  

### Business Requirements
- High business criticality  
- 99.9% uptime  
- 1-hour downtime window  
- Sensitive data  
- Licensing tied to SQL + OS  
- Monthly patching  
- Firewall rule mapping required  
- Connection strings impacted by IP change  

---

## Task 4 – Validate Assessment Results

### Recommended VM Sizes
| Server | Size |characteristic|
|--------|-------|-------------|
| WEB01/WEB02 | D2s_v6 | 2 vCPUs, 8 GB RAM |
| APP01 | D4s_v6 | 4vCPUs, 16GB RAM |
| SQL01 | E8ds_v6 | 8 vCPUs, 64 GB RAM |

### Components to Replace/Optimize
- Replace LB01 with **Azure Load Balancer**
- Modernize SQL with SQL MI or Azure SQL DB
- Move backups to Azure Backup

### Dependency Validation
All WEB -> APP, APP -> SQL, authentication, DNS, and backup paths validated.

### SLA & Downtime
Azure services meet uptime expectations; SQL must fit within 1‑hour downtime.

### SQL Migration Options
| Option | Pros | Cons |
|--------|------|------|
| Rehost | Fast | Requires full management |
| SQL Managed Instance | High Availability + automation | More migration work |
| SQL DB | Fully managed | May lack instance-level features |

---

## Task 5 – Migration Plan 

### Pre-Migration Tasks
- Deploy migrate appliances  
- Complete discovery + assessment  
- Build Azure landing zone  
- Configure Azure Load Balancer  
- Prepare identity + monitoring  
- Finalize SQL migration method  

### Wave Steps

#### Wave 1 – WEB Tier
1. Deploy WEB01/WEB02  
2. Install Internet Information Services + app  
3. Join domain  
4. Attach to Azure LB  
5. Validate front-end  

#### Wave 2 – APP Tier
1. Deploy APP01  
2. Install API  
3. Update config for Azure SQL  
4. Test endpoints  
5. Validate full workflow  

#### Wave 3 – SQL Tier
1. Migrate SQL  
2. Update connection strings  
3. Validate performance  
4. Configure backup + monitoring  

### DNS Updates
- web.tailwind.internal -> Azure LB  
- api.tailwind.internal -> APP01  
- sql.tailwind.internal -> SQL endpoint  

### Load Balancer Considerations
- Health probes  
- Session persistence  
- Load distribution  

### Post-Migration Checklist
- Test WEB -> APP -> SQL  
- Confirm DNS  
- Validate app functionality  
- Enable backup + monitoring  
- LB failover test  

### Back-Out Plan
1. Revert DNS  
2. Restore SQL on-prem  
3. Switch LB traffic back  
4. Roll back WEB/APP changes  
5. Notify stakeholders  

---

## Task 6 – Migration Waves

### Final Wave Plan
| Wave | Servers | Reason |
|------|---------|--------|
| Wave 1 | WEB01, WEB02 | Stateless, simple rollback |
| Wave 2 | APP01 | Depends on WEB tier |
| Wave 3 | SQL01 | Highest risk; strict downtime |

### Rationale
- WEB tier first for early testing  
- APP after WEB validation  
- SQL last due to sensitivity and downtime limits  

---

## Conclusion
This migration plan provides a structured and low-risk approach for Tailwind's transition to Azure. With a mix of automated discovery, performance-based assessment, dependency analysis, and phased execution, Tailwind can ensure a smooth migration aligned with both technical and business requirements.
