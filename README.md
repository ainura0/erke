graph TD
    subgraph Client Tier
        User((Пайдаланушы))
    end
    
    subgraph AWS VPC
        direction LR
        
        % 1. Frontend: Static Content
        User --> CloudFront[AWS CloudFront: CDN]
        CloudFront --> S3[S3 Bucket: Static React Files]
        
        % 2. Backend: Dynamic Content
        CloudFront --> ALB[Application Load Balancer (ALB)]
        
        ALB --> ASG[Auto Scaling Group (ASG)]
        ASG --> EC2_1[EC2/Flask App 1]
        ASG --> EC2_2[EC2/Flask App 2]
        
        % 3. Database Layer
        EC2_1 --> RDS[AWS RDS: PostgreSQL Managed DB]
        EC2_2 --> RDS
        
        % 4. Monitoring (Cross-VPC)
        EC2_1 -.-> Prom[Prometheus Server: Metrics Collection]
        EC2_2 -.-> Prom
        Prom --> Grafana[Grafana: Visualization]
    end
    
    style User fill:#007bff,color:#fff
    style Prom fill:#ffcc00
    style Grafana fill:#34a853,color:#fff
    
    % Легенда
    subgraph Data Flow Legend
        RDS -.-> Backups[S3: Snapshots]
        Prom -.-> Alert[Alert Manager]
    end
