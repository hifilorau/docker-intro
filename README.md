Building and running a React app inside of Docker using Docker Compose can help you manage multiple containers and their dependencies. Here's a short tutorial on how to do it:

Create a new React app: Use the create-react-app command to create a new React app. Open a terminal window and run the following command:

```
npx create-react-app my-app
```

This will create a new React app called my-app.

Create a Dockerfile: In the root directory of your React app, create a new file called Dockerfile and add the following code:

```
FROM node:latest

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

This Dockerfile sets the base image as the latest Node.js image, creates a working directory called /app, copies the package.json and package-lock.json files to the working directory, runs npm install to install dependencies, copies the entire contents of your React app to the container, exposes port 3000, and runs npm start to start the React app.

Create a docker-compose.yml file: In the root directory of your React app, create a new file called docker-compose.yml and add the following code:

```
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    environment:
      - NODE_ENV=development
    command: npm start
    
```

This docker-compose.yml file defines a service called app which builds the Docker image using the Dockerfile in the current directory, maps port 3000 in the container to port 3000 on your local machine, mounts the current directory to the /app directory in the container, sets the NODE_ENV environment variable to development, and runs the npm start command.

Build and run the Docker container: In the terminal window, navigate to the root directory of your React app and run the following command to build and run the Docker container:

```
docker-compose up
```

This command builds the Docker image and starts the Docker container. You should see the React app running in your terminal window.

View the React app: Finally, open your web browser and navigate to http://localhost:3000 to view your React app running inside of the Docker container.
That's it! You've successfully built and run your React app inside of Docker using Docker Compose.
