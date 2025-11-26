## 🚀 Demo App – Developing with Docker & Pushing Images to a Registry

This demo app is a simple user profile application built with:
- 🎨 Plain JavaScript and CSS for the UI
- 🟩 Node.js backend using Express
- 🍃 MongoDB for data storage
- 🐳 Fully containerized services using Docker

All components are docker-based

### 🐳 Run with Docker

#### To start the application

1️⃣ Create a Docker network

    docker network create mongo-network 

2️⃣ Start MongoDB

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo    

3️⃣ Start Mongo Express
    
    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb -e ME_CONFIG_MONGODB_URL=mongodb://mongodb:27017 mongo-express   

4️⃣ Open Mongo Express

 👉 http://localhost:8081

5️⃣ Create DB & Collection 
  - Database: user-account
  - Collection: users

6️⃣ Start Node.js app

    cd app
    npm install 
    node server.js
    
7️⃣ Access the UI

👉 http://localhost:3000

### ⚙️ Run with Docker Compose

#### 🧱 Start the Application (Detailed Steps)

🟦 Step 1: Start MongoDB and Mongo Express

    docker-compose -f docker-compose.yaml up
    
Mongo Express UI will be available at:
👉 http://localhost:8080
    
🟩 Step 2: Create a new database
   In Mongo Express UI:
-  Create a database named user-account

🟩 Step 3: Create a collection
    Inside the user-account database:
-   Create a collection named users
    
🟦 Step 4: Start the Node.js server
    cd app
    npm install
    node server.js
    
🟩 Step 5: Access your Node.js application

👉 http://localhost:3000

#### 🏗️ Build a Docker Image from the Application

    docker build -t my-app:1.0 .       
    
The dot "." at the end of the command denotes location of the Dockerfile.


###  📦 Build and Push the Image (Elastic Container Registry)

1️⃣ Build the image
   docker build -t my-app:1.1 .

2️⃣ Authenticate to ECR
Replace <aws-account-id>, <region>, and <repo>:

    aws ecr get-login-password --region <region> \  | docker login --username AWS --password-stdin <aws-account-id>.dkr.ecr.<region>.amazonaws.com

3️⃣ Authenticate
    docker push <aws-account-id>.dkr.ecr.<region>.amazonaws.com/<repo>:1.1




