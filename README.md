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
