# Automated-Server-Configuration-with-Ansible
Status: 🚧 Project in Progress 🚧

Project Goal

To develop a set of modular and reusable Ansible roles for the complete and automated configuration of a secure Linux web server. This project demonstrates Infrastructure as Code (IaC) principles and best practices for configuration management, enabling consistent, repeatable, and secure server provisioning.

Planned Tech Stack

Configuration Management: Ansible

Target Operating System: Ubuntu 22.04

Core Services: Nginx, Git, Fail2Ban

Planned Architecture & Roles

This repository will contain a collection of independent Ansible roles, each responsible for a specific component of the server configuration:

common Role: Handles baseline server setup, including updating packages, setting the timezone, and hardening user access.

security Role: Implements essential security measures by installing and configuring fail2ban to prevent brute-force attacks and setting up basic firewall rules.

nginx Role: Installs, configures, and manages the Nginx web server.

webapp-deploy Role: A powerful role designed to automatically deploy a web application by:

Cloning a specified Git repository.

Installing any necessary dependencies.

Configuring Nginx to serve the application.

A master playbook.yml file will be used to orchestrate these roles, allowing for a one-command, idempotent provisioning of a complete web server from a bare OS.
