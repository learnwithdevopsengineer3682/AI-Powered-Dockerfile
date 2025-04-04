# AI-Powered-Dockerfile

AI-Powered Dockerfile Optimization with Mistral & Ollama
Project Overview
This project demonstrates how to optimize Dockerfiles using AI powered by the Mistral model with the Ollama CLI. The goal is to reduce the Docker image size and improve the build time by utilizing AI-driven optimizations. The demo includes:

Two Dockerfiles: One unoptimized and one optimized using Mistral.

GitHub Actions Pipelines: Automates the process of building and measuring the build time and image size.

Ollama CLI with Mistral: Optimizes the Dockerfile by suggesting improvements to reduce size and build time.

Features
Automated Dockerfile Optimization: Using the Mistral model via Ollama CLI.

Build Time Comparison: Measure the impact of optimizations on Docker build times.

Image Size Comparison: Show the before and after Docker image sizes.

GitHub Actions Integration: Set up pipelines to automate the process.

Free AI DevOps Resources: Share valuable links for learning more about AI and DevOps.

Prerequisites
Docker: Ensure Docker is installed on your machine or CI environment.

Ollama CLI: This project uses the Ollama CLI to run the Mistral model for optimization.

GitHub Account: To access GitHub Actions pipelines for CI/CD automation.

.
├── big/
│   └── Dockerfile  # Unoptimized Dockerfile
├── optimized/
│   └── Dockerfile  # Optimized Dockerfile using Mistral
├── .github/
│   └── workflows/
│       ├── big.yml   # GitHub Action for building the unoptimized Dockerfile
│       └── ai-optimized.yml  # GitHub Action for building the optimized Dockerfile
├── app.py  # Simple Python application used for the Docker image build
└── requirements.txt  # Required dependencies for app.py

How to Run the Project Locally
Step 1: Set Up the Environment
Ensure you have Docker installed and running on your local machine.

Install Docker: Follow the installation instructions from Docker’s official site.

Install Ollama CLI: You can install Ollama CLI from Ollama's official website.

Step 2: Clone the Repository

git clone https://github.com/yourusername/dockerfile-optimization.git
cd dockerfile-optimization

Step 3: Optimize Dockerfile Using Ollama & Mistral

CI/CD with GitHub Actions
This project includes GitHub Actions workflows to automate the process of building the Docker images and comparing the results.

Optimized dockerfile

Explanation:
1) Base Image:
FROM python:3.9-slim-buster
This line specifies the base image for the Docker container. Instead of using a large image like ubuntu:latest, this uses a smaller Python image based on Debian Buster (python:3.9-slim-buster). The slim variant is a minimal version of the Python image, making it lighter and faster to build.

2) Set Working Directory:
WORKDIR /app
This line sets the working directory inside the container to /app. Any subsequent commands, like COPY or RUN, will operate relative to this directory. If the /app directory doesn't exist, it will be created automatically.

3) Copy the requirements.txt File First:
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY requirements.txt .: This copies the requirements.txt file from your local system into the /app directory of the container.

RUN pip install --no-cache-dir -r requirements.txt: This installs the Python dependencies listed in requirements.txt using pip. The --no-cache-dir flag ensures that no cache is stored, reducing the image size. This step is done early in the build process to optimize Docker's cache mechanism. If the requirements.txt file hasn’t changed, Docker will cache the result, speeding up future builds.

4) Copy the Application Files:
COPY . .
This copies the rest of the application files (everything in the current directory) from the host machine to the /app directory in the container. By doing this after installing the dependencies, Docker can cache the dependency installation step and avoid reinstalling dependencies if only the application files change.

5) Expose Port 5000:
EXPOSE 5000
This line exposes port 5000 inside the container. This tells Docker that the container will be using this port for communication, usually for web applications that listen on port 5000 (e.g., Flask or other Python web frameworks). It doesn’t actually map the port to the host system; it's just a declaration. When you run the container, you would use the -p flag to bind the port to your host system.

6) Run the Application:
CMD ["python", "app.py"]
The CMD instruction defines the default command to run when the container starts. Here, it runs the Python application (app.py) using the python command. This will be the entry point for your application, so when you start the container, it will run this command automatically.

Summary of Optimization:
Smaller Base Image: Using python:3.9-slim-buster instead of ubuntu reduces the size of the image, making it lighter and faster to build.

Optimized Caching: The requirements.txt is copied and dependencies are installed before copying the rest of the application files. This takes advantage of Docker's caching mechanism to avoid reinstalling dependencies every time the application files change.

Efficient Layering: The layers are ordered efficiently, ensuring that the dependencies are cached and only updated when necessary   

Workflow 1: build-big.yml
Builds the unoptimized Dockerfile.

Measures the build time and Docker image size.

Workflow 2: ai-optimized.yml
Builds the optimized Dockerfile.

Measures the build time and Docker image size.

These workflows will automatically run when you push changes to the repository. You can find the workflows under the .github/workflows/ directory.

Free AI & DevOps Learning Resources
To get started with AI in DevOps, here are some free learning resources:

Practical MLOps by Google
[MLOps Continuous Delivery and Automation Pipelines](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning)

[Linux Foundation AI & DevOps Training](https://training.linuxfoundation.org/training/data-and-ai-fundamentals-lfs115x/)


License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgments
Ollama for providing the CLI interface to run Mistral.

Mistral for the AI model used in the Dockerfile optimization.