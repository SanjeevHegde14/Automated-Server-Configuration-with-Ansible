# Automated Server Configuration with Ansible

This project uses Ansible to fully automate the provisioning and configuration of a new Linux web server. This playbook takes a bare-bones server (like a new VM on Azure, AWS, or DigitalOcean) and, in one command, turns it into a secure, production-ready web host.

## What This Playbook Does

This configuration is broken into modular, reusable roles:

* ****: Updates all packages (Reading package lists...) and installs  to protect against brute-force attacks.
* ****: Creates a new admin user named `ansible_admin`, adds them to the `sudo` group, and copies a local public SSH key for access.
* ****: Hardens the `root` user's account by adding the same public SSH key for secure access.
* ****: Installs, enables, and starts the Nginx web server.
* ****: Creates the web directory () and deploys a static web application from a local `site.tar.gz` package.

## How to Use

1.  **Prerequisites:**
    * You need a target Linux server (e.g., Ubuntu 22.04).
    * You need Ansible installed on your local machine (Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: ansible in /home/anteinfierno/.local/lib/python3.10/site-packages (10.7.0)
Requirement already satisfied: ansible-core~=2.17.7 in /home/anteinfierno/.local/lib/python3.10/site-packages (from ansible) (2.17.14)
Requirement already satisfied: PyYAML>=5.1 in /usr/lib/python3/dist-packages (from ansible-core~=2.17.7->ansible) (5.4.1)
Requirement already satisfied: packaging in /home/anteinfierno/.local/lib/python3.10/site-packages (from ansible-core~=2.17.7->ansible) (25.0)
Requirement already satisfied: cryptography in /usr/lib/python3/dist-packages (from ansible-core~=2.17.7->ansible) (3.4.8)
Requirement already satisfied: resolvelib<1.1.0,>=0.5.3 in /home/anteinfierno/.local/lib/python3.10/site-packages (from ansible-core~=2.17.7->ansible) (1.0.1)
Requirement already satisfied: jinja2>=3.0.0 in /usr/lib/python3/dist-packages (from ansible-core~=2.17.7->ansible) (3.0.3)).
    * You must have passwordless SSH access to your server (e.g., by using `ssh-copy-id user@server_ip`).

2.  **Clone this repository:**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name
    ```

3.  **Create your Inventory:**
    This repository's `.gitignore` file correctly ignores the inventory file for security. You must create your own `inventory.ini`:

    ```ini
    [servers]
    my_server ansible_host=YOUR_SERVER_IP ansible_user=YOUR_SSH_USER
    ```

4.  **Run the Playbook:**

    * **To run the entire setup:**
        ```bash
        ansible-playbook -i inventory.ini setup.yml
        ```

    * **To run only a specific role (e.g., to re-deploy the app):**
        ```bash
        ansible-playbook -i inventory.ini setup.yml --tags "app"
        ```
