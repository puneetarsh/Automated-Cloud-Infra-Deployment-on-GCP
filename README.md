# Automated-Cloud-Infra-Deployment-on-GCP
# Architecture Diagram
```mermaid
graph TD
    subgraph VPC ["Virtual Private Cloud"]
        direction TB
        
        subgraph Utils ["Cloud Connectivity"]
            NAT[Cloud NAT]
            Router[Cloud Router]
        end

        subgraph Public_Tier ["Public Subnets"]
            direction TB
            sub1["Public Subnet 1<br/>(Bastion Host)"]
            sub2["Public Subnet 2"]
        end

        subgraph Private_Tier ["Private Subnets"]
            direction TB
            p_sub1["Private Subnet 1<br/>(Private Instances)"]
            p_sub2["Private Subnet 2"]
        end

        %% Connections within VPC
        sub1 -- "Cloud Firewall Rules" --- p_sub1
        sub2 -- "Cloud Firewall Rules" --- p_sub2
    end

    subgraph Peering_Network ["PSA + VPC Peering"]
        direction TB
        MS[Memorystore]
        SQL[Cloud SQL]
    end

    %% VPC Peering Connection
    VPC -- "VPC Peering" --- Peering_Network

    %% Styling
    style VPC fill:#0f172a,stroke:#3b82f6,color:#fff
    style Public_Tier fill:#1e293b,stroke:#22c55e,color:#fff
    style Private_Tier fill:#1e293b,stroke:#a855f7,color:#fff
    style Peering_Network fill:#0f172a,stroke:#0d9488,color:#fff
    style Utils fill:#1e293b,stroke:#3b82f6,color:#fff