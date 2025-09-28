
# 🌐 **AWS VPC (Virtual Private Cloud) – Simple Notes**

* **VPC = Your own private network inside AWS cloud.**
* It’s like having your own **mini-internet** inside the bigger internet.
* You decide how resources (servers, databases, storage) connect and talk.

---

## 🛠️ **Key Points**

* **Isolated & Secure** → Other people’s VPCs cannot see yours.
* **IP Range** → You choose the private IP addresses for your VPC.
* **Subnets** → Smaller networks inside your VPC (e.g., one for public servers, one for private databases).
* **Gateways/Routers** → Let your VPC talk to the internet or other networks.

  * **Internet Gateway (IGW)** → Gives public access.
  * **NAT Gateway** → Private resources can reach internet (updates) but are not exposed.
* **Security** →

  * **Security Groups** → Control traffic at instance level.
  * **Network ACLs** → Control traffic at subnet level.

---

## 📌 Example

Imagine a house 🏠 (VPC):

* **Rooms** = Subnets (organize resources)
* **Doors** = Gateways (entry/exit to internet)
* **Locks** = Security Groups/ACLs (who can enter/leave)

---

💡 **In simple words:**
VPC = Your **private, secure, customizable network** in AWS where you place all your cloud resources.

---

