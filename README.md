
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

```Dockerfile
# === Base stage (dependencies only)
FROM node:18-alpine as base
WORKDIR /app
COPY package*.json ./
RUN npm install

# === Development stage
FROM base as development
COPY . .
CMD ["npm", "run", "dev"]

# === Production stage
FROM base as production
COPY . .
RUN npm run build
CMD ["node", "src/index.js"]
```

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
