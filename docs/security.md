# Linux security hardening

I wanted to make my Ubuntu system more secure and, more importantly, understand what was already running on it before changing anything.

I treated this as a learning project. I checked the current system, changed some settings, and then checked the result again.

Some parts of the original security plan were not finished before I cancelled the project. I do not want to write them as if I actually completed them.

## What I planned to check

The security work was based around:

- system information,
- users and permissions,
- running services,
- open ports,
- SSH,
- UFW,
- AppArmor,
- automatic updates,
- Fail2ban,
- audit logging.

I also wanted to compare the system before and after the changes.

---

# 1. System audit

Before changing security settings, I collected information about the system.

## Ubuntu version

I checked the Ubuntu version with:

```bash
lsb_release -a
```

This tells me which Ubuntu release I am working with.

## Package updates

I refreshed the package information:

```bash
sudo apt update
```

Then I checked available upgrades:

```bash
apt list --upgradable
```

I updated the system before continuing with the security configuration.

## Current user

I checked which user I was logged in as:

```bash
whoami
```

I also checked the groups of the current user:

```bash
groups
```

This showed whether the account had administrative access through the `sudo` group.

## Users

To see the users configured on the system:

```bash
cut -d: -f1 /etc/passwd
```

I looked for accounts that I did not recognize or no longer needed.

## Running services

I checked the services that were currently running:

```bash
systemctl list-units --type=service --state=running
```

I was mainly looking for services that I recognized and services that I did not need.

A service being unfamiliar does not automatically mean that it is dangerous. I should first find out what it does before disabling it.

## Open ports

I checked listening TCP and UDP ports with:

```bash
sudo ss -tulpn
```

The options mean:

- `t` = TCP
- `u` = UDP
- `l` = listening
- `p` = process
- `n` = show numbers instead of resolving names

I found ports used by Web Services Dynamic Discovery (`wsdd`). I did not disable the service because I had not found a reason that I needed to remove it.

The better way to decide whether a port should stay open is to identify the service, find out why it is running, and check whether I actually need it.

---

# 2. UFW firewall

I checked whether UFW was installed:

```bash
ufw --version
```

It was already installed.

If it is not installed, I can install it with:

```bash
sudo apt install ufw
```

I checked the current firewall status:

```bash
sudo ufw status verbose
```

The firewall was inactive.

## Firewall rules

I set the default policy to deny incoming connections and allow outgoing connections:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Before enabling the firewall, I allowed SSH:

```bash
sudo ufw allow ssh
```

I did this before enabling UFW because I wanted SSH access to continue working after the firewall was activated.

I checked the rules:

```bash
sudo ufw status
```

Then I enabled the firewall:

```bash
sudo ufw enable
```

Finally I checked the detailed status:

```bash
sudo ufw status verbose
```

The important part is to check the rules before enabling the firewall. Otherwise it is possible to block the connection that I am using to manage the computer.

---

# 3. SSH

I checked whether the SSH service was installed:

```bash
systemctl status ssh
```

At first the service was not installed and the system returned:

```text
Unit ssh.service could not be found.
```

I installed OpenSSH Server:

```bash
sudo apt update
sudo apt install openssh-server
```

Then I checked the service again:

```bash
systemctl status ssh
```

SSH was now running.

Because I had already allowed SSH in UFW, I did not create another firewall rule for it.

## Check SSH configuration

Before changing the SSH configuration, I checked the current values:

```bash
sudo sshd -T | grep -E "permitrootlogin|passwordauthentication|port"
```

This shows the effective values for:

- SSH port
- root login
- password authentication

I wanted to record these values before making any hardening changes.

## SSH hardening status

I did not finish the planned SSH hardening before I cancelled this project.

The planned next steps were:

- create SSH key authentication,
- test the key login,
- disable root login,
- disable password authentication,
- test the connection again.

I am leaving these as unfinished instead of claiming they were completed.

---

# 4. AppArmor

I checked whether AppArmor was active:

```bash
sudo aa-status
```

The output showed that the AppArmor kernel module was loaded and that profiles were available.

The check on my system showed:

```text
234 profiles are loaded.
154 profiles are in enforce mode.
5 profiles are in complain mode.
75 profiles are in unconfined mode.
```

The full `aa-status` output is very long, so I do not need to keep the whole list in this documentation.

The important part for my initial audit was that AppArmor was loaded and profiles were already being used.

`enforce` means AppArmor actively blocks actions that violate the profile.

`complain` records violations without enforcing the restrictions in the same way.

An application being unconfined does not automatically mean that it is unsafe. It means that an AppArmor profile is not currently restricting that application in the normal way.

---

# 5. Automatic updates

I checked the automatic update service with:

```bash
systemctl status unattended-upgrades
```

The service was enabled and active on my system.

I also checked the APT periodic configuration:

```bash
cat /etc/apt/apt.conf.d/20auto-upgrades
```

The relevant automatic update settings were enabled.

If `unattended-upgrades` is not installed, it can be installed with:

```bash
sudo apt update
sudo apt install unattended-upgrades
```

The configuration can then be enabled with:

```bash
sudo dpkg-reconfigure unattended-upgrades
```

I did not need to install it again because it was already working on my system.

---

# 6. Fail2ban

Next I checked whether Fail2ban was installed:

```bash
fail2ban-client --version
```

It was not installed, so I installed it:

```bash
sudo apt install fail2ban
```

Then I enabled and started the service:

```bash
sudo systemctl enable --now fail2ban
```

I checked the service:

```bash
systemctl status fail2ban
```

It should show that the service is running.

## Check the jails

I checked the enabled jails:

```bash
sudo fail2ban-client status
```

I also checked the SSH jail:

```bash
sudo fail2ban-client status sshd
```

The `sshd` jail is the one I used to protect SSH from repeated failed login attempts.

## Configure the SSH jail

I did not edit the default `jail.conf` file directly. Instead I used the local configuration:

```bash
sudo nano /etc/fail2ban/jail.local
```

For this project I enabled the SSH jail:

```ini
[sshd]
enabled = true
```

Then I restarted Fail2ban:

```bash
sudo systemctl restart fail2ban
```

I checked the jails again:

```bash
sudo fail2ban-client status
```

## Check the Fail2ban log

If I need to troubleshoot Fail2ban, I can watch its log with:

```bash
sudo tail -f /var/log/fail2ban.log
```

## Unban an address

If a trusted address gets banned, I can check the SSH jail:

```bash
sudo fail2ban-client status sshd
```

Then remove the ban with:

```bash
sudo fail2ban-client set sshd unbanip IP_ADDRESS
```

## Whitelist trusted addresses

Fail2ban can ignore addresses that I trust.

I should only add addresses that I actually trust. I should also use my real addresses instead of copying example addresses from a guide.

The configuration can be placed in `/etc/fail2ban/jail.local`:

```ini
[DEFAULT]
ignoreip = 127.0.0.1/8 ::1 YOUR_TRUSTED_IP
```

After changing the configuration:

```bash
sudo systemctl restart fail2ban
```

---

# 7. Audit logging

I also planned to use `auditd` for system audit logging.

I checked whether it was installed:

```bash
systemctl status auditd
```

At the time of the audit it was not installed.

I did not finish the auditd part of the project, so I am not documenting it as completed.

The planned work was to install auditd, configure useful rules, generate some events, and check the audit logs.

---

# 8. Security work that was completed

During this project I completed these parts:

- Checked the Ubuntu system before making changes.
- Checked users and sudo access.
- Checked running services.
- Checked listening network ports.
- Installed and enabled UFW.
- Set UFW to deny incoming connections by default.
- Allowed outgoing connections.
- Allowed SSH before enabling UFW.
- Installed OpenSSH Server.
- Checked the effective SSH configuration.
- Checked AppArmor.
- Checked automatic updates.
- Installed and configured Fail2ban for SSH.

# 9. Security work that was not completed

I did not finish:

- SSH key authentication setup.
- Disabling SSH root login.
- Disabling SSH password authentication.
- Full SSH hardening testing.
- auditd configuration.
- Full before/after security comparison.
- Complete Fail2ban attack testing.

The project was cancelled before these parts were finished.

# What I learned

The biggest thing I learned was that security is not only about installing security tools.

Before changing anything, I need to know what is already running and why it is running.

I also learned to be careful with firewalls. If I enable a firewall before allowing the connection I need, I can lock myself out.

The same idea applies to SSH, storage, and other system changes. I should check what I am changing before I run a command with `sudo`.
