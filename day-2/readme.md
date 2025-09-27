🔐 AWS IAM (Identity and Access Management)

IAM is AWS’s security system for controlling who can access what in your AWS account.

🛠️ Key Components

Users → Individual people or apps with credentials (username, password, or keys).

Groups → Collection of users with similar permissions (easier management).

Roles → Temporary access for AWS services, apps, or external accounts.

Policies → Rules (in JSON) that define what actions are allowed/denied on resources.

✅ Important Points

Follows least privilege → give only required permissions.

Supports MFA (Multi-Factor Authentication) for extra security.

Provides audit logs (CloudTrail) for tracking activities.

Policies can be AWS-managed (ready-made) or Customer-managed (you create).

💡 In simple words:
IAM = The guard of your AWS account.
It decides who can log in, what they can do, and which resources they can access — keeping everything secure.