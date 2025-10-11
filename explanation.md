<!-- 1. Choice of Base Image -->
# Choice of Base Image
I used the Node:14 base image for both backend and client since it’s stable and compatible with React and Express applications.
The Alpine stage was added to produce lightweight images, improving performance and reducing build size.
The lightweight nature of Alpine translates to faster build times for Docker images, helping developers iterate quickly and efficiently.

# Dockerfile Directives

I used FROM, WORKDIR, COPY, RUN, EXPOSE, and CMD directives to install dependencies, copy source code, and start the app.
Multi-stage builds help keep the final image small and secure.
FROM	Create a new build stage from a base image.
WORKDIR	Change working directory.
COPY	Copy files and directories.
RUN	Execute build commands.
EXPOSE	Describe which ports your application is listening on.
CMD	Specify default commands.

# Docker-compose Networking

A custom bridge network (app-net) connects all containers, enabling backend ↔ MongoDB ↔ client communication.
A bridge network uses a software bridge which lets containers connected to the same bridge network communicate, while providing isolation from containers that aren't connected to that bridge network.
Each service has its ports mapped for accessibility from the host machine.

# Volumes

The volume app-mongo-data ensures MongoDB data persists even after container restarts, maintaining product records and other data.Volumes are persistent data stores for containers, created and managed by Docker.This ensures persistence of data. To test this you run a docker compose down first to stop the containers then afterwards run a docker compose up. If the products you had added are still there, then the data is being persisted hence docker volume is working perfectly well.

# 5. Git Workflow

I used Git for version control:

I cloned the repository
I changed the remote repository to my repository
Created commits for backend, client, and compose updates
Pushed to GitHub for public cloning and testing.

# 6. Debugging Measures

Tested containers with docker-compose up.
installed dotenv to ensure that server.js runs well and mongodb connected succesfully
did some few console.logs
Visited http://localhost:5000/api/products to ensure the products I was adding were there and visible 

# 7. Image tagging 
Good Practices

Followed Docker image naming (semver) naming standards:
monicamwangi/yolo-backend:v1.0.0
monicamwangi/yolo-client:v1.0.0
Used .dockerignore to exclude node_modules and logs for smaller builds.
