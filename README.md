# docker

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
