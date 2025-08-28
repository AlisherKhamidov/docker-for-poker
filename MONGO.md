Here’s a simple **Docker Compose** file to run MongoDB with persistence and an admin UI:

```yaml
version: "3.9"

services:
  mongo:
    image: mongo:6.0
    container_name: mongo
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    volumes:
      - mongo_data:/data/db

  mongo-express:
    image: mongo-express:1.0.0-20
    container_name: mongo-express
    restart: always
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: example
      ME_CONFIG_MONGODB_SERVER: mongo

volumes:
  mongo_data:
```

### Explanation:

* **mongo service**

  * Runs MongoDB 6.0
  * Root username: `root`, password: `example` (change these in real use)
  * Data persists via `mongo_data` volume

* **mongo-express service**

  * Lightweight web UI for MongoDB
  * Accessible at [http://localhost:8081](http://localhost:8081)
  * Uses the same credentials as the MongoDB root

* **volumes**

  * Stores MongoDB data outside the container so it won’t be lost when the container restarts

---

Do you want me to make this minimal (just MongoDB, no UI) or keep the `mongo-express` admin dashboard included?
