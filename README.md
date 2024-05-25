# Scanning Localhost Application with Docker ZAP

[![YouTube Video](./thumbnail.svg)](https://www.youtube.com/watch?v=j9vqvzBPVMw)

## Table of Contents

1. [Introduction](#introduction)
2. [Key Features of ZAP](#key-features-of-zap)
3. [Benefits of Using ZAP for DAST](#benefits-of-using-zap-for-dast)
4. [Getting Started with ZAP](#getting-started-with-zap)
5. [Setting up TIWAP](#setting-up-tiwap)
6. [Docker Installation Instructions](#docker-installation-instructions)
7. [Execution Instructions](#execution-instructions)

## Introduction

Dynamic Application Security Testing (DAST) is a type of security testing that involves testing an application in its running state. Unlike static analysis, which examines the source code, DAST scans an application from the outside in, simulating an attacker’s perspective. This approach helps identify vulnerabilities that might be exploited in a real-world attack scenario, such as SQL injection, cross-site scripting (XSS), and other web application vulnerabilities.

One of the most popular tools for performing DAST is the Zed Attack Proxy (ZAP), an open-source security scanner maintained by the Open Web Application Security Project (OWASP). ZAP is designed to be easy to use, even for those new to application security, while also providing powerful features for advanced users.

## Key Features of ZAP

- **Automated Scanning**: ZAP can automatically scan web applications for security vulnerabilities.
- **Passive Scanning**: Monitors HTTP traffic and passively scans for vulnerabilities without altering the request-response cycle.
- **Active Scanning**: Actively probes the web application for vulnerabilities by sending various types of malicious requests.
- **Spidering**: Crawls the web application to discover all the pages and endpoints that need to be tested.
- **API Integration**: Provides a robust API that allows for integration with CI/CD pipelines for continuous security testing.
- **Extensibility**: Supports various add-ons and plugins to extend its functionality.

## Benefits of Using ZAP for DAST

1. **Comprehensive Coverage**: ZAP can identify a wide range of vulnerabilities, including those listed in the OWASP Top Ten.
1. **Ease of Use**: Its intuitive interface and extensive documentation make it accessible for beginners.
1. **Community Support**: Being an OWASP project, ZAP benefits from a large community of contributors and users who help in improving and updating the tool.
1. **Cost-Effective**: As an open-source tool, ZAP is free to use, making it an attractive option for organizations of all sizes.

## Getting Started with ZAP

To start using ZAP for DAST scanning, follow these steps:

1. **Download and Install ZAP**: ZAP is available for Windows, macOS, and Linux. You can download it from the [official ZAP website](https://www.zaproxy.org/download/).
1. **Configure Your Browser**: Set up your web browser to use ZAP as a proxy to capture and inspect the HTTP traffic.
1. **Start Scanning**: Use ZAP's spidering and scanning features to discover and test the web application's endpoints for vulnerabilities.
1. **Review and Mitigate**: Analyze the scan results to identify vulnerabilities and take appropriate actions to mitigate them.

## Setting up TIWAP

Sure! Here are the improved instructions with more clarity and additional details for each step:

### Step-by-Step Instructions to Set Up the Web Application

1. **Clone the GitHub Repository**

   First, clone the repository to your local machine. Open your terminal and run the following command:

   ```bash
   git clone https://github.com/The-DevSec-Blueprint/TIWAP.git 
   ```

   This command downloads all the project files from the GitHub repository to a directory named `TIWAP` on your local machine.

1. **Navigate to the Project Directory**

   After cloning the repository, navigate into the project directory:

   ```bash
   cd TIWAP
   ```

   This changes your current directory to the `TIWAP` directory, where the project files are located.

1. **Run Docker Compose to Spin Up the Web Application**

   Use Docker Compose to build and start the web application. Make sure Docker is installed and running on your system. Then run:

   ```bash
   docker-compose up -d
   ```

   This command uses the `docker-compose.yml` file to build the Docker containers and start the application in detached mode (running in the background).

1. **Verify the Application is Running**

   After running the Docker Compose command, verify that the application is running. Open your web browser and navigate to:

   ```bash
   http://localhost:8000
   ```

   You should see the web application up and running.

## Docker Installation Instructions

In order for you to run any of these commands, you'll need to have Docker installed. You can view the instructions here: [Get Docker: Installation Instructions](https://docs.docker.com/get-docker/).

## Execution Instructions

### Step 1: Pull the ZAP Docker Image

First, ensure you have Docker installed and running on your system. Then, pull the latest OWASP ZAP Docker image:

```bash
docker pull owasp/zap2docker-stable
```

### Step 2: Start Your Localhost Application

Make sure your local application is running on localhost. For example, if it's a web application, it might be accessible at `http://localhost:8000`.

### Step 3: Run the ZAP Scan

Use the following command to run the ZAP scanner against your localhost application. This command assumes your application is accessible on port 8080. Adjust the port number accordingly if your application uses a different port.

- Linux/Unix

    ```bash
    docker run -v $(pwd):/zap/wrk/:rw --network="host" zaproxy/zap-stable zap-baseline.py -t https://localhost:8000 -r scan-report.html
    ```

- Windows Powershell

    ```cmd
    docker run -v ${PWD}:/zap/wrk/:rw --network="host" zaproxy/zap-stable zap-baseline.py -t https://localhost:8000 -r scan-report.html
    ```

#### Explanation of the Command

- `-v $(pwd):/zap/wrk/:rw`: This option mounts the current directory (`$(pwd)`) to the `/zap/wrk/` directory inside the container. The report will be saved in this directory.
- `--network="host"`: This tells Docker to use the host's network, allowing the Docker container to access `localhost`.
- `zap-full-scan.py`: This is a script provided by ZAP for running a full scan, which performs a deeper and more thorough scan. It will take a while though....
- `-t http://localhost:8000`: Specifies the target URL for the scan.
- `-r scan-report.html`: Specifies the name of the report file to generate.

### Step 4: Retrieve the HTML Report

Once the scan is complete, an HTML report named `scan-report.html` will be saved in your current working directory. You can open this file in any web browser to view the detailed security scan report.

### Additional Tips

- **Scan Duration**: Depending on the complexity and size of your application, the scan may take some time. Ensure your application remains running until the scan is completed.
- **Security Considerations**: Regularly update the Docker image with `docker pull owasp/zap2docker-stable` to ensure you are using the latest security checks and features.
