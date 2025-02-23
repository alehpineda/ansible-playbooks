# ansible-playbooks

Homelab Ansible Playbooks

This repository contains a collection of Ansible playbooks to manage and secure your homelab environment. The playbooks cover tasks such as updating APT packages, installing and configuring Docker (including Docker Compose), hardening SSH configurations, and managing UFW firewall rules.

## Directory Structure

- **playbooks/**  
  Contains individual playbooks:
  - `apt_update.yml` – Update and upgrade APT packages.
  - `install_docker.yml` – Install Docker, Docker Compose, and perform post-installation steps.
  - `harden_ssh.yml` – Harden the SSH configuration by updating `/etc/ssh/sshd_config` and applying firewall rules.
  - `enable_ufw.yml` – Install, enable, and configure UFW for SSH ports.
  - `remove_docker_armv6.yml` – Undo Docker installation (intended for hosts with ARMv6 architecture).

- **inventory/**  
  Contains your inventory files and group variables:
  - `inventory_lan.ini` – Inventory definition for all hosts.
  - `group_vars/` – Contains variables for groups (e.g., `ubuntu_lts.yml` and `all_hosts.yml`).

- **.ansible/**, **.gitignore**, **LICENSE**  
  Additional repository configuration files.

## Prerequisites

- **Ansible installed on your control machine.**
- **Linux-based hosts** are assumed.
- Each host should have Python installed.
- (Optional) Vault password if you are using Ansible Vault for sensitive variables. Use the `--ask-vault-pass` option when running playbooks.

## How to Use

1. **Clone this repository:**

   ```bash
   git clone <repository_url>
   cd ansible-playbooks

Below is an example README that explains how to use the codebase:

```md
# ansible-playbooks

Homelab Ansible Playbooks

This repository contains a collection of Ansible playbooks to manage and secure your homelab environment. The playbooks cover tasks such as updating APT packages, installing and configuring Docker (including Docker Compose), hardening SSH configurations, and managing UFW firewall rules.

## Directory Structure

- **playbooks/**  
  Contains individual playbooks:
  - `apt_update.yml` – Update and upgrade APT packages.
  - `install_docker.yml` – Install Docker, Docker Compose, and perform post-installation steps.
  - `harden_ssh.yml` – Harden the SSH configuration by updating `/etc/ssh/sshd_config` and applying firewall rules.
  - `enable_ufw.yml` – Install, enable, and configure UFW for SSH ports.
  - `remove_docker_armv6.yml` – Undo Docker installation (intended for hosts with ARMv6 architecture).

- **inventory/**  
  Contains your inventory files and group variables:
  - `inventory_lan.ini` – Inventory definition for all hosts.
  - `group_vars/` – Contains variables for groups (e.g., `ubuntu_lts.yml` and `all_hosts.yml`).

- **.ansible/**, **.gitignore**, **LICENSE**  
  Additional repository configuration files.

## Prerequisites

- **Ansible installed on your control machine.**
- **Linux-based hosts** are assumed.
- Each host should have Python installed.
- (Optional) Vault password if you are using Ansible Vault for sensitive variables. Use the `--ask-vault-pass` option when running playbooks.

## How to Use

1. **Clone this repository:**

   ```bash
   git clone <repository_url>
   cd ansible-playbooks
   ```

2. **Review and modify variables:**

   - Check inventory_lan.ini to ensure the correct hosts, usernames, and hostnames.
   - Review group variables in group_vars for SSH keys or vault passwords if needed.

3. **Running a playbook:**

   For example, to update and upgrade APT packages across your hosts:

   ```bash
   ansible-playbook -i inventory/inventory_lan.ini playbooks/apt_update.yml
   ```

   To install Docker and Docker Compose:

   ```bash
   ansible-playbook -i inventory/inventory_lan.ini playbooks/install_docker.yml
   ```

   To harden your SSH configuration on targeted hosts:

   ```bash
   ansible-playbook -i inventory/inventory_lan.ini playbooks/harden_ssh.yml
   ```

4. **Vault Usage:**

   If you encounter encrypted values (for example in ubuntu_lts.yml), run playbooks using:

   ```bash
   ansible-playbook -i inventory/inventory_lan.ini playbooks/<playbook_name>.yml --ask-vault-pass
   ```

5. **Managing UFW:**

   To install and configure UFW on your hosts, run:

   ```bash
   ansible-playbook -i inventory/inventory_lan.ini playbooks/enable_ufw.yml
   ```

## Additional Information

- **Docker on ARMv6 Hosts:**  
  The install_docker.yml includes a variable (`skip_docker_armv6`) to automatically skip Docker installation on ARMv6 hosts.

- **Backup and Revert:**  
  Playbooks like harden_ssh.yml use the `backup` parameter to create backups (e.g., for `/etc/ssh/sshd_config`) before making changes. There is also a playbook (`remove_docker_armv6.yml`) to undo Docker installations for specific host architectures.

- **License:**  
  This code is distributed under the GNU General Public License, Version 3. See the LICENSE file for details.

## Contributing

Feel free to contribute by submitting issues or pull requests to improve these playbooks or adapt them to new environments.

---
Happy automating!
