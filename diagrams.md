## AWS Architecture Diagram
```mermaid
flowchart TD
    %% Define Styles
    style EC2 fill:#FFDD00,stroke:#000,stroke-width:2px
    style S3 fill:#1F618D,stroke:#000,stroke-width:2px
    style RDS fill:#2ECC71,stroke:#000,stroke-width:2px
    style Lambda fill:#F39C12,stroke:#000,stroke-width:2px
    style CloudWatch fill:#9B59B6,stroke:#000,stroke-width:2px
    style VPC fill:#5D6D7E,stroke:#000,stroke-width:2px
    style IAM fill:#E74C3C,stroke:#000,stroke-width:2px
    style SQS fill:#8E44AD,stroke:#000,stroke-width:2px
    style SNS fill:#2980B9,stroke:#000,stroke-width:2px

    %% Reposition VPC to the left side, and IAM to the right
    subgraph VPC[VPC]
        EC2[EC2 Instances] --> S3[S3 Bucket]
        EC2 --> RDS[RDS Database]
        S3 --> Lambda[Lambda Function]
        Lambda --> CloudWatch[CloudWatch Monitoring]
        EC2 --> SQS[SQS Queue]
        SQS --> Lambda
        Lambda --> SNS[SNS Notifications]
    end

    %% IAM Role and rerouted authentication arrow on the right side
    IAM[IAM Role] -->|Authentication| EC2
    IAM -.->|Access Control| RDS