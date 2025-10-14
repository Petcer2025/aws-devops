# ☁️ AWS CloudFormation – Complete Class Notes & Interview Guide

> 📚 **Comprehensive notes covering fundamentals, advanced concepts, examples, and interview tips for AWS CloudFormation (CFT)**  
> Includes beginner & intermediate templates, CLI vs CFT comparison, and deployment steps.

---

## 🧠 1. What is AWS CloudFormation?

AWS **CloudFormation** is a service that allows you to **model, provision, and manage AWS infrastructure as code (IaC)**.  
You write **declarative templates** (YAML or JSON) that define your desired AWS resources, and CloudFormation automatically provisions and manages them.

### ✨ Key Benefits:
- Declarative IaC (describe *what*, not *how*)
- Version-controlled & code-reviewable
- Automatic dependency resolution
- Rollbacks on failure
- Drift detection (detect manual changes)
- Repeatable deployments across environments

---

## 🧭 2. IaC Flow with CloudFormation

1. 📝 **Write YAML/JSON template** describing infra  
2. 📤 Submit to **CloudFormation** via Console / CLI / API  
3. ☁️ AWS parses the template & provisions resources in correct order  
4. 🧱 Template becomes a **Stack** (a single deployable unit)  
5. 🔁 Future changes go through version-controlled template updates

CloudFormation acts as the **middle layer between your code and AWS APIs**, handling dependencies, order, rollback, and consistency.

---

## 🆚 3. CLI vs CFT — Interview Tip

| AWS CLI 🧰 | AWS CloudFormation 📄 |
|-----------|-------------------------|
| Imperative (step by step) | Declarative (desired end state) |
| Great for **short, one-off actions** | Best for **complex infra setups** |
| Not easily versioned | Stored in Git, versioned, reviewed |
| Manual orchestration | Automatic dependency resolution |
| Good for experiments / scripts | Good for production deployments |
| Example: create 1 bucket | Example: build entire VPC + EC2 stack |

👉 **Interview tip:**  
> “For quick tasks, I use CLI. For real infra or reusable deployments, I use CloudFormation.”

---

## 🧱 4. Key CloudFormation Concepts

### 🧠 **Stacks**
- A **stack** is a deployed instance of a template.
- Can be created, updated, deleted as one unit.
- Stacks are idempotent and versioned.

### 🔁 **Change Sets**
- Preview proposed changes before applying them to running stacks.
- Safe way to update production.

### 🧭 **Drift Detection**
- Detect resources that were changed manually outside CloudFormation.

### 🧨 **Rollback**
- Automatic rollback if stack creation/update fails.

### 🧰 **Stack Policies**
- JSON policies attached to stacks to protect critical resources from unintended updates.

### 🧩 **Nested Stacks**
- Reuse templates by calling one stack from another.

### 🌍 **StackSets**
- Deploy stacks across multiple AWS accounts and regions.

---

## 📝 5. CloudFormation Template Structure

A template can be written in YAML or JSON.  
It typically includes these sections:

| Section | Purpose |
|---------|---------|
| `AWSTemplateFormatVersion` | Version of template (e.g., 2010-09-09) |
| `Description` | Human-readable description |
| `Metadata` | Additional template info |
| `Parameters` | User inputs to customize stacks |
| `Rules` | Validation logic for parameters |
| `Mappings` | Lookup tables (e.g., region → AMI) |
| `Conditions` | Conditional resource creation |
| `Resources` | 🧱 Core section — defines AWS resources |
| `Outputs` | Export values (e.g., Instance ID, VPC ID) |

---

## 🧰 6. Intrinsic Functions (YAML Short Forms)

| Function | Usage |
|----------|-------|
| `!Ref` | Reference a parameter or resource |
| `!GetAtt` | Get an attribute (e.g., `!GetAtt MyEC2Instance.PublicDnsName`) |
| `!Sub` | Substitute variables inside strings |
| `!Join` | Concatenate values |
| `!If`, `!Equals`, `!And`, `!Or`, `!Not` | Conditionals |
| `!FindInMap` | Lookup in Mappings |
| `!ImportValue` | Import outputs from another stack |

---

## 🪜 7. Steps to Create a Stack (Console)

1. Go to **AWS CloudFormation** in AWS Console  
2. Click **Create stack** → “With new resources”  
3. Choose **Upload template file** or S3 URL  
4. Fill in stack name + parameters  
5. Review and click **Create stack**  
6. Monitor events until status = `CREATE_COMPLETE`

---

## 🧰 8. Steps to Deploy via CLI

```bash
# Create stack
aws cloudformation create-stack   --stack-name my-ec2-stack   --template-body file://template.yaml   --parameters ParameterKey=InstanceType,ParameterValue=t2.micro

# Update stack
aws cloudformation update-stack   --stack-name my-ec2-stack   --template-body file://template.yaml

# Delete stack
aws cloudformation delete-stack   --stack-name my-ec2-stack
```

---

## 🟢 9. Beginner Example: EC2 Instance Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Beginner EC2 Instance
Parameters:
  KeyName:
    Type: AWS::EC2::KeyPair::KeyName
    Description: Existing KeyPair
  InstanceType:
    Type: String
    Default: t2.micro
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-0c02fb55956c7d316
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      KeyName: !Ref KeyName
      InstanceType: !Ref InstanceType
      ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", AMI]
Outputs:
  InstanceId:
    Value: !Ref MyInstance
    Description: ID of the instance
```

---

## 🟡 10. Intermediate Example: VPC + Subnet + SG + EC2

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: VPC with EC2
Parameters:
  KeyName:
    Type: AWS::EC2::KeyPair::KeyName
    Description: Existing KeyPair
Resources:
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true
  PublicSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref VPC
      CidrBlock: 10.0.1.0/24
      MapPublicIpOnLaunch: true
  InternetGateway:
    Type: AWS::EC2::InternetGateway
  AttachGateway:
    Type: AWS::EC2::VPCGatewayAttachment
    Properties:
      VpcId: !Ref VPC
      InternetGatewayId: !Ref InternetGateway
  RouteTable:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref VPC
  Route:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId: !Ref RouteTable
      DestinationCidrBlock: 0.0.0.0/0
      GatewayId: !Ref InternetGateway
  SubnetRouteTableAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PublicSubnet
      RouteTableId: !Ref RouteTable
  SecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow SSH
      VpcId: !Ref VPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
  EC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      KeyName: !Ref KeyName
      InstanceType: t2.micro
      ImageId: ami-0c02fb55956c7d316
      SubnetId: !Ref PublicSubnet
      SecurityGroupIds: [!Ref SecurityGroup]
Outputs:
  PublicIP:
    Value: !GetAtt EC2Instance.PublicIp
    Description: Public IP of instance
```

---

## 🧠 11. Advanced Features

- **Nested Stacks** — modularize templates and reuse
- **StackSets** — deploy to multiple accounts/regions
- **Macros** — transform templates at deployment (e.g., AWS::Include, custom macros)
- **Custom Resources** — extend CFT with Lambda-backed actions

---

## 🌟 12. Best Practices

- ✅ Use YAML over JSON for readability
- 📦 Keep templates modular (Nested stacks)
- 🧪 Use Change Sets before updates in production
- 📊 Use Drift Detection regularly
- 📝 Version templates in Git for traceability
- 🚦 Use parameters, mappings, and conditions for reusability
- 🧠 Use Outputs for cross-stack references

---

## 🛠 13. Troubleshooting

| Issue | Likely Cause | Fix |
|-------|--------------|-----|
| Stack stuck in `ROLLBACK_COMPLETE` | Error during resource creation | Check Events tab |
| Drift detected | Manual resource changes | Reconcile or reapply |
| AccessDenied | IAM permissions | Attach required policies |
| Template validation failed | Syntax error | Use `aws cloudformation validate-template` |

---

## 📝 14. Common Interview Points

- Difference between **CLI vs CFT** ✅  
- Explain **template structure**  
- What are **stacks**, **change sets**, **drift detection**  
- YAML vs JSON  
- How to parameterize templates  
- How to use nested stacks or StackSets  
- Real-world scenario: "How would you deploy infra to 5 regions?"

---

## ✅ Conclusion

AWS CloudFormation is a **powerful declarative IaC tool** for managing AWS resources:
- 📄 Templates are declarative & version-controlled  
- ⚡ Automation handles dependencies, rollbacks, and drift  
- 🧠 Mastering CFT is a strong DevOps/Cloud skill, both for practical work and interviews

---

© 2025 — AWS CloudFormation Class Notes & Interview Prep
