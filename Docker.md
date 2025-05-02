
## ✅ Docker

Q1. **What is containerization and orchestration?**
  - **Containerization** refers to the practice of encapsulating an application and its dependencies into a container that can be executed consistently across different computing environments. Containers are lightweight and portable, allowing applications to run reliably when moved from one computing environment to another.
  - **Orchestration** involves managing and automating the deployment, scaling, and management of containers. Tools like Kubernetes and Docker Swarm provide container orchestration capabilities to manage large numbers of containers efficiently.

Q2. **What is a Docker image vs. a Docker container?**
  - A **Docker image** is a read-only template used to create Docker containers. It contains the application and its dependencies, including configuration files and libraries. An image is portable and can be shared across different systems.
  - A **Docker container** is a running instance of a Docker image. It is isolated and can be executed independently. Containers are created based on images and represent the active environment in which the application is running.

Q3 **How do you manage data persistence in Docker?**
  - Docker containers are ephemeral, meaning their data is lost once the container stops or is deleted. To manage data persistence:
    - **Volumes**: Persistent data is stored outside the container in volumes, which can be shared among multiple containers and survive container restarts or deletions
    - **Bind Mounts**: Data can be persisted by linking a container to a directory on the host system.
    - **Docker Compose**: Volumes can be defined and used to persist data in multi-container setups.

Q4 **Have you used Docker Compose?**
  - Yes, Docker Compose is a tool used for defining and running multi-container Docker applications. It allows you to use a YAML file to configure services, networks, and volumes, and it enables you to manage the entire lifecycle of multi-container applications with a single command.

Q5 **Explain a Dockerfile for a Node.js application.**
  - A Dockerfile is a script used to build a Docker image for an application. Here's an example for a Node.js application:
    ```Dockerfile
    # Use the official Node.js image as a base
    FROM node:14

    # Set the working directory inside the container
    WORKDIR /app

    # Copy package.json and package-lock.json to the working directory
    COPY package*.json ./

    # Install the application dependencies
    RUN npm install

    # Copy the rest of the application code
    COPY . .

    # Expose the port the app will run on
    EXPOSE 3000

    # Start the application
    CMD ["npm", "start"]
    ```
    This Dockerfile installs the required dependencies and exposes the app to port 3000 inside the container.

Q6 **How do you scan Docker images for vulnerabilities?**
  - Vulnerabilities in Docker images can be scanned using tools like:
    - **Docker Scan**: Built-in security scanning tool that checks images for known vulnerabilities.
    - **Clair**: Open-source project for static analysis of vulnerabilities in application containers.
    - **Anchore**: A container scanning tool that inspects container images for vulnerabilities.
    - **Trivy**: A comprehensive security scanner for Docker images and filesystems.

Q7 **Explain multi-stage builds in Docker and their benefits.**
  - **Multi-stage builds** allow you to create smaller, more efficient Docker images by using multiple `FROM` instructions in a Dockerfile. Each stage can be used to build dependencies or compile code, while the final image only contains the runtime environment, reducing the image size.
    Example:
    ```Dockerfile
    # Stage 1: Build stage
    FROM node:14 AS build-stage
    WORKDIR /app
    COPY . .
    RUN npm install

    # Stage 2: Production stage
    FROM node:14-slim
    WORKDIR /app
    COPY --from=build-stage /app .
    EXPOSE 3000
    CMD ["npm", "start"]
    ```
    The benefit is a smaller final image, with only the necessary files included in the final production image.

Q8 **How do you handle secrets in a CI pipeline when building Docker images?**
  - Secrets should never be hard-coded into Dockerfiles. Instead, use secure methods like:
    - **Docker Secrets**: Store and access sensitive data securely in Docker Swarm or Kubernetes.
    - **Environment Variables**: Use environment variables to inject secrets into containers during build or runtime (but ensure they are not exposed in the final image).
    - **HashiCorp Vault**: Integrate with secret management tools like Vault to manage sensitive information securely.
    - **CI/CD Secrets Management**: Use the secret management capabilities of CI/CD platforms (e.g., Jenkins, GitLab CI) to inject secrets during build or deployment without exposing them in Dockerfiles.

Q9 **What’s the impact of using `:latest` in production?**
  - Using the `:latest` tag in production is discouraged as it can lead to unintentional updates or incompatibilities. `:latest` refers to the most recent version of an image, and the image may change over time. This could introduce breaking changes in your application, making it difficult to ensure stability and reproducibility in production environments.
  - Instead, it's recommended to use specific version tags (e.g., `node:14.17.0`) to guarantee consistent behavior across different environments.

Q10. **How to log in to a Docker container?**
  - You can log in to a running Docker container using the following command:
    ```bash
    docker exec -it <container_id> /bin/bash
    ```
    This command opens an interactive shell session inside the container, allowing you to execute commands inside it.

Q11. **Can you install `vim` in a running container?**
  - Yes, you can install `vim` or other tools in a running container by executing:
    ```bash
    docker exec -it <container_id> /bin/bash
    apt-get update && apt-get install vim  # For Debian/Ubuntu-based containers
    ```
    However, it’s better to modify the Dockerfile to install necessary tools at build time for a reproducible environment.

Q12. **How to ensure Jenkins service runs after container restart?**
  - To ensure the Jenkins service keeps running after a container restart, you can use Docker’s restart policies. For example, the `--restart` flag can be added when running the container:
    ```bash
    docker run -d --restart unless-stopped jenkins/jenkins
    ```
    This ensures the Jenkins container automatically restarts unless manually stopped.

Q13. **What is the default network in Docker?**
  - The default network in Docker is the **bridge** network. When a container is created without specifying a network, it is connected to the bridge network. This allows containers to communicate with each other via internal IP addresses, while the host system can access the containers using port mappings.

Q14. **Explain Docker network types.**
  - Docker supports several types of networks:
    - **Bridge**: The default network type, used for standalone containers that communicate via the host system.
    - **Host**: The container shares the host’s network namespace, meaning it has the same IP address as the host.
    - **Overlay**: Used in Docker Swarm or Kubernetes clusters to allow containers running on different hosts to communicate.
    - **None**: No network access. Containers with this network type do not have network access unless explicitly configured.
    - **Container**: Allows one container to share another container’s network stack.

Q15. **What happens if you delete `/var/lib/docker/overlay`?**
  - Deleting the `/var/lib/docker/overlay` directory would remove the Docker overlay filesystem, which is used to manage container file systems. This could break running containers or cause them to lose their data. It’s essential to avoid deleting this directory unless you're certain you want to clear all container data.

Q16. **Write a Dockerfile to deploy a static web server.**
  ```Dockerfile
  # Use an official Nginx image as the base
  FROM nginx:alpine

  # Copy the website files to the Nginx default directory
  COPY ./html /usr/share/nginx/html

  # Expose port 80 for web traffic
  EXPOSE 80

  # Nginx will automatically serve the files
  CMD ["nginx", "-g", "daemon off;"]



                    ## Docker Question & Answers ##
1. What are the steps involved in Docker file ?

2. What are the custom images in Docker ?

3. Diff b/w CMD,RUN and ENTRYPOINT ?
Eg: Given:
ENTRYPOINT ["echo"]
CMD ["HELLO-WORLD"]

4. Diff b/w ADD & COPY ?

5. What are the targets in docker-compose ?

6. What steps can you take to reduce the size of a Docker image?

7. What are the pros and cons of using Alpine images?

8. How will you optimize a Dockerfile?

9. 
