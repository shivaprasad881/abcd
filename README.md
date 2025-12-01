Step 1: Launch EC2 Instance
text
1. Login → AWS Console → EC2 Service
2. Click "Launch Instance"
3. Name: "my-web-server"
4. AMI: Ubuntu 22.04 (free tier)
5. Instance Type: t2.micro (free)
6. Key Pair: Create → "my-key" → Download .pem
7. Network: Allow SSH (22), HTTP (80)
8. Launch Instance
Step 2: Connect via SSH
bash
# On your computer terminal:
cd Downloads
chmod 400 my-key.pem
ssh -i my-key.pem ubuntu@IP_ADDRESS
# IP_ADDRESS = EC2 Public IPv4
Step 3: Install & Setup
bash
# On EC2 (after SSH):
sudo apt update
sudo apt install nginx -y
cd /var/www/html
sudo nano index.html
Step 4: Create Website
html
<!-- In index.html -->
<h1>My AWS Website</h1>
<p>Running on EC2</p>
<p>IP: YOUR_EC2_IP</p>
Step 5: Start & Test
bash
sudo systemctl start nginx
# Test: Open browser → http://IP_ADDRESS
AWS Architecture Diagram
text
┌─────────┐     ┌─────────┐     ┌─────────┐
│  User   │────▶│  AWS    │────▶│  EC2    │
│Browser  │     │  Route  │     │Instance │
└─────────┘     │  53(DNS)│     └─────────┘
                └─────────┘          │
                                ┌────┴────┐
                                ▼         ▼
                          EBS Volume  Security
                          (Storage)   Group
                                     ┌─────┐
                                     │Ports│
                                     │22-SSH│
                                     │80-HTTP│
                                     └─────┘
Important Ports to Remember
text
22  → SSH (Secure Connection)
80  → HTTP (Website)
443 → HTTPS (Secure Website)
3306 → MySQL Database
5432 → PostgreSQL Database
Key AWS Services
text
EC2     = Virtual Servers
S3      = File Storage
RDS     = Managed Database
VPC     = Virtual Network
IAM     = Users & Permissions
Route53 = DNS Service
