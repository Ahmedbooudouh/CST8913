# Lab 9 : Cloud Cost Estimation for Enterprise Application Migration

**Ahmed Boudouh** 

---

## 1. Cost Estimate Report  
*A detailed breakdown of migration, operational, and management costs with explanations.*  

### Executive Summary  
Based on detailed Azure pricing calculations across three regions, ShopPro International's cloud migration presents the following financial overview:

- **Total Monthly Operational Cost:** CA $133,079  
- **One-time Migration Cost (including labor):** CA $46,000 (estimated)  
- **Annual Operational Cost:** CA $1,617,948  
- **Target Optimized Monthly Cost:** CA $79,847 (40% reduction)

This estimate is based on realistic regional deployments, including compute, storage, database, and monitoring resources.

---

### Detailed Cost Breakdown by Region  

#### North America (East US)  
- **Total Monthly:** CA $42,566  
- Compute: CA $2,725  
- Networking: CA $716  
- Databases: CA $35,992  
- Management: CA $3,133  

#### Europe (West Europe)  
- **Total Monthly:** CA $44,522  
- Compute: CA $2,898  
- Networking: CA $721  
- Databases: CA $37,198  
- Management: CA $3,705  

#### Asia-Pacific (Southeast Asia)  
- **Total Monthly:** CA $45,991  
- Compute: CA $3,074  
- Networking: CA $719  
- Databases: CA $38,495  
- Management: CA $3,703  

**Total Global Monthly Operational Cost:** CA $133,079

These operational costs include compute workloads, databases, networking, and monitoring for production systems across all three Azure regions.

---

### Infrastructure Configuration Details  

#### Compute Resources (Per Region)  
- Web Front-end: 10 × DS2 v2 VMs (2 vCPUs, 7 GB RAM)  
- ML Processing: 2 × NV12ads A10 v5 VMs (12 vCPUs, 110 GB RAM, GPU-enabled)  
- Operating System: Linux (cost-optimized)  
- Storage: P10/P20 managed disks  

#### Database Services  
- Azure SQL Managed Instance: Business Critical, 16 vCore, 1 TB storage  
- Azure Cosmos DB: 10,000 RU/s autoscale, 10 TB storage, multi-region write  
- Azure Synapse Analytics: DW2000c, 15 TB storage with geo-redundancy  

#### Networking & CDN  
- Azure Application Gateway: V2 tier with 5 GB data transfer  
- Azure Front Door: Global CDN with 1 TB outbound per region  
- Cross-region data transfer: 5 GB between regions  

These configurations ensure high availability, low latency, and optimized performance for millions of users worldwide.

---

### Migration Costs  

**Migration Cost Breakdown:**  

| Component | Description | Estimated Cost (CAD) |
|------------|--------------|----------------------:|
| Azure Database Migration Service | Used to replicate and migrate 30 TB of SQL, NoSQL, and warehouse data | 2,000 |
| Data Transfer / Data Box | Secure one-time bulk transfer from on-premises → Azure | 1,500 |
| Temporary Migration VMs | Short-term compute for validation/testing during cut-over | 500 |
| Employee Labor and Training | Internal and external staff time for setup, testing, and knowledge transfer (3 engineers × 2 months × CA $7,000) | 42,000 |
| **Total One-Time Migration Cost (including labor)** |  | **≈ CA $46,000** |

**Explanation:**  
This includes estimated personnel costs for migration support and training. Approximately three cloud engineers will contribute to the transition effort over two months. The investment covers data transfer, application cut-over, and validation to ensure smooth continuity during the migration process.

---

## 2. Cost Optimization Strategy  
*Recommendations on how ShopPro International can reduce costs through specific cloud features or service adjustments.*  

### 1. Reserved Instances Implementation  
| Resource | Current PAYG | 1-Year Reserved | Savings |
|-----------|---------------|----------------|----------:|
| Virtual Machines | CA $8,697 | CA $5,642 | 35% |
| SQL Managed Instance | CA $47,143 | CA $30,643 | 35% |
| Cosmos DB | CA $45,712 | CA $29,713 | 35% |
| **Total Monthly Savings** |  |  | **CA $45,661** |

By applying reserved instance pricing to long-running workloads, ShopPro International can save approximately **CA $45,661 per month**.

---

### 2. Auto-Scaling & Right-Sizing  
- ML Training VMs: Schedule for 300 hours/month instead of 730 hours (59% savings).  
- Web Tier: Implement scale sets for automatic adjustment (20–50% savings potential).  
- Database Scaling: Enable **auto-pause** for Azure Synapse during off-hours.  

These steps reduce unnecessary consumption and ensure cost matches actual demand.

---

### 3. Storage Optimization  
- Move backup storage to **Cool tier** for 50% savings.  
- Implement **lifecycle management** to archive analytics data automatically.  
- Optimize **Cosmos DB RU utilization** to reduce over-provisioning.  

Storage tiering can cut total data storage costs by up to **40–50%**.

---

### 4. Hybrid Benefits & Licensing  
- Apply **Azure Hybrid Benefit** for eligible Windows workloads.  
- Use **3-year reservations** for stable, mission-critical workloads for an additional **20% discount**.  

These licensing benefits help reduce compute and database costs further while preserving operational reliability.

---

### 5. Key Findings & Recommendations  

#### Major Cost Drivers  
- **Databases (72% of total cost):** CA $111,685 monthly  
  - Azure SQL Managed Instance: CA $47,143  
  - Cosmos DB: CA $45,712  
  - Synapse Analytics: CA $18,830  
- **Compute Resources (6.5% of total cost):** CA $8,697 monthly  
- **Management & Monitoring (8% of total cost):** CA $10,541 monthly  

#### Immediate Action Items  
- Implement Reserved Instances for databases and VMs (CA $45,661 monthly savings).  
- Enable auto-scaling on web and API tiers.  
- Schedule ML workloads to optimize GPU VM usage.  
- Review storage tiers for backup and archival data.  

#### Long-term Strategic Recommendations  
- Consider **Azure SQL Database** instead of Managed Instance for smaller workloads.  
- Evaluate **Azure Functions** to reduce VM costs for microservices.  
- Enforce **Azure Policy** for cost governance and tagging.  
- Use **Azure Cost Management** for continuous monitoring and reporting.  

---

## 3. Future Growth and Budget Plan  
*A three-year cost projection with strategic adjustments to optimize future expenses.*  

### Year-over-Year Cost Projection  

| Year | Growth Rate | Monthly Cost | Annual Cost | Optimized Cost |
|------|-------------:|-------------:|-------------:|----------------:|
| 2025 | Baseline | CA $133,079 | CA $1,596,948 | CA $79,847 |
| 2026 | +15% | CA $153,041 | CA $1,836,492 | CA $91,825 |
| 2027 | +20% | CA $183,649 | CA $2,203,788 | CA $110,189 |

### Strategic Adjustments for Growth  
- **Year 2:** Implement **serverless architectures** for the API back-end to improve scalability and reduce idle cost.  
- **Year 3:** Migrate to **Azure Kubernetes Service (AKS)** for better container density and management efficiency.  
- **Continuous:** Apply **right-sizing** and **cost recommendations** from Azure Advisor quarterly.  

---

### Conclusion  
The Azure migration for ShopPro International represents a major modernization initiative that provides:  

- Global scalability across three regions  
- A potential **40% cost reduction** through optimization strategies  
- Enterprise-grade reliability with **99.9%+ SLAs**  
- Enhanced security and compliance through Microsoft Defender for Cloud  

The **first-year investment of approximately CA $1.6 million**, plus a one-time **CA $46,000 migration cost including labor**, positions the company to sustain **20% annual growth** while reducing total cost of ownership compared to on-premises infrastructure.

---

