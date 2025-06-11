# Ansible Automation: System Patching and Nginx Deployment

## 📌 Project Overview
This project automates system updates and installs Nginx using Ansible on a local Rocky Linux 8 VM. It demonstrates infrastructure-as-code practices and includes both `cron` and `systemd` timer-based scheduling for repeatable, auditable execution.

## 🛠️ Features
- Full system package update via Ansible
- Nginx installation and service configuration
- Firewalld HTTP service enablement
- Automation via systemd timer or cron job
- Uses local inventory with privilege escalation (`become: yes`)

## 📁 File Structure
ansible-automation-patching/\
├── README.md\
├── inventory.ini\
├── update_system.yml\
├── run_patch.yml.sh\
├── systemd/ \
│ ├── patch-playbook.service\
│ └── patch-playbook.timer\
├── logs/ (optional)\
│ └── example_output.log\
└── docs/ (optional)\
└── screenshots/ 


## 🔧 File Descriptions

| File/Dir                    | Description |
|----------------------------|-------------|
| `inventory.ini`            | Static inventory targeting `localhost` |
| `update_system.yml`        | Main Ansible playbook for patching and Nginx setup |
| `run_patch.yml.sh`         | Shell wrapper to invoke the playbook |
| `systemd/*.service`        | One-shot unit to trigger the playbook |
| `systemd/*.timer`          | Timer unit to run service on schedule |
| `logs/`                    | Output logs from cron or systemd (optional) |
| `docs/screenshots/`        | Validation images or diagrams (optional) |

## 📅 Scheduling Options

### Cron Example
```cron
0 3 * * 0 ansible-playbook ~/ansible/projects/patching/update_system.yml -i ~/ansible/projects/patching/inventory.ini >> ~/ansible/projects/patching/ansible_cron.log 2>&1

systemd Timer Example
systemctl --user enable --now patch-playbook.timer

To view logs:
journalctl --user-unit=patch-playbook.service
```

## ✅ Validation Checklist
- dnf history shows recent update
- systemctl status nginx confirms service is running
- curl http://localhost returns HTTP 200
- firewall-cmd --list-services shows http

## Video Walkthrough
[![Watch the Video](https://github.com/rvq619/ansible-automation-patching/blob/main/ansible_automation_screen.png)](https://youtu.be/9LvceN8wEQ8)

## 👤 Author
Ryan Quisumbing \
San Diego, CA \
[LinkedIn](http://linkedin.com/in/ryan-quisumbing)
