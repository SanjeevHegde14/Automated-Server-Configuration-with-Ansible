# Automated Server Configuration with Ansible

This project automates the configuration of a new Linux web server using Ansible.

## What it Does

This playbook runs 5 modular roles to:
* **base**: Updates all server packages and installs `fail2ban` for security.
* **user**: Creates a new admin user (`ansible_admin`) with `sudo` privileges.
* **ssh**: Adds a local SSH public key to the `root` user for secure access.
* **nginx**: Installs and starts the Nginx web server.
* **app**: Deploys a static website from a local `site.tar.gz` package.

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
