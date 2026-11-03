# Task 06: Copy Files Owned by a Specific User

## 📌 Task Overview

As part of the Nautilus project in the Stratos Datacenter, the production support team accidentally mixed user data.

The task was to identify all regular files owned by the user `siva` inside `/home/usersdata` on App Server 1 and copy them to `/news`, preserving the original directory structure.

## 🎯 Requirements

- **Server:** App Server 1 (`stapp01`)
- **Datacenter:** Stratos
- **Source Directory:** `/home/usersdata`
- **Target User:** `siva`
- **Destination Directory:** `/news`
- **Operation:** Copy files (not move).
- **Preserve:** Original directory structure.
- **Exclude:** Directories.

## 🛠️ Implementation Steps

### Step 1: Connect to App Server 1

```bash
ssh tony@stapp01
```

### Step 2: Find Files Owned by User `siva`

```bash
sudo find /home/usersdata -type f -user siva
```

**Explanation:**
- `find`: Searches for files and directories.
- `/home/usersdata`: Starting directory.
- `-type f`: Selects regular files only.
- `-user siva`: Filters files owned by user `siva`.

### Step 3: Create Destination Directory

```bash
sudo mkdir -p /news
```

The `mkdir -p` command creates the destination directory if it does not already exist.

### Step 4: Copy Files While Preserving Directory Structure

```bash
sudo find /home/usersdata -type f -user siva \
-exec cp --parents {} /news/ \;
```

**

