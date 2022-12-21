# Dockerfile

As with any project, we first have to build out the basics of the application. The **ChatGPT Built App** can be run in various ways and so we need to add the
necessary components in order to do this. The first step is to create a **Dockerfile**. This is a text file that contains all the commands a user could 
call on the command line to assemble an image. We will use this file to create a Docker image that will run our application.

The Question:
> So I've created the basic structure using nest.js and so now have a starting template, I'm going to use a folder called api for the REST, 
> in order to keep some variation in the backend and so making it simpler to work with. One of the initial files I need to create is a Dockerfile, 
> to deploy the backend to our docker server. So how would I build this dockerfile and please show full examples.

The Answer:
> To build a Dockerfile for your Nest.js backend, you'll need to specify a base image to use as the foundation for your Docker container. You can 
> use an official Node.js image from the Docker Hub, or you can use a third-party image that includes Node.js and other dependencies pre-installed.
> 
> Once you've chosen a base image, you'll need to copy your application files into the container, install any dependencies, and specify a command to 
> run when the container is started.
> 
>Here's an example of a Dockerfile that you can use as a starting point for your Nest.js backend:

Code:
```code
FROM node:12

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "npm", "start" ]

```

>This Dockerfile does the following:
> - Uses the node:12 image as the base image for the container.
> - Creates a working directory for the app at /usr/src/app.
> - Copies the package.json and package-lock.json files into the working directory.
> - Installs the app dependencies using npm install.
> - Copies the rest of the application files into the working directory.
> - Exposes port 3000, which is the default port used by Nest.js.
> - Specifies the command npm start to run when the container is started. This command will start the Nest.js server.
>
> To build your Docker image, navigate to the directory containing your Dockerfile and run the following command:

Code
```code
docker build -t my-nest-app .
```

> This will build a Docker image with the name my-nest-app using the instructions in the Dockerfile. Once the image is built, you can run it using the following command:

Code:
```code
docker run -p 3000:3000 my-nest-app
```

> This will start a container based on the my-nest-app image, and map port 3000 on the host machine to port 3000 on the container. 
> The Nest.js server will start and be accessible at http://localhost:3000 on the host machine.
