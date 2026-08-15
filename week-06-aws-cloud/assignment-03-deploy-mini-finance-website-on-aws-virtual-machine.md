# Assignment 3 — Deploy Mini Finance Website on AWS Virtual Machine

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will deploy the Mini Finance static HTML website on an AWS EC2 Linux virtual machine. You will launch the server, configure network access, connect through SSH, install a web server, deploy the GitHub source files, and confirm the website is reachable through the EC2 public IP.

---

# Task 1 — Launch and Secure an EC2 Linux Instance

## Goal

Launch an Amazon Linux 2 or Ubuntu EC2 instance in a public subnet, and configure its security group to allow SSH (22) and HTTP (80).

> No screenshot required for this task. Completion is verified through Task 4.

---

# Task 2 — Connect via SSH and Install a Web Server

## Goal

Connect to the instance using SSH and install Nginx or Apache.

> No screenshot required for this task. Completion is verified through Task 4.

---

# Task 3 — Clone and Deploy the Mini Finance Site

## Goal

Clone the Mini Finance repository (`https://github.com/pravinmishraaws/mini_finance.git`) and copy the site files to the web server's root directory.

> No screenshot required for this task. Completion is verified through Task 4.

---

# Task 4 — Start the Web Server and Verify the Website

## Goal

Start the web server and confirm the Mini Finance website is accessible through the EC2 public IP.

### Evidence

#### Screenshot 1 — Browser showing the Mini Finance website running at the EC2 public IP

![alt text](screenshots/aws-ass2-mini-finance.PNG)

---

#### Public IP URL

Paste the public IP address of your EC2 instance here (e.g. `http://3.91.105.10`):

http://13.49.224.225/

### Deployment walkthrough

# Deploying a Mini Finance Website on AWS EC2 with Nginx

As part of this deployment, I launched an Ubuntu 24.04 `t3.micro` EC2 instance in a public subnet within the default VPC in the `eu-north-1` AWS region. The instance was configured with a security group that allowed HTTP traffic on port 80 from anywhere, while SSH access on port 22 was restricted to my own IP address rather than being exposed to the entire internet.

After successfully connecting to the instance through SSH, I updated the Ubuntu system and installed Nginx, which would serve as the web server for the application. I also enabled Nginx to start automatically whenever the server boots.

Next, I cloned the Mini Finance repository onto the EC2 instance and copied the required website files into Nginx's web root:

```bash
/var/www/html
```

Before serving the application, I removed Nginx's default `index.nginx-debian.html` file. This was important because Nginx's default configuration includes several possible index filenames. Leaving the default Ubuntu page in the web root could cause it to be served instead of the actual application's homepage.

I also cleaned the web root by removing the repository's README, template notes, and Git tracking information. These files are useful during development but are not part of the website itself. Keeping unnecessary repository files in a publicly accessible web directory could expose internal project information without providing any benefit to website visitors.

Before testing the application from a browser, I verified the deployment locally from the EC2 server using `curl` against `localhost`. The request returned an HTTP `200` response, confirming that Nginx was running correctly and successfully serving the deployed website files.

This local test was an important troubleshooting step because it confirmed that the web server and application files were working correctly. Therefore, if the website could not be reached from an external browser, the remaining issue would most likely be related to networking, the EC2 public IP address, the security group, or the route between the public subnet and the internet.

Overall, the deployment successfully demonstrated how to provision an AWS EC2 server, configure secure SSH and HTTP access, install and configure Nginx, deploy a website from a Git repository, clean the production web root, and verify the application locally before exposing it to external traffic.


---

# Submission Instructions

- Add the required screenshot in your submission
- Include the EC2 Public IP URL
- Do not expose private keys, passwords, or account IDs

---

# Completion Checklist

- [x] EC2 instance launched in a public subnet with SSH (22) and HTTP (80) allowed
- [x] Connected to the instance via SSH
- [x] Web server (Nginx or Apache) installed
- [x] Mini Finance repository cloned and files copied to the web server root
- [x] Web server started and website verified in the browser (Screenshot 1)
- [x] EC2 Public IP URL included
- [x] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
