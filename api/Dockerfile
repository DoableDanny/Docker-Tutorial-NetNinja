# Layer 1
# First, we pull the parent image. The `FROM` command defines the base image.
# If this image isn't available locally, Docker will pull it from DockerHub.
# `node:17-alpine` specifies that we want Node.js version 17 on a lightweight Alpine Linux distribution.
FROM node:17-alpine

# Layer 2
# Install Nodemon globally. This command runs during the image build process and adds Nodemon, a tool for restarting Node.js apps automatically when file changes are detected.
RUN npm i -g nodemon

# Layer 3
# Set the working directory inside the container to `/app`. Any subsequent command that references paths will be relative to `/app`.
# This is where we will place our app's files.
WORKDIR /app

# Layer 4
# Copy `package.json` and `package-lock.json` (if present) into the container's `/app` directory.
# This ensures that we only install the necessary dependencies based on the `package.json` before copying the entire project (reducing cache invalidation).
COPY package.json .

# Layer 5
# Install the dependencies specified in `package.json` inside the container.
# This allows us to install dependencies separately before adding the rest of the source code, optimizing the build cache.
RUN npm install

# Layer 6
# Copy the rest of the application source code from the current directory (host machine) to `/app` inside the container.
# The `.` refers to the current directory on your machine, and the second `.` refers to the `/app` directory in the container, relative to the `WORKDIR`.
COPY . .

# Layer 7
# Expose port 4000, meaning this port inside the container will be available to the host machine.
# This does not publish the port directly but serves as documentation and a hint for Docker to map the container's port 4000 to a port on the host during runtime.
EXPOSE 4000

# Layer 8
# Specify the default command to run when a container is instantiated from this image.
# `CMD` runs at container runtime and, in this case, starts the app in development mode using Nodemon. This command will only execute when the container is started.
CMD ["npm", "run", "dev"]
