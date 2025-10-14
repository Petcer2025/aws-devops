# AWS CLI – Quick Notes (Windows)

## 🌐 What is AWS CLI?

The **AWS Command Line Interface (CLI)** is a tool to manage AWS services from your terminal.  
Instead of clicking through the AWS Console, you can:
- Create/delete S3 buckets
- Deploy Lambdas
- Spin up EC2 instances
- Manage IAM users, and much more

---

## 🧰 1. Installation (Windows)

### Option 1: Official Installer (Recommended)
1. Download from [AWS CLI official page](https://aws.amazon.com/cli/).
2. Run the Windows MSI installer (64-bit).
3. Verify installation:

```bash
aws --version    for linux 
./aws.exe --version  for windows
```

Expected output:

```
aws-cli/2.x.x Python/3.x.x Windows/10 exe/AMD64 prompt/off
```

### Option 2: Portable Method
1. Extract AWS CLI folder (e.g., `N:\Cloud`).
2. Add folder path to **Environment Variables → User PATH**.
3. Test with:

```bash
aws --version  for linux
./aws.exe --version for windows
```

---

## ⚙️ 2. Configure AWS CLI

Run once to set up credentials:

```bash
aws configure                  for linux
./exe.aws configure            for windows
```

Prompts:

```
AWS Access Key ID [None]: <your-access-key>
AWS Secret Access Key [None]: <your-secret-key>
Default region name [None]: us-east-1
Default output format [None]: json
```

Config files stored in:

```
C:\Users\<YourName>\.aws\credentials
C:\Users\<YourName>\.aws\config
```

---

## 🧠 3. CLI Structure

```
aws <service> <operation> [parameters]
```

Example:

```bash
aws s3 ls                    for linux
./aws.exe aws s3 ls          for windows
```

---

## 🪣 4. Common S3 Commands

| Task                         | Command                                        |
|------------------------------|------------------------------------------------|
| List buckets                 | `aws s3 ls`                                    |
| List bucket contents         | `aws s3 ls s3://my-bucket`                     |
| Create bucket                | `aws s3 mb s3://my-bucket`                     |
| Remove empty bucket          | `aws s3 rb s3://my-bucket`                     |
| Remove bucket + all contents | `aws s3 rb s3://my-bucket --force`             |
| Upload file                  | `aws s3 cp file.txt s3://my-bucket/`           |
| Download file                | `aws s3 cp s3://my-bucket/file.txt .`          |
| Sync local ↔ bucket          | `aws s3 sync ./ s3://my-bucket`                |

---

## 💻 5. Common EC2 Commands

| Task               | Command                                                |
|--------------------|--------------------------------------------------------|
| List instances     | `aws ec2 describe-instances`                           |
| Start instance     | `aws ec2 start-instances --instance-ids i-xxxx`        |
| Stop instance      | `aws ec2 stop-instances --instance-ids i-xxxx`         |
| Terminate instance | `aws ec2 terminate-instances --instance-ids i-xxxx`    |
| List key pairs     | `aws ec2 describe-key-pairs`                           |

---

## 👤 6. IAM Commands

| Task              | Command                                               |
|-------------------|-------------------------------------------------------|
| List users        | `aws iam list-users`                                  |
| List roles        | `aws iam list-roles`                                  |
| Create access key | `aws iam create-access-key --user-name <username>`    |

---

## 🌎 7. Regions & Profiles

Set region inline:

```bash
aws s3 ls --region us-west-2
```

Use profiles:

```bash
aws configure --profile dev
aws s3 ls --profile dev
```

---

## 🧰 8. Useful Commands

```bash
aws help                      # CLI help menu
aws s3 help                   # Help for S3
aws configure list            # Show current config
aws sts get-caller-identity   # Verify logged-in account
```

---

## 📝 9. Troubleshooting

- **Command not found** → PATH not set / terminal not restarted  
- **AccessDenied** → Wrong credentials or missing IAM permissions  
- **Region error** → Set default region or add `--region us-east-1`  
- **Proxy issues** → Set `HTTP_PROXY` and `HTTPS_PROXY` env variables  

---

## 🌟 Pro Tips

- Combine with **AWS CDK** or **Terraform** for infrastructure as code  
- Use `aws s3 sync` for backups/migrations  
- Parse JSON with `jq`:

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

---

✅ You are now ready to **play with AWS CLI on Windows!**
