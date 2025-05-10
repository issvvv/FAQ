## SELinux Commands FAQ

### General Status & Audit
- **`sestatus`** — Show SELinux status and mode.
- **`ausearch -m avc -ts recent --raw`** — Show recent AVC denials.
- **`semanage permissive -l`** — List all domains (services) in permissive mode.

### Permissive Mode Control
- **`semanage permissive -a <custom_policy_name>`** — Add domain to permissive mode.
- **`semanage permissive -d <custom_policy_name>`** — Remove domain from permissive mode.

### Context & Service Inspection
- **`ls -Z /var/log/audit/audit.log`** — Check the SELinux context of a file.
- **`ps -eZ | grep <service_name>`** — View SELinux contexts of a specific service.

### Policy Module Creation
- **`semodule -i <custom_policy_name>`** — Install policy module from AVC denials.
- **`audit2allow -a -M <custom_policy_name>`** — Generate policy module from denials.

### Restore Context
- **`restorecon -v /var/log/audit/audit.log`** — Restore default SELinux context for a file.

### Denial Search Examples
- **`grep "avc:.*denied.*" -i /var/log/audit/audit.log`** — Search for AVC denials in audit logs.
- **`grep "avc:.*denied.*auditd_log_t" /var/log/audit/audit.log | audit2allow -M rsyslog_audit`** — Generate policy for a specific service denial.

### Boolean for Rsyslog
- **`setsebool -P rsyslog_read_audit_log 1`** — Allow rsyslog to read audit logs.

### Context Reassignment (Not Recommended)
- **`semanage fcontext -a -t syslog_log_t "/var/log/audit/audit.log"`** — Change SELinux context of a file (e.g., from `audit_log_t` to `syslog_log_t`).

### Apply Policy Immediately
- **`load_policy`** — Apply the SELinux policy immediately.

---

### Compilation Steps
- **`seinfo -c <class_name>`** — Check class availability (e.g., `"file"`).
- **`checkmodule -M -m -o <custom_policy_name>.mod <custom_policy_name>.te`** — Compile `.te` file to `.mod`.
- **`semodule_package -o <custom_policy_name>.pp -m <custom_policy_name>.mod`** — Package the compiled policy into a `.pp` file.
- **`semodule -i <custom_policy_name>.pp`** — Install the compiled policy module.
- **`semodule -l | grep <custom_policy_name>`** — Verify that the policy module is installed.

---

### Useful Troubleshooting
- **`getenforce`** — Quickly check if SELinux is in Enforcing, Permissive, or Disabled mode.
- **`setenforce 0|1`** — Temporarily switch SELinux mode to Permissive (0) or Enforcing (1) without rebooting.
- **`journalctl -t setroubleshoot`** — View parsed AVC denials (if `setroubleshoot` is installed).
- **`sesearch -A -s <domain> -t <target_type> -c <class> -p <perm>`** — Query existing SELinux rules using `policycoreutils`.

### Recommended Practices
- **Avoid disabling SELinux** — Prefer using Permissive mode or writing a custom policy instead of disabling SELinux entirely.
- **Use `audit2allow` with caution** — Review the generated policies carefully before applying them.
- **Track changes** — Keep `.te` policy files under version control for traceability and audit purposes.