## Building our own Docker Image

### Below are the steps to build a Docker image for a Node.js application:

Step 1: Create a new file named Dockerfile in the project directory with the following contents:

        FROM node:13-alpine

    ENV MONGO_DB_USERNAME=admin \
        MONGO_DB_PWD=password

    RUN mkdir -p /home/app

    COPY ./app /home/app

    # set default dir so that next commands executes in /home/app dir
    WORKDIR /home/app

    # will execute npm install in /home/app because of WORKDIR
    RUN npm install

    # no need for /home/app/server.js because of WORKDIR
    CMD ["node", "server.js"]
   
Step 2: This Dockerfile specifies that we will use the official Node.js image from Docker Hub as our base image, set the working directory to /app, copy the package.json and package-lock.json files to the working directory and install dependencies. Then, copy the rest of the application code to the working directory, expose port 3000 for the application to listen on, and start the application with npm start.

Note: Make sure your Node.js application code is located in the same directory as the Dockerfile.

Step 3: Build the Docker image by running the following command in the terminal:

    docker build -t my-app:1.0 .

Step 4: This will build a new Docker image with the name "my-app:1.0" using the Dockerfile in the current directory (.).

Step 5: After the build process completes successfully, you can run the Docker image by running the following command in the terminal:

    docker run my-app:1.0
    
 This will start a new Docker container using the image we just built and map port 3000 in the container to port 3000 on your local machine. You should now be able to access your Node.js application by visiting http://localhost:3000 in your web browser.

That's it! You have now successfully built a Docker image for your Node.js application.



  
