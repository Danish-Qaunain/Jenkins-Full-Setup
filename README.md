# Jenkins  setup 🚀  

This documentation provides a complete journey with Jenkins — beginning with installation and culminating in building fully automated pipelines.
It includes instructions for installing Jenkins on AWS EC2, configuring Docker as an agent, setting up CI/CD workflows, and deploying to Kubernetes. 

---
## ⚙️ Installation on AWS EC2  

### Step 1: Launch an EC2 Instance  
1. Go to **AWS Console** → **Instances (running)**  
2. Click **Launch instances**  
3. Choose an Ubuntu-based AMI (recommended)  



## 🔐 Configure Security Groups

#### Note: By default, Jenkins is not accessible externally because of AWS inbound traffic restrictions. To allow external access, you need to open port 8080 in the instance's security group settings.

### Steps:

- Navigate to EC2 > Instances and select your instance.

- In the bottom panel, click Security → Security Groups.

Add an inbound rule to allow TCP traffic on port 8080.
(Alternatively, you may allow all traffic, but it is recommended to restrict access to only the required port.)

## 📦 Install Jenkins 🛠️
```bash
sudo apt update
sudo apt install docker.io
```

### Verify installation:

`java -version`

### Install Jenkins

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```



## 🌐 Step 4: Access Jenkins

Open in browser:

```
http://<ec2-public-ip>:8080
```

Get the Jenkins Admin password:

`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

- 🔑 Paste the password into the Jenkins login page.  
- ⚙️ Install **Suggested Plugins**.  
- 👤 *(Optional)* Create an **Admin User**.




Jenkins Installation is Successful. You can now starting using the Jenkins


## 🔌 Install the Docker Pipeline Plugin in Jenkins 

1. Log in to your Jenkins instance.  
2. Navigate to **Manage Jenkins → Manage Plugins**.  
3. In the **Available** tab, search for **Docker Pipeline**.  
4. Select the plugin and click **Install**.  
5. Once the installation is complete, **restart Jenkins** to apply the changes.


Wait for the Jenkins to be restarted.

## 🐳 Docker Agent Configuration

### 1. Install Docker

Run the following commands to install Docker:

```bash
sudo apt update
sudo apt install docker.io
``` 
### 2. Grant Permissions to Users

Add the Jenkins user and the Ubuntu user to the Docker group to allow Docker commands:

```bash
sudo su -
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
### 3. Restart Jenkins

It is recommended to restart Jenkins after configuring Docker:
```bash
http://<ec2-public-ip>:8080/restart
```

