# How to run Immich App

## Deploy the app with docker

### Step 1 - Download the required files

Download [`docker-compose.yml`](https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml) and [`example.env`](https://github.com/immich-app/immich/releases/latest/download/example.env) by running the following commands or by clicking on their names above (if necessary):

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

Navigate to `http://<private-ip-adress>:2283` in your browser to access the app. If you are running the app locally, you can access it at `http://localhost:2283`.

# Use the notebook main.ipynb to fuzz the app

## Step 1 - Create an .env file for tokens

Once you access the app through the browser with the above steps, you have te create an account, and log in. Then, you have to retrieve the access token from the browser's Application tab in the developer tools. Follow the steps to do so:

- Open the developer tools in your browser by right-clicking on the page and selecting "Inspect", and selecting the "Application" tab on the right.
- In the "Application" tab, expand the "Cookie" section on the left, and copy the value of the `access_token` cookie.
- Create a new file named `.env` in the same directory as the `main.ipynb` file.
- Add the following line to the `.env` file :

```bash title="Add the access token to the .env file"
BEARER_TOKEN=<access_token>
```

## Step 2 - create a virtual environment

```bash title="Create a virtual environment"
python3 -m venv venv
```

## Step 3 - Activate the virtual environment

```bash title="Activate the virtual environment"
source venv/bin/activate
```

## Step 4 - Install the required packages

```bash title="Install the required packages"

pip install -r requirements.txt
```

## Step 5 - Run the notebook

Open the `main.ipynb` file in Jupyter Notebook or Jupyter Lab, and run the cells to fuzz the app.
