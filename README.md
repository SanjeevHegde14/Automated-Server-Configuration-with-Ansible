# Automated Server Configuration with Ansible
This project automates the complete setup of a new Linux web server using Ansible, following modular and reusable role-based automation practices. It provisions a secure, production-ready environment by configuring user access, security tools, and a web server to host static web applications.

The playbook is designed for quick and repeatable deployment of a web server on Azure (or any cloud platform).
It ensures system updates, enforces SSH key-based authentication, installs essential packages like fail2ban for security, and deploys a static website automatically using Nginx.

## What it Does

This playbook runs 5 modular roles to:
* **base**: Updates all server packages and installs `fail2ban` for security.
* **user**: Creates a new admin user (`ansible_admin`) with `sudo` privileges.
* **ssh**: Adds a local SSH public key to the `root` user for secure access.
* **nginx**: Installs and starts the Nginx web server.
* **app**: Deploys a static website from a local `site.tar.gz` package.

## Prerequisites

Before running this playbook, you need a target Linux server with:
1. Passwordless SSH Access: Your local machine's public SSH key must be on the server.

2. Open Firewall Ports: The server's cloud firewall (like Azure or AWS) must allow inbound traffic on:
- TCP/22 (for SSH / Ansible)
- TCP/80 (for the Nginx website)
<img width="587" height="358" alt="Screenshot 2025-10-30 190939" src="https://github.com/user-attachments/assets/e8c07b6b-2131-409a-9b27-bc047c164e2c" />

## How to Run

1.  **Create your `inventory.ini` file:**
    *(This file is in .gitignore for security, so you must create it locally).*
    ```ini
    [servers]
    my_server ansible_host=YOUR_IP ansible_user=YOUR_USER
    ```

2.  **Run the full playbook:**
    ```bash
    ansible-playbook -i inventory.ini setup.yml
    ```
    

3.  **Run only a specific part (e.g., to re-deploy the app):**
    ```bash
    ansible-playbook -i inventory.ini setup.yml --tags "app"
    ```


