# GCP Cost Analysis for Secure VPC Deployment

This document outlines the estimated monthly cost of running a secure application architecture on Google Cloud Platform (GCP). It includes compute, networking, database, and caching services based on the architecture implemented using VPC, Compute Engine, Cloud NAT, Cloud SQL, and Memorystore.

---

## 🧱 1. Compute Engine (VM Instances)

### Bastion Host (Public Subnet)
| Name            | Machine Type | Count | Usage (hrs/month) | Est. Cost (USD) |
|-----------------|--------------|-------|--------------------|-----------------|
| `bastion-host`  | e2-micro     | 1     | 720                | ~$5 – $7        |

> Used for secure SSH access to private instances.

---

### Private Instances (Application Servers)
| Name              | Machine Type | Count | Usage (hrs/month) | Est. Cost (USD) |
|-------------------|--------------|-------|--------------------|-----------------|
| `private-vm`      | e2-medium    | 2     | 720 each           | ~$50 – $60 total|

> Runs backend services inside private subnet.

---

## 🌐 2. Networking (VPC)

### VPC, Subnets & Firewall
| Resource        | Configuration          | Est. Cost (USD) |
|----------------|------------------------|-----------------|
| VPC Network    | Custom VPC             | Free            |
| Subnets        | Public + Private       | Free            |
| Firewall Rules | Allow SSH / Internal   | Free            |

---

### VPC Peering
| Type             | Usage                  | Est. Cost (USD) |
|------------------|------------------------|-----------------|
| Same Region      | Internal communication | Free            |
| Cross Region     | Data transfer          | ~$0.01–$0.05/GB |

---

## 🔄 3. Cloud NAT & Router

### Cloud NAT
| Resource     | Usage            | Est. Cost (USD) |
|--------------|------------------|-----------------|
| NAT Gateway  | Moderate traffic | ~$20 – $40      |

> Allows private instances to access internet securely.

---

### Cloud Router
| Resource        | Usage (hrs/month) | Est. Cost (USD) |
|-----------------|------------------|-----------------|
| Cloud Router    | 720              | ~$36            |

---

## 🗄️ 4. Cloud SQL (Database)

| Instance Type   | Storage | Usage (hrs/month) | Est. Cost (USD) |
|----------------|---------|--------------------|-----------------|
| db-f1-micro    | 10–50GB | 720                | ~$20 – $50      |

> Managed relational database for application.

---

## ⚡ 5. Memorystore (Redis)

| Tier        | Capacity | Est. Cost (USD) |
|-------------|----------|-----------------|
| Basic       | 1 GB     | ~$30 – $35      |
| Standard    | 1 GB     | ~$50 – $80      |

> Used for caching and fast data access.

---

## 📈 6. Data Transfer (Estimate)

| Type                    | Monthly Usage | Est. Cost (USD) |
|-------------------------|---------------|-----------------|
| Inbound Traffic         | Free          | $0.00           |
| Internal (same zone)    | -             | Free            |
| Cross-zone traffic      | Moderate      | ~$5 – $10       |
| Internet Egress         | ~5–10 GB      | ~$10 – $30      |

---

## 💰 Total Estimated Monthly Cost

| Component              | Est. Cost (USD) |
|-----------------------|-----------------|
| Compute Engine        | ~$55 – $65      |
| Networking (NAT + Router) | ~$56 – $76  |
| Cloud SQL             | ~$20 – $50      |
| Memorystore           | ~$30 – $80      |
| Data Transfer         | ~$10 – $30      |
| **Total**             | **~$170 – $300/month** |

---

