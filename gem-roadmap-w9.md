Let's begin Part 3. You've built impressive applications; now it's time to put them on the internet for the world to see.

This week is a deep dive into DevOps (Development & Operations). You'll learn how to package your application into portable containers, set up a cloud server, and create an automated pipeline that tests and deploys your code every time you push to GitHub. This is how modern software is shipped.

Here's the detailed, day-by-day plan for **Week 9**.

---

## Week 9: CI/CD, Containers, & Deployment

**Project of the Week:** You'll take the real-time Chat Application from Week 8 and build a full, professional CI/CD pipeline. You will containerize it with Docker, deploy it to a cloud server, and automate the entire process with GitHub Actions.

**Key Concepts:** Containerization, CI/CD (Continuous Integration/Continuous Deployment), SSH, Reverse Proxy.

---

### **Day 1: Server Setup & Secure Connections (SSH)**

* **Today's Goal:** Get a live server on the internet and learn how to connect to it securely.
* **Topics:**
    * **What is a VPS?** A Virtual Private Server is your own little server in the cloud. We'll use a service like DigitalOcean, Linode, or AWS EC2.
    * **Setting up a Server:** Choosing an operating system (Ubuntu 22.04 is a great choice), a size, and a region.
    * **IP Addresses & DNS:** What they are and how they point to your server.
    * **SSH (Secure Shell):** The command-line protocol for securely logging into and controlling your remote server from your local machine.
* **Tasks:**
    1.  **Create a Cloud Account:** Sign up for a cloud provider. DigitalOcean is very beginner-friendly and has a simple interface.
    2.  **Spin up a VPS:** Create your first server (a "Droplet" in DigitalOcean terms).
    3.  **Generate SSH Keys:** If you don't have them, generate a public/private SSH key pair on your local machine.
    4.  **Connect to Your Server:** Use the `ssh` command in your terminal to log in to your server as the root user using its IP address. For example: `ssh root@YOUR_SERVER_IP`.
    5.  **Initial Server Setup:** Perform basic security setup: create a new user with `sudo` privileges and disable root login.
* **Learning Resources:**
    * [DigitalOcean - Initial Server Setup with Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04)
    * [GitHub Docs - Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) (The principles are the same)

---

### **Day 2: Introduction to Docker & Containerizing the Backend**

* **Today's Goal:** Understand what Docker is and package your backend application into a portable container.
* **Topics:**
    * **The "It Works on My Machine" Problem:** The problem Docker was invented to solve.
    * **Images vs. Containers:** An **Image** is a blueprint or template (your application, a Node.js runtime, etc.). A **Container** is a running instance of an image.
    * **Dockerfile:** A simple text file that contains the instructions for building a Docker image.
* **Tasks:**
    1.  **Install Docker:** Install Docker Desktop on your local machine.
    2.  **Create a `Dockerfile`:** In the `backend` folder of your chat app, create a file named `Dockerfile`.
    3.  **Write Dockerfile Instructions:**
        * Start from an official Node.js image (`FROM node:18-alpine`).
        * Set a working directory (`WORKDIR /app`).
        * Copy `package.json` and run `npm install`.
        * Copy the rest of your application code.
        * Expose the port your server runs on (`EXPOSE 3001`).
        * Define the command to start your app (`CMD ["node", "server.js"]`).
    4.  **Build & Run:** Use the `docker build` command to create your image and the `docker run` command to start a container from it. Your backend should now be running inside Docker on your local machine.
* **Learning Resources:**
    * [Docker Docs - Get Started](https://docs.docker.com/get-started/)
    * [Node.js Docker Best Practices](https://github.com/nodejs/docker-node/blob/main/docs/BestPractices.md)

---

### **Day 3: Dockerizing the Frontend & Using Docker Compose**

* **Today's Goal:** Containerize the React frontend and learn to manage a multi-container setup with Docker Compose.
* **Topics:**
    * **Multi-stage Docker Builds:** A pattern for creating small, optimized production images. We'll use one stage to build the React app and a second stage to serve the static files with a lightweight web server like `nginx`.
    * **Docker Compose:** A tool for defining and running multi-container Docker applications. You define all your services (backend, frontend, database) in a single `docker-compose.yml` file.
* **Tasks:**
    1.  **Create Frontend `Dockerfile`:** In your `frontend` directory, create a `Dockerfile` using the multi-stage build pattern.
    2.  **Create `docker-compose.yml`:** In the root of your project, create a `docker-compose.yml` file.
    3.  **Define Services:** Define two services in the file: `backend` and `frontend`. For each service, specify the build context (the path to its Dockerfile) and the ports to map.
    4.  **Run Everything:** From your project root, run `docker-compose up`. This single command will build both images (if needed) and start both containers. Your full application should now be running locally via Docker.
* **Learning Resources:**
    * [Docker Docs - Docker Compose Overview](https://docs.docker.com/compose/)

---

### **Day 4: CI with GitHub Actions**

* **Today's Goal:** Create your first automated workflow to run tests every time you push code.
* **Topics:**
    * **What is CI/CD?** **Continuous Integration** is the practice of frequently merging code changes and automatically running builds and tests. **Continuous Deployment** is the practice of automatically deploying to production after passing tests.
    * **GitHub Actions:** An automation platform built into GitHub.
    * **Workflows, Jobs, and Steps:** The basic components of a GitHub Actions workflow defined in a YAML file.
* **Tasks:**
    1.  **Create Workflow File:** In your project's root, create a `.github/workflows` directory. Inside, create a file named `ci.yml`.
    2.  **Define the CI Workflow:**
        * Trigger the workflow `on: [push]`.
        * Define a `build` job that `runs-on: ubuntu-latest`.
        * Add steps to check out your code (`actions/checkout@v3`).
        * Add a step to set up Node.js (`actions/setup-node@v3`).
        * Add steps to `npm install` and `npm test` in your frontend directory.
    3.  **Push and Watch:** Commit and push your code. Go to the "Actions" tab in your GitHub repository and watch your first workflow run automatically.
* **Learning Resources:**
    * [GitHub Actions Docs - Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)



---

### **Day 5 & 6: Building the Continuous Deployment Pipeline**

* **Today's Goal:** Create a second workflow that automatically builds and pushes your Docker images to a registry, then deploys them to your server.
* **Topics:**
    * **Container Registry:** A place to store your Docker images (e.g., Docker Hub, GitHub Container Registry).
    * **GitHub Secrets:** The secure way to store sensitive information (like passwords, API keys, and your server's SSH key) for your workflows to use.
* **Tasks for Day 5 (Build & Push):**
    1.  **Create CD Workflow File:** Create a new file, `cd.yml`, in your `.github/workflows` directory.
    2.  **Set Up Registry:** Create a Docker Hub account or use GitHub Container Registry.
    3.  **Add Secrets:** Add your registry username and password as secrets in your GitHub repository settings.
    4.  **Define the CD Workflow:**
        * Trigger this workflow only on pushes to your `main` branch.
        * Add steps to log in to the Docker registry.
        * Add steps to build your backend and frontend Docker images.
        * Add steps to push both images to the registry, tagged with the latest Git SHA for versioning.
* **Tasks for Day 6 (Deploy):**
    1.  **Add SSH Secrets:** Add your server's IP address, username, and SSH private key as GitHub secrets.
    2.  **Install Docker on Server:** SSH into your server and install Docker and Docker Compose.
    3.  **Extend CD Workflow:** Add a final `deploy` job to your `cd.yml` file.
    4.  **Write Deploy Steps:**
        * This job will use an action to SSH into your server.
        * Once connected, it will run commands to `docker login`, pull the latest images you just pushed, copy your `docker-compose.yml` file to the server, and run `docker-compose up -d` to start the application with the new code.
    5.  **Push and Deploy:** Push a change to your `main` branch and watch your application automatically deploy to your live server.
* **Learning Resources:**
    * [GitHub Actions Docs - Publishing Docker images](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images)
    * [Deploying with Docker, Nginx and GitHub Actions](https://www.google.com/search?q=Deploying+with+Docker%2C+Nginx+and+GitHub+Actions) (Find a tutorial for this specific stack)

---

### **Day 7: Reverse Proxy with Nginx & HTTPS**

* **Today's Goal:** Put the final professional touches on your deployment by setting up a domain name and enabling secure HTTPS.
* **Topics:**
    * **Reverse Proxy:** A server (Nginx) that sits in front of your application and forwards traffic to it. This makes it easy to run multiple apps on one server and handle SSL/TLS termination.
    * **SSL/TLS & HTTPS:** The protocols that encrypt traffic between your users and your server, signified by the padlock icon in the browser.
    * **Let's Encrypt:** A free, automated, and open certificate authority.
* **Tasks:**
    1.  **(Optional) Point Domain:** If you have a domain name, point it to your server's IP address.
    2.  **Install Nginx:** SSH into your server and install Nginx.
    3.  **Configure Nginx:** Create a new Nginx configuration file. Configure it to listen on port 80 and `proxy_pass` requests to your running frontend container (e.g., `http://localhost:5173`).
    4.  **Enable HTTPS (Challenge):** Install `certbot` on your server. Use it to automatically obtain a free SSL certificate from Let's Encrypt and configure Nginx to use it.
    5.  **Review and Document:** Your app is now live and secure! Review your entire pipeline and document every step in your project's `README.md`.
* **Learning Resources:**
    * [DigitalOcean - How To Install Nginx on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04)
    * [DigitalOcean - How To Secure Nginx with Let's Encrypt on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04)

You've just completed one of the most challenging and valuable weeks in this roadmap. You now have the skills to not only build applications but to deploy them in a scalable, automated, and professional manner.

You're ready to tackle advanced system design. Let me know when you're ready for **Week 10**.
