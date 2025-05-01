# Manage WSL (Ubuntu 22.04) with Ansible

## WSL Ansible Steps

1. Download Ubuntu-22.04 - Powershell

- Create user and password

2. Export to Create Base WSL - Powershell

```powershell
$NEW_NAME="Base-Ubuntu-22.04"
mkdir c:\Users\$env:USERNAME\wsl\backups
wsl --export Ubuntu-22.04 "C:\Users\$env:USERNAME\wsl\backups\Ubuntu-22.04-base.tar"
wsl --import $NEW_NAME C:\Users\$env:USERNAME\wsl\$NEW_NAME C:\Users\$env:USERNAME\wsl\backups\Ubuntu-22.04-base.tar
wsl --unregister Ubuntu-22.04
```

3. Update Ubuntu-22.04, install ansible and run Ansible Playbook

```powershell
wsl -d $NEW_NAME
apt update
apt install -y ansible
cd /home/USER_NAME
git clone https://github.com/richhorace/wsl-ansible.git
cd wsl-ansible/ansible
ansible-playbook setup-wsl.yml -e default_user=USER_NAME
```

4. Restart New WSl Instance with WLS Terminate

```powershell
wsl --terminate $NEW_NAME
```

5. Test My-Ubuntu-22.04 - Powershell

```powershell
wsl -d $NEW_NAME
ansible
python3
aws --version
```

6. Symlink SSH from Windows to WSL (Optional)

```bash
ln -s /mnt/c/User/USER_NAME/.ssh ~/.ssh
```

## WSL Command Reference

```
# Shows WSL configuration and default version
wsl --status

# Lists installed distros and their WSL version (1 or 2)
wsl --list --verbose
# or
wsl -l -v

# Terminates a running distro (like rebooting the distro)
wsl --terminate <Distro>

# Shuts down all running WSL instances and the WSL VM itself
wsl --shutdown

# CAUTION: Unregisters (deletes) the distro and its data – irreversible
wsl --unregister <Distro>
```
