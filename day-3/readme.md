
# 🚀 **AWS EC2 – Quick Notes for Students**

## 🌐 What is EC2?

* **Amazon Elastic Compute Cloud (EC2)** = Virtual servers in AWS cloud.
* Provides **secure, scalable, pay-as-you-go compute power**.
* High availability (99.99%) and flexible pricing (On-Demand, Reserved, Spot).

---

## 📌 Why EC2?

* Run apps/websites on-demand.
* Scale capacity up/down within minutes.
* HPC (High Performance Computing), ML projects, gaming, analytics.
* Secure & reliable with **AWS Nitro System**.

---

## 🖥️ EC2 Instance Types

Each family is designed for a specific workload:

* **General Purpose (M, T)** → Balanced compute + memory (web apps, dev/test).
* **Compute Optimized (C)** → High-performance processing (gaming, HPC).
* **Memory Optimized (R, X, Z, U)** → Large memory workloads (databases, analytics).
* **Storage Optimized (I, D, Hpc)** → Big data, logs, warehousing.
* **Accelerated Computing (P, G, F, Inf, Trn, VT)** → GPUs, AI/ML, graphics.

👉 Extra letters mean special hardware: `a` (AMD), `g` (Graviton), `i` (Intel), `n` (network optimized), `d` (instance store).

---

## ⚡ EC2 Pricing Options

* **On-Demand** → Pay per hour/second, flexible.
* **Reserved** → Commit for 1–3 years, big discounts.
* **Spot** → Use unused capacity at low cost (can be interrupted).
* **Savings Plans** → Flexible commit for lower cost.
* **Dedicated Hosts** → Physical servers reserved for you.

---

## 🧩 EC2 Basics

* **AMI (Amazon Machine Image)** → Template for OS & software.
* **Instance Type** → Defines CPU, RAM, storage.
* **Instance States** → Pending → Running → Stopped → Terminated.
* **Security Groups** → Virtual firewall (allow/deny inbound & outbound traffic).
* **Key Pairs** → Used for secure login (SSH for Linux, RDP for Windows).

---

## 🚀 Launching an EC2 Instance (Steps)

1. Choose **AMI** (e.g., Ubuntu, Amazon Linux).
2. Select **Instance Type** (t2.micro for free tier).
3. Configure details (network, storage, tags).
4. Add **Security Group** rules (e.g., allow port 22 SSH, port 80 HTTP).
5. Select/create **Key Pair** for login.
6. Launch → Connect with SSH or RDP.

---

## 🔧 Managing EC2 Instances

* **Start/Stop/Restart/Terminate** via console or CLI.
* **Monitor** performance with **CloudWatch**.
* **Scale** with **Auto Scaling Groups**.
* **Elastic IPs** for fixed public IP.
* **EBS Volumes** for persistent storage.
* **Snapshots** for backups.

---

## 🛡️ Security Best Practices

* Use **MFA** and IAM roles instead of root account.
* Restrict **SSH/RDP access** to your IP (not 0.0.0.0/0).
* Keep instances patched and updated.
* Use **CloudTrail** for audit logs.

---

💡 **In simple words:**
EC2 = AWS’s cloud servers. Choose instance type, pricing, security, and launch → then scale and manage as per your workload.

---

👉 Do you want me to turn this into a **Day 22 PDF (AWS EC2 Basics + Launch + Management + Best Practices)** so your students can keep it as a handout?

