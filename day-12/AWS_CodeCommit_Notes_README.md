# 📝 AWS CodeCommit – Simple Notes

## 🌐 What is CodeCommit?

AWS **CodeCommit** is a fully managed **Git-based source control service** provided by AWS.  
Think of it like **GitHub or GitLab**, but hosted inside your AWS account.

👉 You can use CodeCommit to:
- 🧠 Store your **code, configuration files, and scripts** securely in AWS.
- 👥 Collaborate with teammates using Git commands (push, pull, clone).
- 🔐 Keep your repositories private inside your AWS environment.
- 🔗 Integrate easily with **CodePipeline**, **CodeBuild**, **CloudFormation**, and other AWS DevOps tools.

---

## 🧭 Why Use CodeCommit?

- ✅ Fully managed — no servers to set up or maintain.
- 💰 Pay only for usage (first 5 users are free in many regions).
- 🔒 Secure — uses **IAM** for access control and **KMS** for encryption.
- 🧠 Ideal for teams already using AWS services.
- 🚀 Works seamlessly with AWS DevOps workflows.

---

## 🧰 Key Features

| Feature | Description |
|---------|-------------|
| **Git-based** | Standard Git commands, no new tools to learn |
| **Private Repos** | All repos are private by default |
| **IAM Integration** | Fine-grained user/role permissions |
| **Encryption** | Data encrypted in transit (SSL) & at rest (KMS) |
| **Triggers** | Trigger AWS Lambda/SNS on pushes |
| **Notifications** | Built-in for PRs, merges, commits |
| **Branching & PRs** | Supports feature branching & code reviews |

---

## 🪜 Basic Workflow

1. **Create a repository** in CodeCommit.  
2. **Clone the repo** to your local machine using Git.  
3. Make code changes → `git add`, `git commit`, `git push`.  
4. Code is stored securely in AWS.  
5. Integrate with **CodePipeline** or **CodeBuild** to deploy automatically.

---

## 🧑‍💻 Example Commands

```bash
# Configure AWS CLI (first time)
aws configure

# Clone a CodeCommit repository (HTTPS)
git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/my-repo

# Make changes
cd my-repo
echo "Hello from CodeCommit" > hello.txt
git add hello.txt
git commit -m "Initial commit"
git push
```

---

## 🔐 Access Control

- Uses **IAM Users, Roles & Policies** to control access.
- Example minimal IAM policy:

```json
{
  "Effect": "Allow",
  "Action": [
    "codecommit:GitPull",
    "codecommit:GitPush"
  ],
  "Resource": "*"
}
```

- Authentication:
  - **Git credentials** (generated in IAM) for HTTPS.
  - **SSH keys** for SSH access.

---

## ⚠️ Important (2024+)

🚨 New AWS accounts **cannot create their first CodeCommit repo** automatically.  
👉 You must raise a **support request** to get CodeCommit **allowlisted** for your account or AWS Organization.

---

## 🧠 Common Use Cases

- Hosting application code for CI/CD pipelines.
- Version controlling **CloudFormation** or Terraform templates.
- Private repositories for internal tools.
- Managing configuration files in a secure, auditable way.

---

## 🚀 In CI/CD Pipelines

CodeCommit integrates seamlessly with AWS services:

```
CodeCommit → CodePipeline → CodeBuild → Deploy (Lambda / ECS / EC2)
```

Every time you push new code, the pipeline can automatically trigger a deployment.

---

## 📝 Summary Table

| Feature | CodeCommit |
|--------|------------|
| Hosting Type | Private (AWS managed) |
| Pricing | Pay per usage (Free tier for first 5 users) |
| Git Support | ✅ Yes |
| Security | IAM + KMS |
| Integration | Excellent with AWS services |
| Public Repos | ❌ Not supported |
| First Repo Creation | 📝 Requires AWS Support allowlisting (new accounts) |

---

## ✅ In Simple Words

> “CodeCommit is like GitHub — but private, secured, and inside AWS. Perfect if your pipelines and infra already live in AWS.”
