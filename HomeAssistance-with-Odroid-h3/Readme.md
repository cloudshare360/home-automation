Here's a detailed guide to setting up **Docker Compose** with:

- **Home Assistant**
- **PostgreSQL** (PostgresDB)
- **pgAdmin**
- Plus basic **Home Assistant configuration** steps.

---

## 🔧 Step 1: Create Your Project Folder

```bash
mkdir homeassistant_docker && cd homeassistant_docker
```

---

## 🧾 Step 2: Create `docker-compose.yml`

Create a file called `docker-compose.yml` with the following content:

```yaml
version: '3.9'

services:
  homeassistant:
    container_name: homeassistant
    image: ghcr.io/home-assistant/home-assistant:stable
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    network_mode: host
    privileged: true

  postgres:
    container_name: postgres
    image: postgres:15
    restart: unless-stopped
    environment:
      POSTGRES_USER: hauser
      POSTGRES_PASSWORD: hapassword
      POSTGRES_DB: hadb
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4
    restart: unless-stopped
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@home.local
      PGADMIN_DEFAULT_PASSWORD: adminpass
    ports:
      - "5050:80"

volumes:
  pgdata:
```

---

## 📦 Step 3: Start the Stack

Run:

```bash
docker-compose up -d
```

This starts:

- Home Assistant on **http://localhost:8123**
- pgAdmin on **http://localhost:5050**
- PostgreSQL on port **5432**

---

## ⚙️ Step 4: Configure Home Assistant to Use PostgreSQL

1. After Home Assistant starts, **stop it**:

   ```bash
   docker-compose stop homeassistant
   ```

2. Edit the `configuration.yaml` file inside the `config` folder. If it doesn’t exist yet, create it:

   ```yaml
   recorder:
     db_url: postgresql://hauser:hapassword@localhost/hadb
   ```

   This tells Home Assistant to log data to PostgreSQL instead of SQLite.

3. Start Home Assistant again:

   ```bash
   docker-compose start homeassistant
   ```

---

## 📋 Step 5: Use pgAdmin

1. Open pgAdmin at [http://localhost:5050](http://localhost:5050)
2. Login with:
   - **Email**: `admin@home.local`
   - **Password**: `adminpass`
3. Add a new server:
   - **Name**: `HomeAssistantDB`
   - **Host**: `postgres`
   - **Port**: `5432`
   - **Username**: `hauser`
   - **Password**: `hapassword`

---

## ✅ You're Done!

Home Assistant is now:
- Logging to a PostgreSQL database
- Accessible via browser
- Managed alongside pgAdmin and your database via Docker

---

Would you like me to generate a starter `configuration.yaml` with some sensors or automations too?