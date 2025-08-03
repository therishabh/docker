# Docker

| S.No. | Section |
|---------|-------------|
| 1.  | [Explanation of basic Dockerfile](#explanation-of-basic-dockerfile) |
| 2.  | [Show list of Docker Images](#show-list-of-docker-images) |




## Explanation of basic Dockerfile
````
FROM node:20

# Set the working directory inside the container
WORKDIR /myapp

# Copy package.json and package-lock.json to the working directory
COPY package*.json .

# Install the dependencies
RUN npm install

# Copy the rest of the application’s code
COPY . .

CMD ["npm", "start"]
````

This Dockerfile creates a containerized environment to run a Node.js application. Here’s a breakdown of each command:

1. **`FROM node:20`**
   - This line specifies the base image for the container. In this case, it’s the `node:20` image, which includes Node.js version 20. This image provides a compatible Node.js environment with all necessary binaries and dependencies, so you don’t have to install Node.js manually.

2. **`WORKDIR /myapp`**
   - This sets the working directory inside the container to `/myapp`. All subsequent commands in the Dockerfile are executed relative to this directory.
   - If the directory doesn’t exist, Docker will create it. Setting a working directory also keeps the container’s file structure organized.

3. **`COPY package*.json .`**
   - This command copies the `package.json` and `package-lock.json` files from your project directory (on your host machine) to the `/myapp` directory inside the container.
   - The `package*.json` pattern matches both `package.json` and `package-lock.json`, which define your app's dependencies and lockfile for reproducible installs.

4. **`RUN npm install`**
   - This installs the dependencies listed in `package.json`. The command runs `npm install` inside the `/myapp` directory of the container.
   - By copying `package.json` and `package-lock.json` first, Docker can cache the dependencies layer. If no changes are detected in `package.json`, Docker skips this step in future builds, making them faster.

5. **`COPY . .`**
   - This copies the remaining application files (all other files in the current directory) from the host machine to the container’s `/myapp` directory. With this step, the entire application codebase is available inside the container.

6. **`CMD ["npm", "start"]`**
   - This specifies the default command to run when the container starts. `CMD` executes `npm start`, which is defined in `package.json` (often as a script that runs the app, like `node server.js`).
   - This command ensures the application starts automatically when the container is launched.

Together, these commands set up and run a Node.js app inside a container by copying files, installing dependencies, and then executing the start script.

----------------------
----------------------

## Show list of docker images

````
docker image ls
````

Is command `docker image ls` ka use system par available **Docker images** ko list karne ke liye hota hai. Is command ke zariye aapko aapke system par stored sabhi Docker images ke baare mein information milti hai.

**`docker image ls`**:
   - Yeh command sabhi Docker images ko list karta hai jo aapne pull, build, ya create kiye hain.
   - `ls` ka matlab hota hai "list".

##### Example Output:
```bash
REPOSITORY          TAG           IMAGE ID       CREATED         SIZE
mywebapp            latest        a3d5c73a2f6b   2 days ago      132MB
ubuntu              20.04         3b418d7b4669   5 days ago      72.9MB
nginx               stable        b233aaa2ef38   1 week ago      23.1MB
```

##### Additional Options:
- **`docker image ls -a`**: Yeh command **sabhi images** ko dikhata hai, including intermediate (dangling) images jo puri tarah se remove nahi hue hote.
- **`docker image ls --filter dangling=true`**: Sirf un images ko list karta hai jo Docker ke intermediate build steps se bachi hoti hain, jo ab use nahi ho rahi.

-----------------------------------



## Explain command
````
docker run --rm -d --name "my_container" -p 3003:3000 e9f98515e2be
````

1. **`docker run`**: 
   Matlab hum ek naya Docker container start kar rahe hain.

2. **`--rm`**: 
   Yeh flag bolta hai ki jab container ka kaam khatam ho jaayega, toh Docker us container ko automatically delete kar dega. Iska matlab hai ki yeh container temporary hai.

3. **`-d`**: 
   Iska matlab hai ki container ko background mein chalao (detached mode). Matlab aapko terminal par koi output nahi dikhai dega, aur container background mein apna kaam karta rahega.

4. **`--name "my_container"`**: 
   Isse hum apne container ka naam de rahe hain. Is example mein, container ka naam `my_container` hai. Naam dene se aapko container ko baad mein easily identify karne mein madad milegi.

5. **`-p 3003:3000`**: 
   Yeh flag ports ko map karne ke liye use hota hai. Yahan par aap local machine ka port `3003` container ke andar ke port `3000` ke saath connect kar rahe hain. Matlab agar aap browser mein `localhost:3003` kholenge, toh aap container ke andar chal rahe app ke port `3000` se connect ho jayenge.

6. **`e9f98515e2be`**: 
   Yeh container ka image ID hai. Yeh ek specific Docker image ka reference hai jisse aapka container bana hai.

To overall, yeh command ek container ko background mein run karegi, uska naam `my_container` hoga, aur local machine ka port `3003` container ke `3000` port se connected hoga. Aur jab container ka kaam khatam ho jayega, toh woh automatic delete ho jayega.

-------------------

````
docker ps -a
````

`docker ps -a` command ka use aapke system par **sabhi Docker containers** (including those that are stopped) ko list karne ke liye hota hai. 

### Command Breakdown in Hinglish:

- **`docker ps`**:
  - Yeh command currently running Docker containers ko list karta hai.

- **`-a`**:
  - Is flag ka matlab hai **"all"** containers, including those jo abhi stopped ya exited state mein hain. Without `-a`, aapko sirf running containers dikhte.

### Example Output:

```
CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS                      PORTS      NAMES
c0ffee1d3a78   nginx        "/docker-entrypoint.…"   2 hours ago     Exited (0) 5 minutes ago               my_nginx
abcd12345efg   ubuntu       "/bin/bash"              3 days ago      Up 2 hours                            ubuntu_container
1234abcd5678   redis        "redis-server"           1 week ago      Exited (137) 6 days ago               redis_server
```

### Columns Explanation:
1. **CONTAINER ID**: Har container ka unique ID hota hai, yeh usko identify karne ke liye use hota hai.
2. **IMAGE**: Isme Docker image ka naam hota hai jo container run kar raha hai.
3. **COMMAND**: Jo command container start karne ke liye use hui thi, uska snippet dikhai deta hai.
4. **CREATED**: Container kitne time pehle create kiya gaya tha, yeh batata hai.
5. **STATUS**: Yeh column container ka current status batata hai. Status kuch bhi ho sakta hai, jaise `Up`, `Exited`, etc.
6. **PORTS**: Agar container ke ports map kiye gaye hain, toh yeh column us information ko dikhata hai.
7. **NAMES**: Isme container ka naam hota hai (jo aapne diya ho ya Docker ne automatically assign kiya ho).

### Use Case:
- Agar aapko dekhna hai ki kaun kaun se containers past mein run ho chuke hain, chahe wo ab stopped ho ya exited ho, toh aap `docker ps -a` use kar sakte hain.
  
Isse aapko pura history mil jata hai jo aapke system pe chale hue ya stopped containers ke baare mein hota hai.


-------------------
### Build a Docker image

````
docker build -t mywebapp:01 .
````

This command is used to **build a Docker image** from a **Dockerfile** present in the current directory (`.`). Here's the detailed explanation:

### Breakdown:

1. **`docker build`**:
   - Yeh command Docker image banane ke liye use hota hai, jo aapke system mein present **Dockerfile** ka use karke ek image create karta hai.
   
2. **`-t`**:
   - **Tag** flag ka short form hai. Iska matlab hai ki aap image ko ek naam aur version de rahe ho. Taaki baad mein aapko easily identify karne mein help mile.
   - Without `-t`, Docker image ko random generated name aur tag assign hota hai.

3. **`mywebapp:01`**:
   - **`mywebapp`**: Yeh image ka naam hai. Is case mein, aap apne image ko `mywebapp` naam de rahe hain.
   - **`:01`**: Yeh image ka **tag** ya version hai. `01` ka matlab hai ki yeh pehla version hai. Agar aap different versions banaoge, toh alag-alag tags use kar sakte ho, jaise `mywebapp:02`, `mywebapp:latest`, etc.

4. **`.` (dot)**:
   - Yeh **current directory** ko refer karta hai. Iska matlab hai ki Docker current directory se `Dockerfile` search karega aur uske base pe image banayega.
   - Dot ka use location specify karne ke liye hota hai jahan Dockerfile aur baaki build context present hote hain.

### Example Scenario:
Aapke paas ek `Dockerfile` hai jo web application ko define karta hai, aur aap chahte ho ki usse ek image banayein jisse baad mein containers run kiye ja sakein. Yeh command aapko image ka naam aur version define karne ka option deta hai, jo future mein aapko alag-alag versions ke liye helpful hoga.

### In Short:
- `docker build` -> Docker image build kar raha hai
- `-t mywebapp:01` -> Image ko naam "mywebapp" aur version/tag "01" de raha hai
- `.` -> Dockerfile current directory mein hai, aur isi se build hoga.

------------------
````
docker rmi my_test_image:02
````

The command `docker rmi my_test_image:02` ka use ek **Docker image** ko remove (delete) karne ke liye hota hai. Is command mein hum ek specific image ka naam aur uska tag de rahe hain, taaki Docker us image ko remove kar sake.

### Breakdown in Hinglish:

1. **`docker rmi`**:
   - **`rmi`** ka matlab hai **"remove image"**. Yeh command Docker images ko delete karne ke liye use hoti hai.
   - Is command se Docker image aapke local machine se remove ho jaati hai.

2. **`my_test_image:02`**:
   - **`my_test_image`**: Yeh image ka naam hai jo aap delete karna chahte ho.
   - **`:02`**: Yeh image ka **tag** hai. Aapne specific version ya tag `02` mention kiya hai. Agar image ke paas multiple tags hain, toh aap us tag ka naam specify karte ho jo delete karna hai.
   
   - Example: Agar `my_test_image` ke paas multiple versions hain, jaise `my_test_image:01`, `my_test_image:02`, etc., toh sirf `:02` tag wala image delete hoga.

### Overall Command Meaning:

Yeh command Docker ko bol raha hai ki **`my_test_image` ka version/tag `02`** ko aapke local system se delete kare. Agar image currently kisi running container mein use nahi ho raha, toh woh safely remove ho jayega. Agar image kisi container ke saath associated hai ya container us image par dependent hai, toh Docker error throw karega ya force remove ke liye `-f` flag add karna padega.

### Note:
- Agar aapko **sabhi tags** ke saath image delete karna hai, toh aap sirf `my_test_image` likh sakte hain.
- Example: `docker rmi my_test_image`



````
docker tag my_test_image:01 therishabh19/webapp-demo:02
````


The command `docker tag my_test_image:01 therishabh19/webapp-demo:02` ka use ek **existing Docker image** ko **naya naam** aur **naya tag** dene ke liye hota hai. Effectively, aap apne image ko ek new repository ya registry mein upload karne ke liye ready kar rahe hote ho.

1. **`docker tag`**:
   - **Tag** command ka use ek existing image ko naya naam ya tag dene ke liye hota hai, without actually copying the image. Aap sirf reference create karte ho.

2. **`my_test_image:01`**:
   - Yeh existing image ka naam aur tag hai. Is example mein, aap `my_test_image` ka **`01` version** (tag) ko naya tag dena chahte hain.

3. **`therishabh19/webapp-demo:02`**:
   - **`therishabh19`**: Yeh Docker Hub ya kisi bhi registry ka username hai. Agar aap Docker Hub pe image push karne wale hain, toh username ka hona zaroori hai.
   - **`webapp-demo`**: Yeh naya repository name hai jisme aap image ko upload karenge.
   - **`:02`**: Yeh naya tag (version) hai. Is command mein aap image ka version `02` define kar rahe hain.

### Command Ka Kya Matlab Hai?

Is command ka matlab hai ki aap **existing image** `my_test_image:01` ko **naya naam aur version** de rahe hain, jisme:
- Image ka **naya repository name** hoga: `therishabh19/webapp-demo`
- Aur **naya tag/version** hoga: `02`

### Example Scenario:

1. Aapke paas local machine pe ek image hai `my_test_image:01`, aur ab aap chahte hain ki ise **Docker Hub** pe push karen taaki doosre log bhi ise access kar sakein.
2. To push karne se pehle, aapko image ka naam aur tag ko Docker Hub ke compatible format mein change karna padta hai, jisme username/repository aur tag specified ho.
   
### Steps After Tagging:
1. **Image ko push karna**: 
   - Ab aap is tagged image ko Docker Hub ya kisi aur registry pe push kar sakte ho by using:
     ```bash
     docker push therishabh19/webapp-demo:02
     ```

2. **Docker Hub par upload ke baad**:
   - Aap aur doosre log ise pull kar sakte hain by running:
     ```bash
     docker pull therishabh19/webapp-demo:02
     ```

### In Short:
- **`docker tag`** command ka use ek image ko naya naam aur tag dene ke liye hota hai.
- Aap apni local image `my_test_image:01` ko `therishabh19/webapp-demo:02` naam aur tag ke saath mark kar rahe ho, jisse aap ise Docker Hub ya kisi aur registry pe upload kar sako.


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

---
