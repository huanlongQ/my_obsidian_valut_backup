# cmd & powershell

Windows `cmd`可以执行 **`C:\Windows\System32\`** dir下的可执行程序`.exe`. 

# powershell only 

# linux 

~~~
ssh admin admin2 gpunode44
ls -lh /public/software # here shows our compiler kernel
nohup /public/software/Python-3.8.12/bin/python3.8  .py > output.log 2>&1 &
ps aux | grep  .py
nohup python mcmcpotts.py 2>&1 | tee output.log &
Ctrl + R
~~~

## 🖥️ 1. **Navigation**

|Command|What it does|
|---|---|
|`pwd`|Print current working directory|
|`ls` / `ls -lh`|List files (human-readable)|
|`cd foldername`|Change directory|
|`cd ..`|Go up one level|
|`cd ~`|Go to home directory|

---

## 📂 2. **File & Directory Handling**

| Command                        | What it does            |
| ------------------------------ | ----------------------- |
| `mkdir new_folder`             | Create folder           |
| `touch file.txt`               | Create empty file       |
| **`cp file.txt backup.txt`**   | Copy file               |
| **`mv file.txt folder/`**      | Move file               |
| `rm file.txt` / `rm -r folder` | Delete file / folder    |
| **`cat file.txt`**             | **Print file contents** |
| `less file.txt`                | Scroll through file     |

---

## 🧠 3. **Process & Job Control**

| Command          | What it does                                     |
| ---------------- | ------------------------------------------------ |
| **`ps aux`**     | Show running processes                           |
| `top` or `htop`  | Live system monitor                              |
| **`kill PID`**   | Kill process by PID                              |
| **`qstat`**      | Show queue jobs (PBS/Torque)                     |
| **`qdel JOBID`** | Cancel a queued/running job                      |
| `&`              | Run command in background (e.g. `python a.py &`) |
| **`Ctrl+C`**     | Stop a running command                           |

---

## ⚙️ 4. **System Info & Tools**

|Command|What it does|
|---|---|
|`which python3`|Show path to python binary|
|`python3 --version`|Show Python version|
|`echo $PATH`|Show current search path|
|`df -h`|Disk space usage|
|`du -sh folder/`|Size of a folder|

---

## 📦 5. **Package & Env Management (Python)**

|Command|What it does|
|---|---|
|`pip install package`|Install a Python package|
|`python3 -m venv myenv`|Create virtual environment|
|`source myenv/bin/activate`|Activate it|
|`deactivate`|Leave environment|

---

## 📁 6. **Searching and Editing**

| Command                        | What it does                         |
| ------------------------------ | ------------------------------------ |
| **`grep "text" file.txt`**     | Find lines with "text"               |
| `find . -name "*.py"`          | Find all `.py` files in current tree |
| `nano file.py` / `vim file.py` | Edit file in terminal                |

---

## 🛜 7. **Networking & Remote**

|Command|What it does|
|---|---|
|`ssh user@host`|Login to remote machine|
|`scp file user@host:/path/`|Copy file to remote|
|`scp user@host:/path/file .`|Download file from remote|

---

## 🚀 Bonus: Shell Tricks

| Command        | What it does                         |
| -------------- | ------------------------------------ |
| `!python`      | Run previous python command          |
| `history`      | Show command history                 |
| **`Ctrl + R`** | Search command history interactively |
| `tab` (twice)  | Autocomplete file or command         |
|                |                                      |

## 8. nohup 🧠 What is `nohup`?

**`nohup`** stands for **"no hang up"**. It's a Linux command that lets you **run a command in the background** even after you **log out or close the terminal**.

---

### 🔧 Why use `nohup`?

Normally, if you run a command over SSH and then disconnect, the process stops. But with `nohup`, it **keeps running** even after logout.

---

### 🛠️ Basic Usage

`nohup your-command &`

- `nohup`: Prevents the command from stopping when you log out.
    
- `&`: Runs the command **in the background**.
    
- Output (stdout + stderr) goes to a file called `nohup.out` by default.

---

### ✅ Example

`nohup python3 myscript.py &`

- This runs `myscript.py` in the background.
    
- Output goes to `nohup.out`.

---

### 📄 Redirect Output (optional)

`nohup python3 myscript.py > output.log 2>&1 &`

- `> output.log`: Standard output goes to `output.log`.
    
- `2>&1`: Redirects error output (stderr) to the same place.
    
- `&`: Runs in background.

---

### 📍 Check Running Process

`ps aux | grep myscript.py`

Or check background jobs:

`jobs -l`

---

### ❌ Stop a `nohup` Process

Find the process ID (PID), then kill it:

`ps aux | grep myscript.py kill PID`

---

### 🔁 Combine with SSH

You can start a long-running script over SSH like this:

`ssh user@server nohup ./long_task.sh > task.log 2>&1 & exit`

It keeps running after you disconnect.

---

# CLI + 

## **`C:\Windows\System32\`**

Windows `cmd`可以执行 **`C:\Windows\System32\`** dir下的可执行程序`.exe`. 

```cmd
code
explorer
conda
```

## VScode cmd prompt 

- key: `Ctrl + Alt + P` 
