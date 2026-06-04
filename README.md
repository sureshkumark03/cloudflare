# Cloudflare Static Site & CI/CD Pipeline

A streamlined boilerplate repository demonstrating how to host, style, and automatically deploy a responsive static website using **Cloudflare**, **AWS EC2**, and **GitHub Actions**.

This repository serves as a starting point for setting up an automated DevOps pipeline that pushes frontend updates seamlessly from code to production.

---

## 🚀 Features

* **Production-Ready Frontend:** Lightweight static page structured with vanilla `index.html` and styled via `style.css`.
* **Automated CI/CD:** Powered by GitHub Actions (`github-actions-ec2.yml`) to handle automated testing and deployment workflows upon pushing to the repository.
* **Cloudflare Integration:** Built to leverage Cloudflare's global DNS, CDN benefits, and security proxy features for fast, secure content delivery.

---

## 📂 Project Structure

```text
├── .github/workflows/
│   └── github-actions-ec2.yml  # CI/CD pipeline configuration for deployment
├── index.html                  # Main website landing page
├── style.css                   # Custom UI styling sheet
└── README.md                   # Project documentation

---

## 🛠️ Prerequisites

Before utilizing the CI/CD pipeline, ensure you have the following components and configurations in place:

### 1. Infrastructure Setup
* **AWS EC2 Instance:** A running Linux instance (e.g., Ubuntu) acting as your web server.
* **Web Server:** Nginx or Apache installed and running on your EC2 instance, configured to serve files from your target deployment directory (e.g., `/var/www/html`).
* **Cloudflare Configuration:** Your custom domain must be added to Cloudflare, with DNS records pointing to your AWS EC2 instance's public IP address.

### 2. Network & Security Access
* **Inbound SSH Access:** Ensure your EC2 security group allows inbound SSH traffic (**Port 22**). *Tip: For enhanced security, restrict access to GitHub Actions IP ranges or utilize a secure proxy.*
* **SSH Key Pair:** A valid SSH private key configured on your local machine that grants access to your EC2 instance.

---

## 🤖 CI/CD Deployment Pipeline

The workflow defined in `.github/workflows/github-actions-ec2.yml` automates the entire deployment process. Every time a commit is pushed to the main branch, GitHub Actions safely transfers the updated static files directly to your server.

### Pipeline Workflow Steps
1. **Trigger:** The workflow is initiated by a `push` event to the primary branch.
2. **Environment Setup:** Runner initializes and checks out the latest repository code.
3. **Authentication:** Establishes a secure SSH connection to the AWS EC2 instance using your configured secrets.
4. **Deployment:** Syncs the `index.html` and `style.css` files to the target web directory on the server (e.g., via `rsync` or `scp`).
5. **Post-Deployment:** Clears or restarts any necessary server caches to ensure changes reflect immediately behind the Cloudflare proxy.

### Required GitHub Secrets
To make the pipeline function securely without exposing credentials, add the following parameters under your GitHub Repository **Settings > Secrets and variables > Actions**:

| Secret Name | Description | Example / Format |
| :--- | :--- | :--- |
| `EC2_HOST` | The public IP address or public DNS of your EC2 instance. | `54.210.xx.xx` or `ec2-xx.compute.amazonaws.com` |
| `EC2_USERNAME` | The default SSH admin user for your server OS. | `ubuntu` (for Ubuntu) or `ec2-user` (for Amazon Linux) |
| `SSH_PRIVATE_KEY` | The entire contents of your private `.pem` key file. | `-----BEGIN RSA PRIVATE KEY----- ...` |

---

## 💻 Local Development

To test or edit this website locally on your machine:

1. Clone the repository:
   ```bash
   git clone [https://github.com/sureshkumark03/cloudflare.git](https://github.com/sureshkumark03/cloudflare.git)
2. Navigate into the directory:
cd cloudflare
3. Open index.html directly in any web browser or run it using a local development server extension (like Live Server in VS Code).

License
This project is open-source and available under the MIT License.
