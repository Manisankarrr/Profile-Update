 Demo App - Developing with Docker
This demo app showcases a simple User Profile Application set up using:

index.html with pure JavaScript and CSS

Node.js backend with Express framework

MongoDB for data storage

All components are containerized with Docker.

🐳 Running the Application with Docker
Step 1: Create a Docker Network
bash
Copy
Edit
docker network create mongo-network
Step 2: Start MongoDB Container
bash
Copy
Edit
docker run -d \
  --name mongodb \
  --network mongo-network \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  mongo:4.2.1
Step 3: Start Mongo-Express Container
bash
Copy
Edit
docker run -d \
  --name mongo-express \
  --network mongo-network \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_SERVER=mongodb \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  -e ME_CONFIG_BASICAUTH_USERNAME=admin \
  -e ME_CONFIG_BASICAUTH_PASSWORD=password \
  mongo-express:0.49
Note:
Creating a separate Docker network is optional.
If you use the default network, omit the --network flag in the above commands.

Step 4: Access Mongo-Express
Visit http://localhost:8081 in your browser.

Create a user-account database.

Inside it, create a users collection.

Step 5: Start the Node.js Application
Navigate to the project’s backend directory:

bash
Copy
Edit
npm install
node server.js
Step 6: Access the Frontend
Open http://localhost:3000 in your browser.

🐳 Running the Application with Docker Compose
Step 1: Start MongoDB and Mongo-Express
bash
Copy
Edit

to start:
docker-compose -f docker-compose.yaml up
to stop:
docker-compose -f docker-compose.yaml down

Mongo-Express will be available at http://localhost:8080.

Step 2: Setup Database and Collection
In Mongo-Express:

Create a database named user-account.

Create a collection named users inside my-db.

Step 3: Start the Node.js Application
bash
Copy
Edit
npm install
node server.js
Access the app at http://localhost:3000.

🛠️ Building a Docker Image for the Application
To build a custom Docker image:

bash
Copy
Edit
docker build -t my-app:1.0 .
The . at the end points to the location of the Dockerfile.

📌 Notes
Ensure Docker and Node.js are installed on your machine.

MongoDB credentials used in this app are basic for demonstration purposes.
In production environments, always secure your databases properly.

