- Perfect timing — let’s move from **planning → doing**. With *Lab Nexus*, we want to build in layers:
- **Workspace structure** (folders, notes, backups)
- **Core tools** (DBs, networking, automation)
- **Environment setup** (virtualization, containers, configs)
- Here’s a starter plan you can action right away:
  
  ---
- ## 🗂️ Step 1: Folder & Project Structure
  
  Let’s keep it clean so you don’t drown in files. On your main machine (Windows or server), create a top-level directory:
  
  ```
  LabNexus/
  ├─ Databases/
  ├─ Analytics/
  ├─ Networking/
  ├─ Automation/
  ├─ Projects/
  └─ Notes/   (if not only in Logseq)
  ```
  
  👉 Pro tip: symlink this folder into **Logseq** so notes + files are unified. For example, `LabNexus/Notes` could be a Logseq graph root.
  
  ---
- ## ⚙️ Step 2: Core Tools to Install/Configure
- ### **Databases**
- Install **PostgreSQL** (main workhorse).
- Optionally, **Oracle XE** (since you use Oracle at work, it’s good for testing).
- Install **DBeaver** or **pgAdmin** (GUI for DB management).
- ### **Analytics Tools**
- Python environment (`conda` or `venv`):
	- Core libs: `pandas`, `sqlalchemy`, `psycopg2`, `matplotlib`
- Jupyter or VS Code with Python extension.
- Optional: **Apache Superset** or **Metabase** (dockerized dashboards).
- ### **Networking**
- **Wireshark** (packet capture).
- **Nmap** (scanning).
- **iPerf3** (bandwidth tests).
- pfSense/OPNsense VM (VirtualBox/VMWare/Proxmox/Hyper-V).
- ### **Automation (n8n)**
- You already installed locally 🎉
- Consider running it via **Docker** for easier upgrades & persistence.
- Create a folder: `LabNexus/Automation/n8n/` for workflows & backups.
  
  ---
- ## 🖥️ Step 3: Environment Options
  
  Depending on how deep you want to go:
- **Lightweight route:** Install everything directly on your main PC.
- **Clean route:** Use **Docker** to run DBs + tools in containers.
- **Pro route:** Set up a dedicated hypervisor (Proxmox/VMware ESXi) and spin up VMs.
  
  👉 Since you’re already comfortable with Docker and VMs, I’d suggest:
- Docker for DBs + Superset/Metabase/n8n.
- VM (pfSense) for networking practice.
  
  ---
- ## 🚀 Step 4: First Action Items
- Create `LabNexus/` folder structure.
- Install **PostgreSQL** (native or Docker).
- Create a **Python venv** with pandas + sqlalchemy.
- Install **Wireshark** + **nmap**.
- Confirm **n8n** runs (save a test workflow).
  
  That gets you a base environment in place within a weekend.
  
  ---
  
  👉 Do you want me to give you **exact commands/configs** (e.g., Docker compose for Postgres + Superset + n8n), so you can bootstrap the lab in one go?
- Heck yes. Here’s a **copy-paste, one-shot PowerShell bootstrap** for **Lab Nexus** on your Windows 11 + Docker Desktop (WSL2) box. It will:
- Create the `LabNexus/` folder tree
- Write a `.env`, `docker-compose.yml`, and `Analytics\requirements.txt`
- Start **Postgres 16**, **pgAdmin**, **Metabase**, **n8n**, and an **iperf3** server
- Create a **Python venv** with pandas/sqlalchemy/etc.
- (Optional) Install **Wireshark** + **Nmap** using winget (commented—uncomment if you want)
  
  > 
  
  Run PowerShell as your user (admin only needed if you uncomment the winget installs). Make sure Docker Desktop is running.
- # Postgres
  POSTGRES_DB=labnexus
  POSTGRES_USER=labadmin
  POSTGRES_PASSWORD=labsecret
  POSTGRES_PORT=5432
- # Metabase (app DB)
  MB_DB_TYPE=postgres
  MB_DB_DBNAME=metabase
  MB_DB_HOST=postgres
  MB_DB_PORT=5432
  MB_DB_USER=labadmin
  MB_DB_PASS=labsecret
- # pgAdmin
  PGADMIN_DEFAULT_EMAIL=jeff@compoundcreative.ca
  PGADMIN_DEFAULT_PASSWORD=labadmin
- # n8n
  N8N_HOST=localhost
  N8N_PORT=5678
  N8N_PROTOCOL=http
  N8N_EDITOR_BASE_URL=http://localhost:5678
  N8N_API_BASE_URL=http://localhost:5678
  N8N_BASIC_AUTH_ACTIVE=false
  N8N_RUNNERS_ENABLED=true
- # ===== Lab Nexus Bootstrap (Windows 11 + Docker + WSL2) =====
	- ```
	  # ===== Lab Nexus Bootstrap (Windows 11 + Docker + WSL2) =====
	  $ErrorActionPreference = 'Stop'
	  
	  # --- Paths
	  $Root = Join-Path $env:USERPROFILE 'LabNexus'
	  $Dirs = @(
	    'Databases\postgres',
	    'Analytics\notebooks',
	    'Analytics\venv',
	    'Networking\pcaps',
	    'Automation\n8n',
	    'Projects',
	    'Notes'
	  ) | ForEach-Object { Join-Path $Root $_ }
	  
	  Write-Host "Creating folder structure under $Root..."
	  New-Item -ItemType Directory -Path $Root -Force | Out-Null
	  $Dirs | ForEach-Object { New-Item -ItemType Directory -Path $_ -Force | Out-Null }
	  
	  # --- .env for compose (reflects working config)
	  $EnvContent = @'
	  # ===== Lab Nexus .env =====
	  
	  # Postgres
	  POSTGRES_DB=labnexus
	  POSTGRES_USER=labadmin
	  POSTGRES_PASSWORD=labsecret
	  POSTGRES_PORT=5432
	  
	  # Metabase application DB (use Postgres instead of default H2)
	  MB_DB_TYPE=postgres
	  MB_DB_DBNAME=metabase
	  MB_DB_PORT=5432
	  MB_DB_USER=labadmin
	  MB_DB_PASS=labsecret
	  MB_DB_HOST=postgres
	  
	  # pgAdmin (must be a deliverable-looking email)
	  PGADMIN_DEFAULT_EMAIL=jeff@compoundcreative.ca
	  PGADMIN_DEFAULT_PASSWORD=labadmin
	  
	  # n8n
	  N8N_HOST=localhost
	  N8N_PORT=5678
	  N8N_PROTOCOL=http
	  N8N_EDITOR_BASE_URL=http://localhost:5678
	  N8N_API_BASE_URL=http://localhost:5678
	  N8N_BASIC_AUTH_ACTIVE=false
	  # (set these only when enabling basic auth)
	  # N8N_BASIC_AUTH_USER=admin
	  # N8N_BASIC_AUTH_PASSWORD=<strong-password>
	  N8N_RUNNERS_ENABLED=true
	  '@
	  Set-Content -Path (Join-Path $Root '.env') -Value $EnvContent -Encoding UTF8
	  
	  # --- docker-compose.yml (no 'version' key to avoid deprecation warning)
	  $Compose = @'
	  services:
	    postgres:
	      image: bitnami/postgresql:16
	      container_name: labnexus-postgres
	      restart: unless-stopped
	      environment:
	        - POSTGRESQL_DATABASE=${POSTGRES_DB}
	        - POSTGRESQL_USERNAME=${POSTGRES_USER}
	        - POSTGRESQL_PASSWORD=${POSTGRES_PASSWORD}
	      ports:
	        - "${POSTGRES_PORT}:5432"
	      volumes:
	        - ./Databases/postgres:/bitnami/postgresql
	      healthcheck:
	        test: ["CMD-SHELL", "/opt/bitnami/postgresql/bin/pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
	        interval: 10s
	        timeout: 5s
	        retries: 30
	  
	    pgadmin:
	      image: dpage/pgadmin4:8
	      container_name: labnexus-pgadmin
	      restart: unless-stopped
	      environment:
	        PGADMIN_DEFAULT_EMAIL: ${PGADMIN_DEFAULT_EMAIL}
	        PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_DEFAULT_PASSWORD}
	      ports:
	        - "8081:80"
	      depends_on:
	        postgres:
	          condition: service_healthy
	  
	    metabase:
	      image: metabase/metabase:latest
	      container_name: labnexus-metabase
	      restart: unless-stopped
	      env_file:
	        - .env
	      environment:
	        MB_DB_TYPE: ${MB_DB_TYPE}
	        MB_DB_DBNAME: ${MB_DB_DBNAME}
	        MB_DB_PORT: ${MB_DB_PORT}
	        MB_DB_USER: ${MB_DB_USER}
	        MB_DB_PASS: ${MB_DB_PASS}
	        MB_DB_HOST: ${MB_DB_HOST}
	      ports:
	        - "3000:3000"
	      depends_on:
	        postgres:
	          condition: service_healthy
	  
	    n8n:
	      image: n8nio/n8n:latest
	      container_name: labnexus-n8n
	      restart: unless-stopped
	      env_file:
	        - .env
	      environment:
	        - N8N_HOST=${N8N_HOST}
	        - N8N_PORT=${N8N_PORT}
	        - N8N_PROTOCOL=${N8N_PROTOCOL}
	        - N8N_EDITOR_BASE_URL=${N8N_EDITOR_BASE_URL}
	        - N8N_API_BASE_URL=${N8N_API_BASE_URL}
	        - N8N_BASIC_AUTH_ACTIVE=${N8N_BASIC_AUTH_ACTIVE}
	        - N8N_BASIC_AUTH_USER=${N8N_BASIC_AUTH_USER}
	        - N8N_BASIC_AUTH_PASSWORD=${N8N_BASIC_AUTH_PASSWORD}
	        - N8N_RUNNERS_ENABLED=${N8N_RUNNERS_ENABLED}
	        - GENERIC_TIMEZONE=America/Toronto
	      ports:
	        - "5678:5678"
	      volumes:
	        - ./Automation/n8n:/home/node/.n8n
	      depends_on:
	        postgres:
	          condition: service_healthy
	  
	    iperf3:
	      image: networkstatic/iperf3:latest
	      container_name: labnexus-iperf3
	      restart: unless-stopped
	      command: -s
	      ports:
	        - "5201:5201"
	  
	  networks:
	    default:
	      name: labnexus-net
	  '@
	  Set-Content -Path (Join-Path $Root 'docker-compose.yml') -Value $Compose -Encoding UTF8
	  
	  # --- requirements.txt for Python analytics
	  $Reqs = @'
	  pandas
	  sqlalchemy
	  psycopg2-binary
	  jupyter
	  matplotlib
	  '@
	  Set-Content -Path (Join-Path $Root 'Analytics\requirements.txt') -Value $Reqs -Encoding UTF8
	  
	  # --- Bring up the stack
	  Write-Host "Starting Docker services..."
	  Push-Location $Root
	  docker compose pull
	  docker compose up -d
	  
	  # --- Wait for Postgres to be healthy (poll health status)
	  Write-Host "Waiting for Postgres health..."
	  $deadline = (Get-Date).AddMinutes(3)
	  do {
	    Start-Sleep -Seconds 3
	    $state = docker inspect -f '{{.State.Health.Status}}' labnexus-postgres 2>$null
	    Write-Host "  postgres health: $state"
	    if ($state -eq 'healthy') { break }
	  } while ((Get-Date) -lt $deadline)
	  
	  if ($state -ne 'healthy') {
	    throw "Postgres did not become healthy in time."
	  }
	  
	  # --- Postgres helpers
	  $PgUser='labadmin'; $PgDb='labnexus'; $PgPass='labsecret'
	  $Prefix='export PATH=/opt/bitnami/postgresql/bin:$PATH;'
	  
	  function Invoke-PsqlScalar([string]$sql) {
	    docker exec -e PGPASSWORD=$PgPass -i labnexus-postgres bash -lc `
	      "$Prefix psql -U $PgUser -d $PgDb -tAc '$sql'"
	  }
	  function Invoke-PsqlExec([string]$sql) {
	    docker exec -e PGPASSWORD=$PgPass -i labnexus-postgres bash -lc `
	      "$Prefix psql -U $PgUser -d $PgDb -c '$sql'"
	  }
	  
	  # --- Ensure 'metabase' application DB exists (for Metabase app storage)
	  Write-Host "Ensuring 'metabase' database exists..."
	  $exists = (Invoke-PsqlScalar "SELECT 1 FROM pg_database WHERE datname='metabase'").Trim()
	  if ($exists -ne '1') {
	    Invoke-PsqlExec "CREATE DATABASE metabase OWNER $PgUser;"
	  }
	  
	  # --- OPTIONAL: seed app schema + sample metrics (idempotent)
	  Write-Host "Seeding labnexus_app schema & sample metrics (idempotent)..."
	  Invoke-PsqlExec "CREATE SCHEMA IF NOT EXISTS labnexus_app AUTHORIZATION $PgUser;"
	  Invoke-PsqlExec @"
	  CREATE TABLE IF NOT EXISTS labnexus_app.metrics (
	    id SERIAL PRIMARY KEY,
	    metric_name TEXT NOT NULL,
	    metric_value NUMERIC,
	    created_at TIMESTAMP DEFAULT now()
	  );
	  "@
	  Invoke-PsqlExec @"
	  INSERT INTO labnexus_app.metrics (metric_name, metric_value) VALUES
	    ('cpu_load', 0.42),
	    ('net_latency_ms', 12.7),
	    ('disk_free_gb', 250.1)
	  ON CONFLICT DO NOTHING;
	  "@ | Out-Null
	  
	  Pop-Location
	  
	  # --- Python venv setup
	  Write-Host "Creating Python venv and installing packages..."
	  $Py = (Get-Command python -ErrorAction SilentlyContinue)?.Source
	  if (-not $Py) {
	    Write-Warning "Python not found in PATH. Install Python 3.11+ or adjust the script."
	  } else {
	    $VenvPath = Join-Path $Root 'Analytics\venv'
	    python -m venv $VenvPath
	    & "$VenvPath\Scripts\python.exe" -m pip install --upgrade pip
	    & "$VenvPath\Scripts\pip.exe" install -r (Join-Path $Root 'Analytics\requirements.txt')
	  }
	  
	  # --- Optional desktop tools (uncomment to use)
	  # winget install --id WiresharkFoundation.Wireshark -e --source winget
	  # winget install --id Insecure.Nmap -e --source winget
	  
	  Write-Host "`nAll set! Endpoints:"
	  Write-Host "  Postgres:       localhost:5432  (db=labnexus, user=labadmin, pass=labsecret)"
	  Write-Host "  pgAdmin:        http://localhost:8081  (login: jeff@compoundcreative.ca / labadmin)"
	  Write-Host "  Metabase:       http://localhost:3000  (first-run wizard; app DB = Postgres 'metabase')"
	  Write-Host "  n8n:            http://localhost:5678  (auth currently disabled)"
	  Write-Host "  iperf3 server:  localhost:5201"
	  if ($VenvPath) { Write-Host "  Python venv:    $VenvPath`n  To activate: `"$VenvPath\Scripts\Activate.ps1`"" }
	  Write-Host "`nDocker quick cmds:"
	  Write-Host "  docker compose -f `"$Root\docker-compose.yml`" ps"
	  Write-Host "  docker logs labnexus-postgres --tail=100 -f"
	  Write-Host "  docker compose -f `"$Root\docker-compose.yml`" down   # stop stack"
	  
	  ```
- **# LabNexus Credentials (Local Dev)**
  
  *_Last updated: 2025-09-08 00:15:57_*
  
  > **Keep this file private.** These credentials are for your **local** LabNexus stack running on Docker.
  
  --
- -
- # ===== Lab Nexus Bootstrap (Windows 11 + Docker + WSL2) =====
-
- **## Postgres**
- **Host:** localhost
- **Port:** 5432
- **Database (default):** `labnexus`
- **User:** `labadmin`
- **Password:** `labsecret`
- **Container:** `labnexus-postgres`
  
  **## Metabase (Web App)**
- **URL:** http://localhost:3000
- **Admin login:** *_the email & password you set during the first-run wizard_*
- **Metabase application DB:** Postgres database **metabase** on the same server above
  
  **## pgAdmin**
- **URL:** http://localhost:8081
- **Email:** jeff@compoundcreative.ca
- **Password:** labadmin
- **Container:** `labnexus-pgadmin`
  
  **## n8n**
- **URL:** http://localhost:5678
- **Auth:** *_currently disabled_* (`N8N_BASIC_AUTH_ACTIVE=false`)
- **If you enable auth later:**
  - **User:** `admin`
  - **Password:** `n8nsecret`  *_(or whatever you change it to in **`.env`**)_*
- **Container:** `labnexus-n8n`
  
  **## iPerf3**
- **Server:** localhost:5201
- **Container:** `labnexus-iperf3`
  
  **## Python (Analytics)**
- **Venv:** `C:\Users\databoho\LabNexus\Analytics\venv`
- Activate:
  - PowerShell: `"C:\Users\databoho\LabNexus\Analytics\venv\Scripts\Activate.ps1"`
  
  ---
  
  **## Notes**
- All services run on the `labnexus-net` Docker network.
- Edit credentials and ports in: `C:\Users\databoho\LabNexus\.env` and `docker-compose.yml`.
- After changes: `docker compose -f "C:\Users\databoho\LabNexus\docker-compose.yml" up -d`