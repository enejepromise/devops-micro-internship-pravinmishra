# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

![alt text](<react app.PNG>)

---

#### Screenshot 2 — Output of `ip a`

![alt text](<task 3 2.PNG>)
---

#### Screenshot 3 — Output of `sudo ss -tulpen`

![alt text](<task 3 3.PNG>)
---

#### Screenshot 4 — Output of `sudo ufw status`

![alt text](<task 3 4.PNG>)
---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

The following line from the ss -tulpen output proves that Nginx is listening on 0.0.0.0:80:
tcp LISTEN 0 511 0.0.0.0:80 0.0.0.0:* users:(("nginx",pid=25233,fd=5),("nginx",pid=25232,fd=5),("nginx",pid=25231,fd=5))

---

**2. What proves SSH is active on port 22?**

The following lines confirm that SSH is active on port 22:

tcp LISTEN 0 4096 0.0.0.0:22 0.0.0.0:* users:(("systemd",pid=1,fd=119))

tcp LISTEN 0 4096 [::]:22 [::]:* users:(("systemd",pid=1,fd=121))

---

**3. Did you find any unexpected open ports? Explain briefly.**

No. The expected open ports were:

Port 80 for the Nginx web server.
Port 22 for SSH remote access.

The other listening ports (53 for systemd-resolved, 68 for DHCP, and 323 for chronyd) are standard system services used for DNS resolution, network configuration, and time synchronization. They are expected on an Ubuntu server and do not indicate any unexpected services.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

![alt text](<task 3 5.PNG>)
---

#### Screenshot 2 — Output of `sudo nginx -t`
![alt text](<task 3 6.PNG>)

---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`
![alt text](<task 3 7.PNG>)

---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart in production, the website or application may become unavailable to users because Nginx is responsible for receiving and forwarding incoming web requests. In a real production environment, this could mean customers cannot access the application, leading to downtime and a poor user experience. The first thing I would do is check the error by running sudo nginx -t to see if there is a configuration problem. I would also review the Nginx logs to understand what caused the restart to fail before making any changes.

---

**2. What's your basic rollback plan?**

If my changes caused Nginx to fail, I wouldn't continue making random fixes. Instead, I would roll back to the last known working configuration. My basic rollback plan would be:

Run sudo nginx -t to identify the problem.
Restore the previous working Nginx configuration from a backup or from version control (Git).
Test the restored configuration again using sudo nginx -t to make sure there are no errors.
Restart or reload Nginx with sudo systemctl restart nginx or sudo systemctl reload nginx.
Verify that the service is running using systemctl status nginx and test the website to confirm it is working again.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`
![alt text](<task 3 8.PNG>)

---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

![alt text](<task 3 9.PNG>)
---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

![alt text](<task 3 10.PNG>)
---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

No. I did not find any error messages in the Nginx error log during my inspection. The only message I saw was a notice, which said that Nginx was using inherited sockets during a restart. This is a normal informational message and not an error.

An empty error log or one with no recent errors means that Nginx did not encounter any problems during the period I checked. It does not mean the server will never have issues, it only means that no errors were recorded at that time.

---

**2. If there were no errors, what does that indicate about the system?**

Since there were no recent errors, it indicates that the system was operating normally while I monitored it. Nginx started successfully, accepted requests, and served web pages without any recorded failures. However, this only reflects the health of the system during the time I examined the logs, not its overall long-term reliability.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes. My curl requests were visible in the access log with the curl user agent and an HTTP 200 (OK) status code. This proves that my requests successfully reached the Nginx server, were processed correctly, and received a successful response. It also confirms that traffic is flowing properly between the client and the web server and that Nginx is recording incoming requests in its access log.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

![alt text](<task 3 11.PNG>)
---

#### Screenshot 2 — Output of `free -h`

Add your screenshot here.
![alt text](<task 3 12.PNG>)
---

#### Screenshot 3 — Output of `df -h`

Add your screenshot here.
![alt text](<task 3 13.PNG>)
---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

Add your screenshot here.
![alt text](<task 3 14.PNG>)
---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Based on the system information, none of the resources are currently under critical pressure. The CPU load is 0.00, which means the server is almost idle. Memory usage is also healthy, with about 539 MiB available out of 908 MiB. The disk is 59% used, leaving about 2.8 GB of free space, so there is still enough storage available.

If I had to choose one resource to monitor more closely, it would be disk space. Unlike CPU and memory, disk usage usually keeps increasing over time because of logs, application data, and updates. If it is not monitored, it can eventually fill up and cause problems.

---

**2. What happens if disk becomes 100% full in a production server?**

If the disk reaches 100% capacity, the server can experience serious problems. Applications may fail to write files, databases may stop working properly, log files cannot be updated, and users may start receiving errors or be unable to use the application. In some cases, services like Nginx may fail to start or restart because they cannot create temporary files or write logs. This is why monitoring disk usage and cleaning up unnecessary files regularly is an important part of managing a production server.
---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

Add your screenshot here.
![alt text](<task 3 15.PNG>)
---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

Add your screenshot here.
![alt text](<task 3 16.PNG>)
---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

![alt text](<task 3 17.PNG>)
---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

I confirm that the correct version of the application is deployed by opening the application's public URL in a browser and checking that the latest changes I made are visible. I also verify that Nginx is serving the updated build successfully by ensuring the service is running and by sending a request with curl to confirm the server responds with a successful HTTP 200 status. If the application displays the expected updates and the server responds correctly, I can be confident that the correct version has been deployed.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)
![alt text](<task 3 18.PNG>)

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

![alt text](<task 3 19.PNG>)
---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.
![alt text](<task 3 20.PNG>)
---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

The configuration failure happened because I removed the semicolon (;) at the end of the try_files directive in the Nginx configuration file. Since Nginx requires every directive to end with a semicolon, it could not correctly interpret the configuration and reported a syntax error: unexpected "}" in /etc/nginx/sites-enabled/default:9
This prevented the configuration test from passing.
---

**2. How did you fix the issue?**

I fixed the issue by opening the Nginx configuration file and adding the missing semicolon (;) back to the try_files directive. After saving the file, I ran sudo nginx -t again to verify that the configuration was valid. Once the syntax test passed successfully, I restarted Nginx using sudo systemctl restart nginx and confirmed that the website was working by sending a curl request, which returned an HTTP 200 OK response.
---

**3. How can you avoid this kind of issue in real production systems?**
To avoid this kind of issue in a real production environment, I would always test the Nginx configuration with sudo nginx -t before restarting or reloading the service. I would also keep the configuration files in version control, review changes carefully, and make small, incremental updates instead of large changes. These practices help catch syntax errors early and reduce the risk of causing downtime in production.
---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

![alt text](<task 3 21.PNG>)

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![alt text](<task 3 22.PNG>)
---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

The application broke because the web files in /var/www/html were removed. Since Nginx could no longer find the files it was supposed to serve, it returned an HTTP 500 Internal Server Error instead of loading the application.
---

**2. How did you fix the issue and restore the application?**

I restored the application by moving the backup folder back to its original location using:

sudo mv /var/www/html_backup /var/www/html

After that, I restarted Nginx with sudo systemctl restart nginx and tested the application using curl. The server responded with HTTP 200 OK, confirming that the application had been restored successfully.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

To prevent this type of issue in a production environment, I would keep regular backups of the application files, avoid deleting production files directly, and use version control and deployment tools to manage changes safely. I would also test updates in a staging environment before deploying them to production and have a rollback plan ready in case something goes wrong.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

SSH key-based authentication is more secure because it uses a pair of cryptographic keys instead of a password. Private keys are much harder to guess or crack with brute-force attacks, and they are never sent over the network during authentication. This makes unauthorized access much more difficult than using passwords alone.
---

**2. Why should only required ports be open on a production server?**

Only the ports that are needed should be open because every open port is a possible entry point for attackers. Closing unnecessary ports reduces the server's attack surface and lowers the risk of unauthorized access or exploitation.

---

**3. Why is it important for Nginx to be enabled on boot?**

Enabling Nginx on boot ensures that the web server starts automatically whenever the server is restarted. This helps keep the application available without requiring someone to log in and start the service manually after every reboot.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Sharing secrets, SSH keys, passwords, or API credentials publicly can allow unauthorized users to access servers, applications, or cloud resources. This could lead to data theft, service disruption, financial losses, or complete compromise of the system. Sensitive credentials should always be kept private and stored securely.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Cloud resources should be stopped or terminated when they are no longer needed to avoid unnecessary costs and reduce security risks. Leaving unused virtual machines or services running can increase cloud charges and create additional systems that could be targeted by attackers. Cleaning up unused resources is a good practice for both cost management and security.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`__________________________`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*