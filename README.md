# 🏠 Home Assistant OS Automated Deployment via Ansible on Proxmox

This Ansible playbook automates the **deployment of a Home Assistant OS VM** on a **Proxmox hypervisor** using the `qm` CLI.  
It is **idempotent**, supports **safe re-runs**, and performs the following tasks automatically:

- Downloads the latest **Home Assistant OS** image  
- Imports it as a disk in Proxmox storage  
- Creates and configures the VM  
- Enables the **guest agent**  
- Reports the VM’s **private IP** for browser-based management  

---

## ⚙️ Requirements

- **Proxmox VE** running on your target hypervisor  
- **Password-based SSH access** to the Proxmox host for the provided user  
- **Ansible** installed on the control machine (`ansible-core >= 2.10` recommended)  
- `unxz` utility available on the Proxmox host  
- `qm` CLI in the system `$PATH`

---

## 🧩 Variables

Edit the variables at the top of the playbook before running:

```yaml
proxmox_host: "enter_proxmox_ip_here"
proxmox_user: "proxmox_user_name"
proxmox_password: "proxmox_user_password"
vmid: enter_vm_id_here
vm_name: enter_vm_name_here
storage: local-lvm
memory: 4096
cores: 2
sockets: 1

```

---

## 🚀 Usage

1. Clone this repository or copy the playbook to your control machine

2. Edit the playbook variables as described above.

3. Run the playbook: ansible-playbook homeassistant_proxmox.yml

4. At the end of the playbook run, the VM's private IP address will be printed in the terminal.

---

## 🌐 Accessing the Home Assistant GUI

1. Wait for the Home Assistant OS VM to fully boot.

2. Open a web browser on a device in the same network.

3. Visit: http://VM-PRIVATE-IP:8123

Replace `<VM-PRIVATE-IP>` with the IP shown by the playbook.

🕒 The initial boot may take a few minutes. If the setup wizard doesn’t appear right away, wait and retry.

---

## 🛡️ Notes

- The playbook is safe for repeated runs (idempotent).
- Use a unique vmid for each VM instance.
- For advanced customization (VM resources, network, storage), modify the variables or shell commands in the playbook.
- All tasks are executed directly on the Proxmox host via SSH.

---

## 🧰 Troubleshooting

- If the guest agent is not installed inside the VM, private IP discovery will not work.
- If you cannot access the GUI:
- Ensure the VM is running.
- Verify the correct network bridge is used.
- Check there are no firewall rules blocking port 8123 between your workstation and the VM.

---

## 🔢 Default Home Assistant Web UI Port -> 8123

---

## 🤝 Contributions

This playbook is production-ready and suitable for Proof-of-Concept (PoC) setups.  
Contributions and pull requests are always welcome!
