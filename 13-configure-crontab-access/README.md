# Task 13 – Configure Crontab Access

## Objective
Configure crontab access on Application Server 2 (`stapp02`) to meet security compliance requirements.

- Allow the `ravi` user to access crontab.
- Deny the `eric` user access to crontab.

## Server Details

| Detail | Value |
|---|---|
| Server | Application Server 2 |
| Hostname | stapp02 |
| SSH User | steve |

## Implementation

### 1. Connect to App Server 2

```bash
ssh steve@stapp02
```

### 2. Allow Ravi

```bash
sudo sh -c 'echo ravi > /etc/cron.allow'
```

### 3. Deny Eric

```bash
sudo sh -c 'echo eric > /etc/cron.deny'
```

### 4. Verify Configuration

```bash
sudo cat /etc/cron.allow
sudo cat /etc/cron.deny
```

Expected output:

**/etc/cron.allow**
```text
ravi
```

**/etc/cron.deny**
```text
eric
```

### 5. Test User Access

```bash
sudo -u ravi crontab -l
sudo -u eric crontab -l
```

Results:

- `ravi`: Access permitted. The message `no crontab for ravi` indicates that no cron jobs currently exist.
- `eric`: Access denied with a permission error.

## Key Learnings

- `/etc/cron.allow` specifies users permitted to access crontab.
- `/etc/cron.deny` specifies users denied access when the allow file does not exist.
- When `/etc/cron.allow` exists, it takes precedence.
- Restricting cron access improves server security.

## Final Result

Successfully configured and verified crontab access on App Server 2.

| User | Access |
|---|---|
| ravi | Allowed |
| eric | Denied |

**Status: Completed**

