
## 🧠 What is a Docker Image?

### 🔸 Definition:

A **Docker Image** ek **read-only template** hoti hai jo ek container banane ke liye use hoti hai. Ye image me **application code**, **libraries**, **dependencies**, aur **environment settings** included hote hain.

Container ko jab start karte hain, to wo kisi image ke base par hi banta hai.

---

## 🔍 Real-World Analogy:

* 🧱 **Image** = Blueprint (jaise ek ghar ka naksha)
* 🏠 **Container** = Actual house (image ka real run-time version)

---

## 📦 Common Docker Image Examples:

| Image Name | Description                             |
| ---------- | --------------------------------------- |
| `ubuntu`   | Ubuntu OS ka base image                 |
| `node`     | Node.js runtime + OS layer              |
| `nginx`    | NGINX web server                        |
| `mysql`    | MySQL server with base OS               |
| `alpine`   | Super lightweight Linux distro (\~5 MB) |

---

## 🛠 Commands to Work with Docker Images

---

### 🔹 1. List all local Docker images

```bash
docker images
```

📘 **Explanation:**

* Lists all images present on your local machine.
* Columns:

  * `REPOSITORY`: Image ka naam (e.g., ubuntu)
  * `TAG`: Version (e.g., latest)
  * `IMAGE ID`: Unique identifier (shortened hash)
  * `CREATED`: Image kab banayi gayi
  * `SIZE`: Disk space used

🧾 **Example Output:**

```
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
ubuntu       latest    1d622ef86b13   2 weeks ago    29.1MB
node         20        2fe2e413eabf   5 days ago     120MB
```

---

### 🔹 2. Pull an image from Docker Hub

```bash
docker pull ubuntu
```

📘 **Explanation:**
Downloads image from Docker Hub to your local system.

---

### 🔹 3. Remove an image

```bash
docker rmi ubuntu
```

📘 **Explanation:**

* `docker rmi`: Removes a Docker image.
* Agar image se koi container bana hua hai to error aayega. Pehle us container ko delete karo.

---

### 🔹 4. Build your own Docker image (from Dockerfile)

```bash
docker build -t my-custom-image .
```

📘 **Explanation:**

* `-t`: Image ko naam aur tag dena.
* `.`: Current directory me Dockerfile hai.

---

### 🔹 5. Inspect details of an image

```bash
docker inspect ubuntu
```

📘 **Explanation:**
Gives detailed JSON output with info like:

* Environment variables
* Layers
* Config settings
* OS info

---

### 🔹 6. Tag an image

```bash
docker tag ubuntu myrepo/ubuntu:dev
```

📘 **Explanation:**
Ek image ko naye naam/tag ke sath duplicate karta hai without actual duplication of layers.

---

### 🔹 7. Save and Load Docker Image (useful for offline use)

#### 🔸 Save:

```bash
docker save -o ubuntu.tar ubuntu
```

#### 🔸 Load:

```bash
docker load -i ubuntu.tar
```

📘 **Explanation:**

* `save`: Docker image ko `.tar` file me export karta hai.
* `load`: `.tar` file se wapas image import karta hai.
* Useful for **offline transfer** ya **backup** ke liye.

---

### 🔹 8. Search images from Docker Hub

```bash
docker search node
```

📘 **Explanation:**
Search Docker Hub for public images matching "node".

---
---
---

## 🔧 Docker Container

### 🔹 1. Check if Docker is installed:

```bash
docker --version
```

**Explanation:**
Ye check karta hai ki Docker system me installed hai ya nahi.

---

### 🔹 2. Pull Ubuntu image from Docker Hub:

```bash
docker pull ubuntu
```

**Explanation:**

* `docker pull` command ka use karke hum Ubuntu ka official image Docker Hub se download karte hain.
* Agar image already local me ho to ye command kuch nahi karega.
* Default image ka naam `ubuntu` hai, jo latest tag ko pull karta hai (`ubuntu:latest`).

---

### 🔹 3. Run Ubuntu container in interactive mode:

```bash
docker run -it ubuntu
```

**Explanation:**

* `docker run`: Ye command container create karke run karta hai.
* `-i` = **interactive** mode: Input ko container ke terminal ke sath connect karta hai.
* `-t` = **pseudo-TTY**: Terminal access dene ke liye pseudo terminal allocate karta hai.
* `ubuntu` = Ye image ka naam hai (jo humne pull kiya).

⚠️ Is command ke baad aapka terminal Ubuntu container ke andar chala jayega — prompt kuch is tarah dikh sakta hai:

```
root@container_id:/#
```

---

### 🔹 4. (Optional) Run with a custom name and bash shell:

```bash
docker run -it --name my-ubuntu ubuntu /bin/bash
```

**Explanation:**

* `--name my-ubuntu`: Isse container ko ek custom naam diya jata hai (yahan `my-ubuntu`).
* `/bin/bash`: Ye specify karta hai ki container start hote hi `bash` shell open ho.

---

### 🔹 5. Verify running container from another terminal:

```bash
docker ps
```

**Explanation:**

* `docker ps`: Currently running containers ko list karta hai.
* Isme aapko `my-ubuntu` container ka ID, name, status, etc. dikhai dega.

---

### 🔹 6. Exit from the container:

```bash
exit
```

**Explanation:**

* `exit` command container ke andar se bahar nikal deta hai.
* Agar container interactive mode me run ho raha hai (without `--detach`), to container **stop** ho jata hai.

---

### 🔹 7. See stopped containers:

```bash
docker ps -a
```

**Explanation:**

* `-a` flag ke saath `docker ps` run karne se aapko saare containers dikhenge — chahe wo stopped ho ya running.

---

### 🔹 8. Start and re-enter the container again:

```bash
docker start -ai my-ubuntu
```

**Explanation:**

* `docker start`: Stopped container ko wapas start karta hai.
* `-a`: Output ko attach karta hai (real-time dekhenge).
* `-i`: Interactive access deta hai (hum type kar sakte hain).

---

### 🔹 9. Delete the container (optional):

```bash
docker rm my-ubuntu
```

**Explanation:**

* Ye command `my-ubuntu` container ko permanently delete kar deta hai.
* Make sure container stopped ho, warna error dega.

---
---
---

## 🧠 What is Dockerization?

**Dockerization** ka matlab hai:

> Apne application ko **Docker container** ke andar run karne ke liye **package**, **configure**, aur **deploy** karna — jisme uske sare dependencies, environment settings, aur runtime included ho.

### 🔥 Simple words me:

"Apne project ko aise tayar karna ki wo kisi bhi system pe Docker container ke through easily aur reliably chal jaye."

---

## ✅ Why Dockerize an Application?

| Benefits          | Description                                         |
| ----------------- | --------------------------------------------------- |
| ✅ Portability     | App kisi bhi OS ya machine pe chal sakta hai        |
| ✅ Isolation       | Har container ka apna isolated environment hota hai |
| ✅ Easy Setup      | Dockerfile se app ka setup reproducible hota hai    |
| ✅ CI/CD Ready     | Easily integrate ho jata hai pipelines me           |
| ✅ Version Control | Specific image version/tag use kar sakte ho         |

---

## 🛠️ Dockerization Process (Step-by-Step)

---

### 🔹 Step 1: Create a Simple App (Node.js Example)

📁 Folder Structure:

```
my-app/
│
├── app.js
├── package.json
└── Dockerfile
```

📄 **app.js**

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Hello from Dockerized App!');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

📄 **package.json**

```json
{
  "name": "docker-app",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {}
}
```

---

### 🔹 Step 2: Write the Dockerfile

📄 **Dockerfile**

```Dockerfile
# 1. Base Image
FROM node:20

# 2. Set working directory
WORKDIR /app

# 3. Copy package files
COPY package*.json ./

# 4. Install dependencies
RUN npm install 
## yaha pe hum RUN npm ci bhi likh skte hai.

# 5. Copy all files (hm log phle kewal package.json or package-lock.json hi copy krte hai and fr npm install krte hai q ki ye best practice hoti hai for layering system. package*.json se jo bhi install hota hai wo cache ho jata hai to next time agar hm  kuch changes krke fir se build bnate hai means image bnate hai to package*.json ko docker apne cache se utha leta hai)
COPY . .

# 6. Expose port
EXPOSE 3000

# 7. Command to run app
CMD ["npm", "start"]
```

🔍 **Explanation of each line:**

| Line                    | Description                                       |
| ----------------------- | ------------------------------------------------- |
| `FROM node:20`          | Use official Node.js base image                   |
| `WORKDIR /app`          | Create and use `/app` directory inside container  |
| `COPY package*.json ./` | Copy only package files first (for caching)       |
| `RUN npm install`       | Install project dependencies                      |
| `COPY . .`              | Copy remaining project files                      |
| `EXPOSE 3000`           | Inform Docker that container listens on port 3000 |
| `CMD ["npm", "start"]`  | Command to run when container starts              |

---

### 🔹 Step 3: Build the Docker Image

```bash
docker build -t my-dockerized-app .
```

**Explanation:**

* `build`: Docker image banata hai
* `-t`: Tag ya naam dena image ko
* `.`: Current directory me Dockerfile hai

---

### 🔹 Step 4: Run the Container from image (which i have created above from Dockerfile)

```bash
docker run -p 3000:3000 my-dockerized-app
```

**Explanation:**

* `-p 3000:3000`: Host machine ka port 3000 → container ke port 3000
* Ab browser me open karo: [http://localhost:3000](http://localhost:3000)

---

### 🔹 Step 5: Optional Flags

| Flag     | Description                          |
| -------- | ------------------------------------ |
| `-d`     | Run in detached (background) mode    |
| `--name` | Custom name for container            |
| `--rm`   | Auto-delete container after stopping |

**Example:**

```bash
docker run -d --name nodeapp -p 3000:3000 my-dockerized-app
```

---

## ✅ Summary of Dockerization Workflow

```text
1. Create your app (Node, Python, etc.)
2. Create Dockerfile
3. Build Docker image → `docker build -t my-app .`
4. Run container → `docker run -p 3000:3000 my-app`
5. Access app via browser or API
```

---
---
---

## Docker exec command

---

### 🔧 **Command:**

```
docker exec -it mysql bash
```

---

### ✅ **Is command ka kaam:**

Ye command ek **running Docker container** ke andar **bash shell** open karne ke liye use hoti hai.

---

### 🧩 **Command Breakdown:**

| Part     | Explanation                                                                |
| -------- | -------------------------------------------------------------------------- |
| `docker` | Docker CLI (Command Line Interface) tool                                   |
| `exec`   | "Execute" — container ke andar koi command run karne ke liye               |
| `-it`    | Do options ka combination:                                                 |
|     `-i` | interactive mode (container ke input/output ke sath connected rehta hai)   |
|     `-t` | pseudo-TTY allocate karta hai, jisse terminal dikh sake                    |
| `mysql`  | container ka **name** ya **ID** jisme command run karni hai                |
| `bash`   | command jo container ke andar run hogi — yahan bash shell open kar rahe ho |

---

### 🧪 **Example:**

Agar tumne ek MySQL container run kar rakha hai:

```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql
```

To us container ke andar jaane ke liye:

```bash
docker exec -it mysql bash
```

Par **note karo**: Agar MySQL image `bash` shell support nahi karti (kyonki kai lightweight image jaise `mysql:8.0` ya `alpine` `bash` ki jagah `sh` shell use karti hain), to tumhe bash ki jagah `sh` likhna padega:

```bash
docker exec -it mysql sh
```

---

### 📌 **Use Case:**

* Container ke andar file structure dekhna
* Logs check karna
* Config files edit karna
* Troubleshooting/debugging karna
* MySQL CLI open karke database access karna

---
---
---
---

## 🔖 `docker tag` — *"Tagging an image"*

### ✅ **Purpose:**

`docker tag` ka use Docker **image ko ek naya naam ya version tag dene ke liye** hota hai. Ye command **image ko duplicate** nahi karti — sirf ek **reference** create karti hai.

### 📦 **Syntax:**

```bash
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

### 🧠 **Think of it like:**

Giving another label or name to the same image ID.

---

### 🔧 **Example:**

```bash
docker tag my-app:latest myrepo/my-app:v1.0.0
```

➡️ This tags the existing image `my-app:latest` with a new name `myrepo/my-app:v1.0.0`.

Now if you run:

```bash
docker images
```

You'll see both tags pointing to the same IMAGE ID.

---

### 📤 **Use Cases:**

* Pushing image to a Docker registry:

  ```bash
  docker tag my-app:latest username/my-app:prod
  docker push username/my-app:prod
  ```
* Creating versioned backups of the same image.
* Renaming before deployment.

---

## 🏷️ `docker rename` — *"Renaming a container"*

### ✅ **Purpose:**

`docker rename` ka use ek **running ya stopped container ka naam badalne ke liye** hota hai.

### 📦 **Syntax:**

```bash
docker rename OLD_CONTAINER_NAME NEW_CONTAINER_NAME
```

---

### 🔧 **Example:**

```bash
docker rename boring_morse my-new-app
```

➡️ This changes the container name from `boring_morse` to `my-new-app`.

---

### 📤 **Use Cases:**

* Default container names are random (e.g., `angry_bell` or `silly_lamarr`), so you can rename it to something meaningful.
* Better organization in a team or CI/CD pipeline.

---

## 🆚 Difference Between `tag` and `rename`

| Feature          | `docker tag`                    | `docker rename`                   |
| ---------------- | ------------------------------- | --------------------------------- |
| Works on         | Docker **images**               | Docker **containers**             |
| Purpose          | Add new tag/version to an image | Rename a container                |
| Creates copy?    | ❌ No (just a new reference)     | ❌ No (only changes name)          |
| Typical use case | For image versioning & pushing  | For organizing running containers |

---

### 📌 Summary:

* 🏷 **`docker tag`**: Assigns another name or version to an image.
* 🔁 **`docker rename`**: Changes the name of a container (helpful when auto-names are not meaningful).

---
Sure! Here's a **complete Dockerfile example** along with how you can use `docker tag` and `docker rename` with it in a real-world scenario.

---

## 🧱 Step-by-Step Dockerfile Example

### 📁 Project Structure:

```
my-app/
├── Dockerfile
├── package.json
├── index.js
```

### 📄 `index.js`

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('🚀 Hello from Docker!');
});

server.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

### 📄 `package.json`

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  }
}
```

---

## 📄 `Dockerfile`

```dockerfile
# Use an official Node.js base image
FROM node:18-alpine

# Set working directory inside the container
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the rest of the files
COPY . .

# Expose port 3000
EXPOSE 3000

# Start the app
CMD ["npm", "start"]
```

---

## 🐳 Build the Docker Image

```bash
docker build -t my-app:latest .
```

Now your image is built with the tag `my-app:latest`.

---

## 🏷 Add a New Tag to the Same Image (Using `docker tag`)

```bash
docker tag my-app:latest my-app:v1.0.0
```

Check it:

```bash
docker images
```

You’ll now see:

```
REPOSITORY   TAG        IMAGE ID       CREATED         SIZE
my-app       latest     abc123...       10 seconds ago  130MB
my-app       v1.0.0     abc123...       10 seconds ago  130MB
```

✅ Both tags point to the same image.

---

## 🚀 Run the Container

```bash
docker run -d --name hello-docker -p 3000:3000 my-app:latest
```

You can open `http://localhost:3000` and see your app running.

---

## 🔁 Rename the Container (Using `docker rename`)

```bash
docker rename hello-docker my-cool-app
```

Now run:

```bash
docker ps
```

You'll see the container running with the new name `my-cool-app`.

---

## Summary

| Step               | Command Example                                                |
| ------------------ | -------------------------------------------------------------- |
| Build Docker image | `docker build -t my-app:latest .`                              |
| Tag the image      | `docker tag my-app:latest my-app:v1.0.0`                       |
| Run container      | `docker run -d --name hello-docker -p 3000:3000 my-app:latest` |
| Rename container   | `docker rename hello-docker my-cool-app`                       |

---

### Here's the **same Node.js app Dockerized using Docker Compose**, with **environment variables** handled properly.

---

## ✅ Goal:

We’ll run a simple Node.js server using:

* `Dockerfile`
* `docker-compose.yml`
* `.env` for environment variables

---

## 📁 Final Folder Structure:

```
my-app/
├── Dockerfile
├── docker-compose.yml
├── .env
├── index.js
├── package.json
```

---

## 📄 `index.js`

```js
const http = require("http");

const PORT = process.env.PORT || 3000;
const MESSAGE = process.env.MESSAGE || "Hello from Docker Compose!";

const server = http.createServer((req, res) => {
  res.end(`🚀 ${MESSAGE}`);
});

server.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

---

## 📄 `package.json`

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  }
}
```

---

## 📄 `.env` (Environment Variables)

```env
PORT=4000
MESSAGE=Hello from .env in Compose!
```

---

## 📄 `Dockerfile`

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json ./
RUN npm install

COPY . .

EXPOSE 4000

CMD ["npm", "start"]
```

---

## 📄 `docker-compose.yml`

```yaml
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: my-app-container
    ports:
      - "${PORT}:4000"
    environment:
      - PORT=${PORT}
      - MESSAGE=${MESSAGE}
    env_file:
      - .env
```

---

## 🚀 How to Run It

### 1. Build and start the app

```bash
docker-compose up --build
```

### 2. Output

You’ll see in logs:

```
Server running on http://localhost:4000
```

And if you open [http://localhost:4000](http://localhost:4000), it will display:

```
🚀 Hello from .env in Compose!
```

---

## ✅ Summary

| File                 | Purpose                            |
| -------------------- | ---------------------------------- |
| `.env`               | Holds environment variables        |
| `docker-compose.yml` | Configures service, env, and ports |
| `Dockerfile`         | Builds Node.js app image           |
| `index.js`           | Reads env vars and runs web server |

---

Here's a complete and optimized **Docker Compose setup** that includes:

- ✅ A Node.js app
- ✅ MongoDB service
- ✅ Volume mounting for live reload (in development)
- ✅ Multi-stage build for production optimization
- ✅ Use of environment variables from a `.env` file

---

### 📁 Project Structure

```
my-app/
├── docker-compose.yml
├── Dockerfile
├── .env
├── .dockerignore
├── src/
│   └── index.js
├── package.json
└── ...
```

---

### 📄 `.env`

```env
# App
NODE_ENV=development
PORT=3000

# MongoDB
MONGO_INITDB_ROOT_USERNAME=admin
MONGO_INITDB_ROOT_PASSWORD=secret

```

---

### 📄 Dockerfile (multi-stage for Node.js app)

```dockerfile
# ===============================
# === BASE STAGE ===============
# This stage sets up Node environment and installs dependencies.
# It is reused by both development and production stages to avoid repeating setup.
# ===============================

# Use Node.js v18 on Alpine Linux (lightweight)
FROM node:18-alpine as base

# Set the working directory inside the container to /app
WORKDIR /app

# Copy only package.json and package-lock.json (dependency files)
# This helps in leveraging Docker cache – if these files don't change, Docker will not reinstall packages
COPY package*.json ./

# Install all NPM dependencies
RUN npm install

# ===============================
# === DEVELOPMENT STAGE ========
# Used when running app in development mode with live reload (like `npm run dev`)
# ===============================
FROM base as development

# Copy all project files from host to container
COPY . .

# Set the command to start development server
CMD ["npm", "run", "dev"]


# ===============================
# === PRODUCTION STAGE =========
# Used for building and running production-ready optimized app
# ===============================
FROM base as production

# Copy all project files again (important: needs full source code to build)
COPY . .

# Run production build (transpile, optimize, etc.)
RUN npm run build

# Start the built app using Node.js
CMD ["node", "src/index.js"]
```

---

### ✅ Summary for Beginners:

| Section               | Purpose                                             |
| --------------------- | --------------------------------------------------- |
| `FROM node:18-alpine` | Start from a lightweight Node.js image              |
| `WORKDIR /app`        | Set working directory for all following commands    |
| `COPY package*.json`  | Only copy dependency files for faster Docker builds |
| `RUN npm install`     | Install dependencies                                |
| `COPY . .`            | Copy your full app source code into the container   |
| `CMD [...]`           | Command to start the app (`dev` or `node`)          |


---

### 📄 docker-compose.yml

```yaml
version: '3.8'

services:
  app:
    container_name: node-app
    build:
      context: .
      target: ${NODE_ENV}
    ports:
      - "${PORT}:3000"
    volumes:
      - .:/app
      - /app/node_modules
    environment:
      - NODE_ENV=${NODE_ENV}
      - PORT=${PORT}
    depends_on:
      - mongo
    command: npm run dev

  mongo:
    image: mongo:6
    container_name: mongo-db
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=${MONGO_INITDB_ROOT_USERNAME}
      - MONGO_INITDB_ROOT_PASSWORD=${MONGO_INITDB_ROOT_PASSWORD}
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

---

### ✅ Production Tips

* Use `target: production` in Docker Compose for production builds.
* Mount volumes only in development for hot reload.
* You can separate `docker-compose.override.yml` for development-specific options.

---

### 🟢 Run Commands

#### 👉 Development mode:

```bash
docker-compose up --build
```

#### 👉 Production mode:

```bash
NODE_ENV=production docker-compose up --build
```

---
---
---
---
# Docker Network

Bilkul Rishabh! Chalo Docker network ko **beginner-friendly Hinglish** mein detail mein samajhte hain — real-life analogy ke saath, types ke saath, aur saare common commands ke saath.

---

## 🚧 **Docker Network kya hota hai?**

Jab aap multiple Docker containers chalate ho, unhe **ek dusre se communicate** karna padta hai — jaise ki MongoDB aur Mongo Express ke beech. Ye communication possible hota hai via **Docker networks**.

🧠 **Real-life analogy:**
Socho har container ek chhota computer hai, aur Docker network ek Wi-Fi router hai. Jab tak wo sab ek hi Wi-Fi (network) par nahi hote, wo ek dusre se baat nahi kar sakte.

---

## 🔧 Docker Network ke **Types**

Docker me mainly 3 built-in network types hote hain:

| Type                                                         | Description                                                                                                      |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| `bridge`                                                     | Default network jab aap standalone container chalate ho. Private internal network banata hai.                    |
| `host`                                                       | Container directly host machine ka network use karta hai. Port mapping ki zarurat nahi padti.                    |
| `none`                                                       | Container ko koi network access nahi diya jaata. Isolated hota hai.                                              |
| 🧑‍🔧 **Custom bridge network** (most used in real projects) | Aap apna khud ka bridge network bana sakte ho. Containers isme easily ek dusre ko naam se access kar sakte hain. |

---

## 🔗 **Custom Network Kyu Use Karte Hain?**

* Containers ko **by name access** kar sakte ho (e.g., `mongodb`).
* Secure and isolated environment banta hai.
* Useful in multi-container apps (e.g., backend + db + redis).

---

## 🛠️ **Common Docker Network Commands**

### ✅ **1. Create a network**

```bash
docker network create my-custom-network
```

* Ye ek **bridge** type network banata hai by default.
* Ab is network me containers add kar sakte ho using `--network=my-custom-network`.

---

### ✅ **2. List all networks**

```bash
docker network ls
```

🧾 Output me aapko network ka naam, ID, type, etc. dikhega.

---

### ✅ **3. Inspect a network**

```bash
docker network inspect my-custom-network
```

* Ye command network ke andar ka configuration dikhata hai:

  * Konsa container is network me connected hai
  * IP addresses kya hain
  * Driver type kya hai (bridge, host, etc.)

---

### ✅ **4. Connect a running container to a network**

```bash
docker network connect my-custom-network my-container
```

* `my-container` ab `my-custom-network` ke andar aa jayega.

---

### ✅ **5. Disconnect a container from a network**

```bash
docker network disconnect my-custom-network my-container
```

---

### ✅ **6. Remove/Delete a network**

```bash
docker network rm my-custom-network
```

🔴 Note: Network me koi container **attached nahi hona chahiye** tabhi aap delete kar sakte ho.

---

## 📦 Example Flow:

```bash
# Step 1: Create network
docker network create mongo-network

# Step 2: Run MongoDB in this network
docker run -d --name=mongodb --network=mongo-network mongo

# Step 3: Run Mongo Express in same network
docker run -d --name=mongo-express --network=mongo-network -p 8081:8081 mongo-express

# Step 4: Inspect network
docker network inspect mongo-network
```

---

## 📘 Summary (Hinglish):

* Docker network containers ke beech communication ke liye highway jaisa hota hai.
* Custom network ka use karne se containers ek dusre ko **naam se** access kar pate hain — IP ya port ki zarurat nahi padti.
* Best practice: production ya dev environment me **custom bridge network** use karo.

---


## 🐳 **Command 1** – MongoDB Container Run

```bash
docker run -d --name=mongodb \
-p 27018:27017 \
--network=mongo-network \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=qwerty \
mongo
```

### 🔍 Explanation:

| Part                                   | Description                                                                                                                                                                      |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `docker run`                           | Docker ko ek new container run karne ke liye command.                                                                                                                            |
| `-d`                                   | Detached mode: Container background me run karega.                                                                                                                               |
| `--name=mongodb`                       | Container ka naam `mongodb` rakha gaya hai (easy to reference).                                                                                                                  |
| `-p 27018:27017`                       | Host ke port **27018** ko container ke **27017** port se map kiya gaya hai.<br>📝 27017 is MongoDB ka default port, lekin host pe hum 27018 use kar rahe hain to avoid conflict. |
| `--network=mongo-network`              | Ye container `mongo-network` naam ke Docker network pe run karega, jisse ye kisi aur container (jaise mongo-express) se communicate kar sake.                                    |
| `-e MONGO_INITDB_ROOT_USERNAME=admin`  | MongoDB ke root user ka username `admin` set kiya gaya hai (environment variable ke through).                                                                                    |
| `-e MONGO_INITDB_ROOT_PASSWORD=qwerty` | Root user ka password `qwerty` set kiya gaya hai.                                                                                                                                |
| `mongo`                                | Ye image ka naam hai (official MongoDB image from Docker Hub).                                                                                                                   |

### 💡 Iska matlab:

Hum ek MongoDB container run kar rahe hain jo custom port (27018) par accessible hai, aur jisme ek secured root user setup hai. Ye container ek custom Docker network par run ho raha hai taaki doosre services (jaise mongo-express) se easily connect ho sake.

---

## 🌐 **Command 2** – Mongo Express Container Run

```bash
docker run -d --name=mongo-express \
--network=mongo-network \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=qwerty \
-e ME_CONFIG_MONGODB_URL=mongodb://admin:qwerty@mongodb:27017/ \
mongo-express
```

### 🔍 Explanation:

| Part                                                             | Description                                                                                                                                      |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `docker run`                                                     | Docker ko ek new container run karne ke liye command.                                                                                            |
| `-d`                                                             | Detached mode (background me chalega).                                                                                                           |
| `--name=mongo-express`                                           | Container ka naam `mongo-express` rakha gaya hai.                                                                                                |
| `--network=mongo-network`                                        | Isko bhi same Docker network me daala gaya hai (jisme MongoDB hai).                                                                              |
| `-p 8081:8081`                                                   | Host ke port **8081** ko container ke port **8081** se map kiya gaya hai.<br>📝 Is port par Mongo Express web UI chalega.                        |
| `-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin`                       | MongoDB ka admin username bataya gaya hai (jo command 1 me diya tha).                                                                            |
| `-e ME_CONFIG_MONGODB_ADMINPASSWORD=qwerty`                      | MongoDB ka admin password.                                                                                                                       |
| `-e ME_CONFIG_MONGODB_URL=mongodb://admin:qwerty@mongodb:27017/` | Is URL ke through Mongo Express ko MongoDB se connect karwaya gaya hai.<br>📝 `mongodb` yahan container name hai jise Docker DNS resolve karega. |
| `mongo-express`                                                  | Ye image ka naam hai (official Mongo Express image from Docker Hub).                                                                             |

### 💡 Iska matlab:

Ye command Mongo Express ko run karta hai – ek lightweight web-based UI jisse aap MongoDB ke data ko GUI ke through dekh sakte hain. Ye web UI aapko `localhost:8081` pe dikhai dega, aur ye internally MongoDB container se connect karega.

---

## ✅ Summary (Hinglish)

* **Command 1** se hum MongoDB container run karte hain with a secure admin user.
* **Command 2** se hum Mongo Express run karte hain jo MongoDB ko GUI ke through manage karne deta hai.
* Dono containers same Docker network (`mongo-network`) pe hain taaki ye easily ek doosre se communicate kar saken.

<img width="1024" height="1024" alt="mongo-network" src="https://github.com/user-attachments/assets/0cb96311-5928-4705-a40d-5574aa131bcc" />


---
---
---

# 🧩 **Docker Compose kya hai?**

`Docker Compose` ek tool hai jo aapko multiple containers ko **ek saath define aur run** karne deta hai ek single YAML file ke through.

🧠 **Real-life Analogy:**
Socho har container ek actor hai, aur Docker Compose ek **script** hai jisme likha hota hai ki kaun kab aayega, kya karega, kis se baat karega.

---

## 🛠️ `docker-compose.yml` Ka Structure

Ek basic `docker-compose.yml` file kuch is tarah dikhti hai:

```yaml
version: '3.8'

services:
  service1:
    image: image-name
    ports:
      - "hostPort:containerPort"
    environment:
      VAR_NAME: value
    networks:
      - my-network

networks:
  my-network:
    driver: bridge
```

---

## 🧪 Example: MongoDB + Mongo Express

Yeh wahi example hai jo humne pehle diya tha — MongoDB aur Mongo Express ko ek hi custom network me chalana.

```yaml
version: '3.8'

services:
  mongodb:
    image: mongo
    container_name: mongodb
    ports:
      - "27018:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: qwerty
    networks:
      - mongo-network

  mongo-express:
    image: mongo-express
    container_name: mongo-express
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: qwerty
      ME_CONFIG_MONGODB_URL: mongodb://admin:qwerty@mongodb:27017/
    depends_on:
      - mongodb
    networks:
      - mongo-network

networks:
  mongo-network:
    driver: bridge
```

---

## 🔍 **Line-by-line Explanation in Hinglish**

| Section          | Meaning                                                                   |
| ---------------- | ------------------------------------------------------------------------- |
| `version: '3.8'` | Docker Compose ka version (3.8 is stable and widely supported).           |
| `services:`      | Isme aap define karte ho **containers** (services = multiple containers). |

### 🔹 mongodb service:

| Key                       | Meaning                                                                                                    |
| ------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `image: mongo`            | MongoDB ka official Docker image use ho raha hai.                                                          |
| `container_name: mongodb` | Container ka naam set kar diya hai `mongodb` (for reference).                                              |
| `ports:`                  | Host\:Container port mapping.<br>Yahan host ke 27018 port ko container ke 27017 port se map kiya gaya hai. |
| `environment:`            | Environment variables (like username/password).                                                            |
| `networks:`               | Ye service custom `mongo-network` me connect hogi.                                                         |

### 🔹 mongo-express service:

| Key                             | Meaning                                                                                    |
| ------------------------------- | ------------------------------------------------------------------------------------------ |
| `image: mongo-express`          | Mongo Express ka image use kiya gaya hai.                                                  |
| `container_name: mongo-express` | Container ka naam diya gaya hai.                                                           |
| `ports:`                        | Host ke 8081 port se access hoga Mongo Express ka web UI.                                  |
| `environment:`                  | MongoDB se connect hone ke liye admin username, password aur connection URL diya gaya hai. |
| `depends_on:`                   | Ye ensure karta hai ki `mongodb` container pehle start ho, tab `mongo-express`.            |
| `networks:`                     | Same network (`mongo-network`) me add kiya gaya hai.                                       |

### 🔹 networks:

```yaml
networks:
  mongo-network:
    driver: bridge
```

* Custom bridge network banayi gayi hai.
* Ye sab containers ko ek secure aur isolated environment provide karta hai.

---

## 🔧 **Compose Commands**

### ✅ 1. Start all containers:

```bash
docker-compose up -d
```

➡️ Sab services background me run ho jaati hain.

---

### ✅ 2. Stop all containers:

```bash
docker-compose down
```

➡️ Sab containers, networks, etc. ko stop & delete kar deta hai (except volumes).

---

### ✅ 3. Rebuild containers (after image/env change):

```bash
docker-compose up --build -d
```

---

### ✅ 4. Check running containers:

```bash
docker-compose ps
```

---

### ✅ 5. Logs of all services:

```bash
docker-compose logs
```

---

## 📘 Summary (Hinglish):

* `docker-compose.yml` ek tarika hai ek se zyada containers ko ek saath manage karne ka.
* YAML file me aap define karte ho services, unka image, ports, environment vars, and network.
* Ek hi command (`docker-compose up`) se sab kuch chalu ho jata hai.
* Ye repeatable, version-controlled aur scalable hota hai — real-world projects me bahut useful.

---
---
---
---

# 🔐 `.env` File in Docker Compose

`.env` file ek **key-value pair** file hoti hai jisme aap sensitive ya frequently changing values (like username, password, ports) ko store kar sakte ho.

🧠 **Real-life analogy:**
Socho `docker-compose.yml` ek recipe hai. `.env` file us recipe ke ingredients ke quantity ka table hai — alag file me likha hua.

---

## 🧾 Step-by-Step Setup

### 📁 1. **Create `.env` file**

`.env` file project root me banate hain:

```env
# .env
MONGO_INITDB_ROOT_USERNAME=admin
MONGO_INITDB_ROOT_PASSWORD=qwerty
MONGO_EXPRESS_PORT=8081
MONGODB_PORT=27018
```

---

### 📄 2. **Update `docker-compose.yml` to use variables**

```yaml
version: '3.8'

services:
  mongodb:
    image: mongo
    container_name: mongodb
    ports:
      - "${MONGODB_PORT}:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_INITDB_ROOT_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_INITDB_ROOT_PASSWORD}
    networks:
      - mongo-network

  mongo-express:
    image: mongo-express
    container_name: mongo-express
    ports:
      - "${MONGO_EXPRESS_PORT}:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: ${MONGO_INITDB_ROOT_USERNAME}
      ME_CONFIG_MONGODB_ADMINPASSWORD: ${MONGO_INITDB_ROOT_PASSWORD}
      ME_CONFIG_MONGODB_URL: mongodb://${MONGO_INITDB_ROOT_USERNAME}:${MONGO_INITDB_ROOT_PASSWORD}@mongodb:27017/
    depends_on:
      - mongodb
    networks:
      - mongo-network

networks:
  mongo-network:
    driver: bridge
```

---

## ✅ Benefits of Using `.env` File

| 🔐 Benefit          | 📄 Explanation                                                                                |
| ------------------- | --------------------------------------------------------------------------------------------- |
| **Security**        | Password, username hardcoded nahi karte — safe aur hidden rakh sakte ho.                      |
| **Maintainability** | Agar port ya user change karna hai to sirf `.env` file edit karo, YAML file untouched rahegi. |
| **Reusability**     | Same compose file different envs (dev, staging, prod) me use ho sakti hai.                    |
| **Cleaner YAML**    | Compose file zyada readable aur short hoti hai.                                               |

---

## 🧪 Run the Compose Project

No change in command! Docker Compose automatically `.env` file ko read karega:

```bash
docker-compose up -d
```

> Bas ensure karo ki `.env` file aur `docker-compose.yml` same directory me ho.

---

## 📘 Summary (Hinglish):

* `.env` file me aap environment variables define karte ho.
* Compose file me `${VAR_NAME}` syntax se inhe use karte ho.
* Isse aapka setup zyada secure, clean aur maintainable hota hai.

---

## 💾 What is Docker Volume?

**Docker Volume** ek mechanism hai **data ko container ke bahar** store karne ka — taaki wo **container delete hone ke baad bhi persist** rahe.

🧠 **Real-life Analogy:**
Socho container ek laptop hai, aur volume ek **external hard drive** jisme aapka data save hota hai. Agar laptop (container) crash ho bhi jaaye, aapka data to external drive (volume) me safe hai!

---

## 🔍 Why Use Volumes?

| 📌 Use Case                   | ✅ Benefit                                              |
| ----------------------------- | ------------------------------------------------------ |
| Persistent data               | Container delete hone ke baad bhi data rahe            |
| Share data between containers | Ek hi volume ko multiple containers use kar sakte hain |
| Backup and restore            | Volume ka snapshot le sakte ho                         |
| Performance                   | Volumes zyada optimized hote hain `bind mounts` se     |

---

## 🧰 Types of Docker Storage

| Type             | Description                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------------- |
| **Volumes**      | Docker manage karta hai, safest & recommended                                               |
| **Bind mounts**  | Host system ke kisi path ko directly container me mount karna                               |
| **tmpfs mounts** | Temporary in-memory mount (RAM me store hota hai) — container restart pe delete ho jata hai |

---

## 🏗️ Volume Creation Example

### 🔹 1. Create a Volume

```bash
docker volume create mydata
```

### 🔹 2. Use Volume in a Container

```bash
docker run -d \
  --name my-container \
  -v mydata:/app/data \
  busybox sleep 3600
```

* `-v mydata:/app/data`: host ka `mydata` volume container ke `/app/data` folder me mount hoga.

---

## 📁 Real Example: Use with MongoDB

```bash
docker run -d \
  --name mongodb \
  -p 27017:27017 \
  -v mongo-volume:/data/db \
  mongo
```

* MongoDB ka data `/data/db` me store hota hai
* Humne us path pe ek named volume `mongo-volume` mount kar diya
* Ab MongoDB ka data container ke bahar persist rahega

---

## 🔧 Volume Commands (Cheat Sheet)

| Command                        | Use                                                         |
| ------------------------------ | ----------------------------------------------------------- |
| `docker volume create [name]`  | Naya volume create kare                                     |
| `docker volume ls`             | Sab volumes list kare                                       |
| `docker volume inspect [name]` | Volume ke details dekhne ke liye                            |
| `docker volume rm [name]`      | Volume delete karne ke liye                                 |
| `docker volume prune`          | Sab unused volumes delete kar dega (⚠️ confirmation aayega) |

---

## 🧪 Volume with Docker Compose

**`docker-compose.yml` Example:**

```yaml
version: '3.8'

services:
  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

🟢 Isme hum `mongo-data` naam ka volume define kar rahe hain jo MongoDB ke internal path `/data/db` se connect hoga.

➡️ Run:

```bash
docker-compose up -d
```

---

## 📘 Docker Volumes – Documentation Notes (For You)

### 📌 What are Docker Volumes?

Docker volumes are persistent data storage mechanisms used to store data **outside** the container's file system.

---

### 🛠️ Features of Docker Volumes

* Data safe even if container is deleted
* Shareable across multiple containers
* Optimized for performance
* Managed by Docker (unlike bind mounts)

---

### 📁 Common Use Cases

* Database storage (MongoDB, MySQL, PostgreSQL)
* Log files
* User uploads
* Caching or temp file storage between service restarts

---

### 🔐 Best Practices

* Always use named volumes for production data
* Use volume for `/data/db`, `/var/lib/mysql`, etc. for DBs
* Avoid storing data inside container filesystem directly
* Use `docker-compose` for consistent volume setup

---

### 📦 Folder Structure Example:

```
/mongo-app
│
├── docker-compose.yml
└── data/
    └── (empty or .gitignore file)
```

---

### 🧹 Clean-up Tips:

```bash
# List all volumes
docker volume ls

# Remove specific volume
docker volume rm volume-name

# Remove all unused volumes
docker volume prune
```

---

## ✅ Summary (Hinglish)

| 🔍 Topic      | 💡 Explanation                                   |
| ------------- | ------------------------------------------------ |
| Docker Volume | Container ke bahar ka data storage               |
| Safe          | Container delete hone par bhi data safe          |
| Shareable     | Multiple containers ek volume use kar sakte hain |
| Persistent    | Restart ke baad bhi data rahega                  |
| Easy Commands | `create`, `ls`, `rm`, `inspect`, `prune`         |

---

## 🔍 **Problem:**

> Jab aap Docker Compose se apna project chala rahe ho (`docker compose up`) aur `server.js` ya kisi JS file me koi **code change** karte ho, to wo **browser me reflect nahi hota** bina container ko dubara run kiye.

---

## 🧠 **Reason:**

Docker container ek isolated environment hota hai. By default, jab aap `my-app` container banate ho using `build: .`, to:

* Docker ek image banata hai aapke code ke base par.
* Phir wo container us image se run karta hai.
* **Par wo image me code "freeze" ho jata hai build time pe**, to agar aap baad me `server.js` ya koi bhi file change karte ho **host machine** pe, wo container ke andar reflect nahi hota.

---

## ✅ **Solution: Use volume binding to sync host code with container**

Aapko Docker Compose me `volumes` ka use karna chahiye taaki container hamesha **aapke local code** ko read kare.

### 🔧 **Fix your `docker-compose.yml` like this:**

```yaml
version: '3.8'

services: 
  mongodb: 
    image: mongo
    container_name: mongodb
    ports : 
      - 27018:27017
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: qwerty

  mongo-express:
    image: mongo-express
    ports:
      - 8081:8081
    restart: always
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=qwerty
      - ME_CONFIG_MONGODB_URL=mongodb://admin:qwerty@mongodb:27017/
    depends_on:
      - mongodb

  my-app:
    build: .
    ports:
      - 5050:5050
    volumes:
      - .:/app
      - /app/node_modules
    depends_on:
      - mongodb
```

📌 `volumes`:

* `.:/app` → Local current directory ko container ke `/app` folder se bind karta hai.
* `/app/node_modules` → Iska use hum karte hain taaki local machine ke `node_modules` accidentally container ke overwrite na ho.

> ⚠️ Make sure aapke Dockerfile me `WORKDIR /app` ho set.

---

## 🔁 **Live Reloading (Optional but recommended)**

### Agar aap chahte ho ki:

* File save karte hi server auto-restart ho jaye (without `docker compose down && up`),

### 🔥 Use `nodemon` in your container

#### Step 1: Install `nodemon` in your project

```bash
npm install --save-dev nodemon
```

#### Step 2: Update your `package.json` scripts:

```json
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
}
```

#### Step 3: Update your `Dockerfile`:

```dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

CMD ["npm", "run", "dev"]
```

---

## 🔹 1. **What is a Volume in Docker?**

### 🚫 By default:

Docker container ke andar ka file system **isolated** hota hai.

* Agar aap `server.js` container ke andar hai, aur aap host machine pe `server.js` change karte ho, **container ko pata nahi chalega**.
* Isliye change reflect nahi hota.

### ✅ Solution:

**Volume** = Ek bridge (connection) hota hai:

* **Host machine ka folder/file** ⇄ **Docker container ka folder/file**

So agar aap local pe `server.js` change karte ho, and wo volume se container ke `/app` se connected hai, to **live update** ho jata hai container ke andar bhi.

---

## 🔹 2. **Types of Volumes**

| Type              | Description                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------- |
| **Bind Mounts**   | Host machine ka specific folder container ke andar mount karte ho                        |
| **Named Volumes** | Docker apne internal folder me ek volume banata hai (useful for persistent data like DB) |

---

## 🔹 3. **Use Case: Node.js App with Bind Mount**

Imagine aapka project structure aisa hai:

```
/my-node-app
  ├── server.js
  ├── package.json
  ├── node_modules/
  └── Dockerfile
```

### 🧩 In your `docker-compose.yml`:

```yaml
my-app:
  build: .
  ports:
    - 5050:5050
  volumes:
    - .:/app               # ← This is bind mount
    - /app/node_modules    # ← Ignore local node_modules
```

**Explanation:**

| Line                | Meaning                                                                                                                                                              |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.:/app`            | Aapka local folder (.) container ke `/app` folder me mount hoga                                                                                                      |
| `/app/node_modules` | Ye ek trick hai – taaki aapka local `node_modules` folder container ke andar overwrite na ho jaye (kyunki Linux vs Mac/Windows ka `node_modules` different hota hai) |

---

## 🔹 4. **Diagram Explanation**

```
Host Machine                         Docker Container
--------------                       ----------------
/my-node-app                         /app
|                                   |
|- server.js       ─────────────▶   |- server.js (auto updated)
|- package.json    ─────────────▶   |- package.json
|- node_modules/                    |- node_modules/  (inside container only)
```

So jab aap **VSCode me server.js** save karoge, wo directly container ke `/app/server.js` me bhi update ho jata hai – isliye restart hone pe latest code run hota hai.

---

## 🔹 5. **Why This Is Important in Development?**

### ✅ Benefits:

* No need to rebuild the image after every code change
* Instant feedback during development
* Great with tools like `nodemon`

---

## 🔄 6. **Production vs Development Volumes**

| Environment | Use Volumes? | Why?                                |
| ----------- | ------------ | ----------------------------------- |
| Development | ✅ Yes        | For live code sync                  |
| Production  | ❌ No         | Code should be frozen (image-based) |

---

## ✅ **Real Example Recap**

If you're using:

* `volumes: - .:/app` → You are saying: **"Hey Docker, run my local code directly inside the container"**

Combine it with `nodemon`, and you’re ready for a full dev workflow!

---

## 📌 Bonus: `docker-compose.override.yml` for dev

You can also create a separate override file just for dev:

```yaml
# docker-compose.override.yml
services:
  my-app:
    volumes:
      - .:/app
      - /app/node_modules
```

So that your main `docker-compose.yml` is production-safe.

---
---
---
---

## 🧪 Command:

```bash
docker-compose up cfar-ui
```

### ✅ Iska matlab:

> **Sirf `cfar-ui` service ko run karo** (jo `docker-compose.yml` me define hai), **along with any services it depends on** (via `depends_on`, if any).

---

## 🔍 Important Points:

### 1. **Ye `cfar-ui` wali service ko run karega**

Agar aapke `docker-compose.yml` me multiple services hain (e.g., `mongodb`, `mongo-express`, `cfar-ui`), to ye command **sirf `cfar-ui`** ko run karega.

### 2. ✅ Agar `cfar-ui` ke andar `depends_on` defined hai:

```yaml
cfar-ui:
  depends_on:
    - backend
    - mongodb
```

To wo **un services ko bhi automatically run karega**, taaki `cfar-ui` sahi se kaam kare.

But agar **`depends_on` nahi hai**, to **wo baaki services run nahi hongi** — chahe wo pehle likhi ho ya baad me.

---

## 💡 Example for clarity

```yaml
version: '3'
services:
  mongodb:
    image: mongo

  mongo-express:
    image: mongo-express

  cfar-ui:
    image: dynatech/cfar-ui
    depends_on:
      - mongodb
```

### ➤ Command: `docker-compose up cfar-ui`

🔸 Ye run karega:

* ✅ `cfar-ui`
* ✅ `mongodb` (because of `depends_on`)

🔸 Ye **skip karega**:

* ❌ `mongo-express` (kyunki wo `depends_on` me nahi hai)

---

## ✅ So, Conclusion:

| Statement                                                                                        | ✅ Correct?    |
| ------------------------------------------------------------------------------------------------ | ------------- |
| "Ye sirf pehli service run karta hai jo file me likhi ho"                                        | ❌ Galat       |
| "Ye sirf us service ko run karta hai jiska naam diya gaya ho (`cfar-ui`) + uske dependencies ko" | ✅ Bilkul Sahi |

---
---
---
---

## Question ?

> **Ek cheez mujhe samajh nahi aa rahi hai, please clear karo:**
>
> Mere paas ek `Dockerfile` aur ek `docker-compose.yml` file hai.
>
> Mere Dockerfile ke end me already ye line likhi hai:
>
> ```Dockerfile
> CMD [ "npm", "run", "start" ]
> ```
>
> Matlab agar koi external command na di jaye to container `npm start` run karega — ye default behavior hai.
>
> **Ab confusion ye hai** ki agar Dockerfile me already `CMD` diya gaya hai, to phir mujhe `docker-compose.yml` ke andar `command:` tag use karke alag se command kyun likhni pad rahi hai?
>
> Jaise ki `cfar-ui` service me `command: npm run start:storybook` diya gaya hai, aur `cfar-prod` me `npm run preview` likha hai.
>
> To kya `docker-compose.yml` ka `command:` Dockerfile ke `CMD` ko override karta hai?
> Aur is tarah alag-alag command likhne ka real use-case kya hota hai jab sab same Dockerfile se ban rahe hain?


---

Answer :

tumne **Dockerfile ke `CMD` vs `docker-compose.yml` ke `command`** ke beech ka actual confusion pakda hai jo har developer ko clear hona chahiye.

Main tumhe **clear, practical, aur real-world logic ke saath** samjha raha hoon ki `docker-compose.yml` me `command:` likhne ki **need kya hoti hai**, jab `Dockerfile` me pehle se `CMD` diya hua hai.

---

## 🧠 Core Concept: Who wins – Dockerfile CMD vs docker-compose command?

| Location                        | Purpose                                                   | Winner                |
| ------------------------------- | --------------------------------------------------------- | --------------------- |
| `Dockerfile → CMD`              | Default command for container if **no override is given** | ❌ Loses if overridden |
| `docker-compose.yml → command:` | **Overrides** the CMD of Dockerfile                       | ✅ **Wins** if present |

---

## 🎯 So, **Why `command:` is used in docker-compose.yml?**

Because:

> It allows you to **override the default CMD** defined in the Dockerfile **without editing** the Dockerfile itself.

Yeh **super useful** hota hai jab:

* Tum ek hi image se **multiple modes** run karna chahte ho (dev, storybook, preview, prod)
* Jaise tumhare case me:

---

### ✅ Your Scenario (Real Use Case):

You have 1 Dockerfile, but 3 different services:

| Service     | Purpose           | What it runs              |
| ----------- | ----------------- | ------------------------- |
| `cfar-ui`   | Runs Storybook    | `npm run start:storybook` |
| `cfar-app`  | Runs Main App     | `npm start`               |
| `cfar-prod` | Runs Preview Mode | `npm run preview`         |

And **Dockerfile CMD** me likha hai:

```Dockerfile
CMD [ "npm", "run", "start"]
```

So agar tum `command:` nahi doge, to **sabhi services by default `npm start` run karenge**.

### ⚠️ Problem:

But tum chahte ho ki:

* Storybook ke liye → `npm run start:storybook`
* Preview ke liye → `npm run preview`
* App ke liye → `npm start`

---

## ✅ Solution:

Aapne smartly `command:` override use kiya in `docker-compose.yml`:

```yaml
cfar-ui:
  command: npm run start:storybook

cfar-app:
  command: npm start

cfar-prod:
  command: npm run preview
```

### 🧠 Isse benefit:

* Tumhara **Dockerfile generic rehta hai**
* Aur `docker-compose.yml` se tum flexible behavior set kar paate ho **without touching image** again and again

---

## 📦 Extra Note:

### Tum ye bhi kar sakte the:

```bash
docker run dynatech/cfar-ui npm run preview
```

But ye CLI level pe thoda messy hota hai — isliye `command:` in `docker-compose.yml` is **cleaner and scalable way**.

---

## 🔚 Final Answer

> **Yes**, `docker-compose.yml` ka `command:` tag is used to **override** the default `CMD` of the Dockerfile.

Aur tumhare case me uska use 100% valid hai kyunki tum ek hi base Dockerfile se **alag-alag services ko alag commands** ke saath run kar rahe ho (storybook, app, preview).

---

## Docker ke beginner to advanced level tak ki sabhi important commands ki list

---

## 🔰 **Beginner Level Docker Commands**

### 1. `docker --version`

**Kaam:** Docker ka installed version dikhata hai.
**Example:**

```bash
docker --version
```

---

### 2. `docker info`

**Kaam:** Docker engine ka detailed system info dikhata hai.
**Example:**

```bash
docker info
```

---

### 3. `docker pull <image-name>`

**Kaam:** Docker Hub se image download karta hai.
**Example:**

```bash
docker pull nginx
```

---

### 4. `docker images`

**Kaam:** Local system me jitni bhi images hain unki list dikhata hai.
**Example:**

```bash
docker images
```

---

### 5. `docker run <image>`

**Kaam:** Image ko run karta hai aur container create karta hai.
**Common flags:**

* `-d` → background me run kare
* `-p` → ports bind kare
* `--name` → container ko custom naam de
* `-e` → environment variable set kare
  **Example:**

```bash
docker run -d --name web-app -p 8080:80 nginx
```

---

### 6. `docker ps`

**Kaam:** Currently running containers dikhata hai.
**Example:**

```bash
docker ps
```

---

### 7. `docker ps -a`

**Kaam:** All (running + stopped) containers dikhata hai.
**Example:**

```bash
docker ps -a
```

---

### 8. `docker stop <container-id|name>`

**Kaam:** Container ko stop karta hai.
**Example:**

```bash
docker stop web-app
```

---

### 9. `docker start <container-id|name>`

**Kaam:** Stopped container ko start karta hai.
**Example:**

```bash
docker start web-app
```

---

### 10. `docker restart <container-id|name>`

**Kaam:** Container ko restart karta hai.
**Example:**

```bash
docker restart web-app
```

---

### 11. `docker rm <container-id|name>`

**Kaam:** Container ko delete karta hai.
**Example:**

```bash
docker rm web-app
```

---

### 12. `docker rmi <image-id|name>`

**Kaam:** Docker image ko delete karta hai.
**Example:**

```bash
docker rmi nginx
```

---

### 13. `docker exec -it <container-name> bash`

**Kaam:** Running container me bash shell open karta hai.
**Example:**

```bash
docker exec -it web-app bash
```

---

### 14. `docker logs <container-name>`

**Kaam:** Container ke logs dikhata hai.
**Example:**

```bash
docker logs web-app
```

---

### 15. `docker build -t <name>:<tag> .`

**Kaam:** Dockerfile se image banata hai.
**Example:**

```bash
docker build -t my-app:latest .
```

---

## 🔁 **Intermediate Level Docker Commands**

### 16. `docker-compose up`

**Kaam:** `docker-compose.yml` file ke through multiple containers run karta hai.
**Example:**

```bash
docker-compose up
```

### 17. `docker-compose down`

**Kaam:** Saare containers, networks, volumes ko stop aur remove karta hai.
**Example:**

```bash
docker-compose down
```

---

### 18. `docker network ls`

**Kaam:** Docker networks ki list dikhata hai.
**Example:**

```bash
docker network ls
```

---

### 19. `docker volume ls`

**Kaam:** Volumes ki list dikhata hai.
**Example:**

```bash
docker volume ls
```

---

### 20. `docker volume create <volume-name>`

**Kaam:** New volume create karta hai.
**Example:**

```bash
docker volume create mongo-data
```

---

### 21. `docker system prune`

**Kaam:** Unused images, containers, networks sab clean karta hai.
**Example:**

```bash
docker system prune
```

---

### 22. `docker inspect <container-name>`

**Kaam:** Container ya image ka low-level detailed info deta hai (JSON format).
**Example:**

```bash
docker inspect web-app
```

---

### 23. `docker tag <image> <new-name>`

**Kaam:** Image ko rename/tag karta hai.
**Example:**

```bash
docker tag my-app my-repo/my-app:v1
```

---

### 24. `docker login`

**Kaam:** DockerHub me login karne ke liye.
**Example:**

```bash
docker login
```

---

### 25. `docker push <image>`

**Kaam:** Image ko DockerHub me upload karta hai.
**Example:**

```bash
docker push my-repo/my-app:v1
```

---

### 26. `docker save -o <file.tar> <image>`

**Kaam:** Image ko tar file me export karta hai.
**Example:**

```bash
docker save -o my-app.tar my-app
```

---

### 27. `docker load -i <file.tar>`

**Kaam:** Tar file se image import karta hai.
**Example:**

```bash
docker load -i my-app.tar
```

---

### 28. `docker rename <old-name> <new-name>`

**Kaam:** Container ka naam change karta hai.
**Example:**

```bash
docker rename web-app my-nginx
```

---

## 🚀 **Advanced Level Docker Commands**

### 29. `docker stats`

**Kaam:** Live container resource usage stats dikhata hai (CPU, Memory, etc).
**Example:**

```bash
docker stats
```

---

### 30. `docker cp <container>:/path/in/container /host/path`

**Kaam:** Container se host machine me file copy karta hai.
**Example:**

```bash
docker cp web-app:/app/logs.txt ./logs.txt
```

---

### 31. `docker cp /host/path <container>:/path/in/container`

**Kaam:** Host se container me file copy karta hai.
**Example:**

```bash
docker cp ./file.txt web-app:/usr/share/nginx/html
```

---

### 32. `docker update --memory <limit> <container>`

**Kaam:** Container ka resource (memory, CPU) update karta hai.
**Example:**

```bash
docker update --memory 500m web-app
```

---

### 33. `docker events`

**Kaam:** Docker engine ke real-time events dikhata hai.
**Example:**

```bash
docker events
```

---

### 34. `docker top <container>`

**Kaam:** Container ke running processes dikhata hai.
**Example:**

```bash
docker top web-app
```

---

### 35. `docker export <container> > file.tar`

**Kaam:** Container ko tar format me export karta hai (stateful backup).
**Example:**

```bash
docker export web-app > app.tar
```

---

### 36. `docker import < file.tar>`

**Kaam:** Tar file se new image banata hai.
**Example:**

```bash
docker import app.tar my-app
```

---

### 37. `docker history <image>`

**Kaam:** Image banne ka history dikhata hai (layers, size, etc).
**Example:**

```bash
docker history nginx
```

---

### 38. `docker buildx`

**Kaam:** Multi-platform builds aur advanced build options ke liye use hota hai.
**Example:**

```bash
docker buildx build --platform linux/amd64,linux/arm64 -t my-app .
```

---

### 39. `docker context`

**Kaam:** Multiple Docker contexts (remote/local engines) ke beech switch karne ke liye.
**Example:**

```bash
docker context ls
```

---

### 40. `docker login --username <username> --password <password>`

**Kaam:** DockerHub me login karne ka CLI shortcut.
**Example:**

```bash
docker login --username myuser --password mypass
```

---

