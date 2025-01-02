# How to run Immich App

## Deploy the app with docker

### Step 1 - Download the required files

Create a directory of your choice (e.g. `./immich-app`) to hold the `docker-compose.yml` and `.env` files.

```bash title="Move to the directory you created"
mkdir ./immich-app
cd ./immich-app
```

Download [`docker-compose.yml`](https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml) and [`example.env`](https://github.com/immich-app/immich/releases/latest/download/example.env) by running the following commands or by clicking on their names above:

```bash title="Get docker-compose.yml file"
wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
```

```bash title="Get .env file"
wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env
```

### Step 2 - Populate the .env file with custom values

- Populate `UPLOAD_LOCATION` with your preferred location for storing backup assets. It should be a new directory on the server with enough free space.
- Consider changing `DB_PASSWORD` to a custom value. Postgres is not publically exposed, so this password is only used for local authentication.
  To avoid issues with Docker parsing this value, it is best to use only the characters `A-Za-z0-9`. `pwgen` is a handy utility for this.
- Set your timezone by uncommenting the `TZ=` line.
- Populate custom database information if necessary.

### Step 3 - Start the containers

```bash title="Start the containers using docker compose command"
docker compose up -d
```

### Step 4 - Access the app

Navigate to `https://immich-server.immich.orb.local/` or `http://<private-ip-adress>:2283` in your browser to access the app.
