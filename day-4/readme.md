What is VPC in AWS?
Amazon Virtual Private Cloud (VPC) is a service that allows you to launch AWS resources in a logically isolated virtual network that you define. This virtual network closely resembles a traditional network that you would operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

Key Features of Amazon VPC
Virtual Private Clouds (VPCs)
A VPC is a virtual network that you can customize to meet your specific needs. You can add subnets, assign IP addresses, and configure route tables and gateways.

Subnets
A subnet is a range of IP addresses within your VPC. Each subnet must reside in a single Availability Zone. You can deploy AWS resources, such as EC2 instances, within these subnets.

IP Addressing
You can assign both IPv4 and IPv6 addresses to your VPCs and subnets. You can also bring your own public IPv4 addresses and allocate them to resources in your VPC.

Routing
Route tables determine where network traffic from your subnet or gateway is directed. You can create custom route tables to control the flow of traffic within your VPC
# 🌐 **AWS VPC (Virtual Private Cloud) – Simple Notes**

* **VPC = Your own private network inside AWS cloud.**
* It’s like having your own **mini-internet** inside the bigger internet.
* You decide how resources (servers, databases, storage) connect and talk.

<img width="521" height="311" alt="image" src="https://github.com/user-attachments/assets/3c4e814f-ddac-4eec-8d27-15941a04d856" />

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

## 🛠️ **Main VPC Components (Simple Explanation)**

* **VPC** → Your private network in AWS (like your own data center).

* **Subnets** → Smaller sections of your VPC (e.g., public subnet for web servers, private subnet for databases).

  * Each subnet is in **one Availability Zone**.

* **IP Addressing** → You decide the IP range (IPv4/IPv6) for your VPC and subnets.

* **NACL (Network ACL)** → Subnet-level firewall (stateless → needs inbound & outbound rules).

  * Example: Block all traffic from a suspicious IP range.

* **Security Groups** → Instance-level firewall (stateful → if you allow inbound, return traffic is auto allowed).

  * Example: Allow SSH (22) or HTTP (80) to a specific EC2.

* **Routing (Route Tables)** → Decides where traffic goes.

  * Example: Internet traffic → Internet Gateway.

* **Gateways & Endpoints** →

  * **Internet Gateway (IGW):** Public internet access.
  * **NAT Gateway:** Private subnet → internet (outbound only).
  * **VPC Endpoint:** Private connection to AWS services (no internet needed).

* **VPC Peering** → Connect two VPCs so they can talk to each other.

* **Transit Gateway** → Central hub to connect multiple VPCs and networks.

* **Traffic Mirroring** → Copy network traffic for monitoring/security.

* **Flow Logs** → Logs all network traffic going in/out of your VPC (for troubleshooting & auditing).

* **VPN Connection** → Connect your AWS VPC to your **on-premise network** securely.

---

## 💡 Quick Analogy (House Example 🏠)

* **VPC** = Your house.
* **Subnets** = Rooms in the house.
* **Security Groups** = Door locks on each room.
* **NACLs** = Fence rules around the property.
* **Gateways** = Main gate to enter/exit house.
* **Route Table** = Google Maps deciding which way traffic goes.

<img width="611" height="481" alt="image" src="https://github.com/user-attachments/assets/1c83aa03-2dcb-4a11-a566-4570f42651b5" />


<img width="663" height="317" alt="ankithafinal1" src="https://github.com/user-attachments/assets/1ea62ab5-c414-4a6d-92bd-754123254eed" />

<img width="663" height="317" alt="ankithafinal" src="https://github.com/user-attachments/assets/5a42163c-5099-4729-8710-601b289ce510" />

<img width="663" height="317" alt="ankitha" src="https://github.com/user-attachments/assets/334a8593-b76e-44c6-ac92-aa1a1d97fc02" />

