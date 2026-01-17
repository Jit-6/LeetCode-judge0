# Steps to install Judge0 in windows

## Step 1: Install WSL (Windows Subsystem for Linux) + Ubuntu 

WSL lets you run Linux inside Windows.

### 1️⃣ Open PowerShell as Administrator

1. Press Windows Key

2. Type PowerShell

3. Right-click Windows PowerShell

4. Click Run as Administrator

### 2️⃣ Install WSL + Ubuntu

In PowerShell, paste this command and press Enter:
`wsl --install`

What this does:

 - Installs WSL

 - Installs Ubuntu Linux

 - Enables required Windows features


### 3️⃣ Restart Your Computer (IMPORTANT)

After installation finishes:

**Restart your PC**

This step is mandatory. Do NOT skip it.

### 4️⃣ Open Ubuntu Terminal After Restart

After your computer restarts:


- Press Windows Key

- Type Ubuntu

- Click Ubuntu App

A black terminal window will open.

This is your Linux terminal running inside Windows.


### 5️⃣ Create Linux Username and Password

When Ubuntu opens for the first time, it will ask:

1. Enter new UNIX username:

What to do:

Type any username (example: jit)

Press Enter

Then:

2. Enter new UNIX password:

Important:

Password will NOT show while typing (this is normal)

Type password → Press Enter

Re-type password → Press Enter

Now Ubuntu setup is complete.

### 6️⃣ Update Ubuntu System

Inside the Ubuntu terminal, run:

`sudo apt update && sudo apt upgrade -y`


What this does:

Updates package list

Installs latest security updates

It may ask:

Do you want to continue? [Y/n]


Type:

Y


Press Enter

Wait until it finishes.

## ⚙️ Fix Docker cgroup Compatibility

This helps avoid Docker errors on some systems.

### 1️⃣ Open GRUB Configuration File

Run:

`sudo nano /etc/default/grub`

### 2️⃣ Edit This Line

Find:

**GRUB_CMDLINE_LINUX=""**


Change it to:

`GRUB_CMDLINE_LINUX="systemd.unified_cgroup_hierarchy=0"`

### 3️⃣ Save the File

Press:

CTRL + O → Press Enter (Save)

CTRL + X (Exit)

### 4️⃣ Update and Restart Ubuntu

Run:

sudo update-grub
sudo reboot


Your Ubuntu terminal will close.

### 5️⃣ Open Ubuntu Again

After reboot:

Press Windows Key

Type Ubuntu

Click Ubuntu app again

## 🐳 Step 2: Install Docker and Docker Compose

Docker is required to run Judge0 services.

### 1️⃣ Install Docker Engine

Inside Ubuntu terminal:

sudo apt update
sudo apt install -y docker.io


Wait until installation completes.

### 2️⃣ Install Docker Compose

Run:

sudo apt install -y docker-compose

### 3️⃣ Start Docker Service

Run:

sudo service docker start


Check if Docker is working:

docker --version


You should see something like:

Docker version 24.x.x

## Step 3: Install and Run Judge0

Now we will download Judge0 and start its services.

### 1️⃣ Download Judge0

Run:

`wget https://github.com/judge0/judge0/releases/download/v1.13.1/judge0-v1.13.1.zip`

### 2️⃣ Install Unzip Tool (If Not Installed)
sudo apt install unzip -y

### 3️⃣ Extract Judge0 Files

Run:

`unzip judge0-v1.13.1.zip`


A folder will be created.

### 4️⃣ Open Judge0 Folder
cd judge0-v1.13.1

### 5️⃣ Configure Passwords (Important)

Open environment config file:

nano .env

Find These Lines:
REDIS_PASSWORD=
POSTGRES_PASSWORD=



REDIS_PASSWORD=enter_a_password_for_redis
POSTGRES_PASSWORD=enter_a_password_for_postgres


**Use different passwords for Redis and Postgres.**

Save and Exit:

CTRL + O → Enter

CTRL + X

### ▶️ Step 4: Start Judge0 Services

- 1️⃣ Start Database and Redis

Run:

docker-compose up -d db redis

- 2️⃣ Wait 10 Seconds

Run:

`sleep 10`

- 3️⃣ Start All Services

Run:

docker-compose up -d

- 4️⃣ Wait Again
sleep 5

###  Step 5: Verify Judge0 Is Working
Open Browser (Chrome / Edge)

Go to:

http://localhost:2358/docs

🎉 If You See:

👉 Judge0 Swagger API page
👉 API endpoints listed

That means:

Judge0 is running successfully!

### How to Stop Judge0
docker-compose down

### How to Restart Judge0
docker-compose up -d

### How to Check Running Containers
docker ps
