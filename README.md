# Scanning Localhost Application with Docker ZAP

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

<<<<<<< HEAD
1. **Download and Install Java**: Before installing ZAP, ensure that you have Java installed on your system, as ZAP requires Java to run. You can download and install the latest version of Java from the [official Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
=======
>>>>>>> a9e859d473d4d9799bf65137c4c23deacca7f113
1. **Download and Install ZAP**: ZAP is available for Windows, macOS, and Linux. You can download it from the [official ZAP website](https://www.zaproxy.org/download/).
1. **Configure Your Browser**: Set up your web browser to use ZAP as a proxy to capture and inspect the HTTP traffic.
1. **Start Scanning**: Use ZAP's spidering and scanning features to discover and test the web application's endpoints for vulnerabilities.
1. **Review and Mitigate**: Analyze the scan results to identify vulnerabilities and take appropriate actions to mitigate them.

<<<<<<< HEAD
## Post-Installation Configuration

1. **Java Configuration**:
    - Ensure that your system’s `JAVA_HOME` environment variable is set correctly. This is necessary for ZAP to locate your Java installation.

1. **Proxy Configuration**:
    - Configure your web browser to use ZAP as a proxy. This allows ZAP to intercept and analyze HTTP/HTTPS traffic.

By following these steps, you will have OWASP ZAP installed on your system, ready for use in security testing your web applications.
=======
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

```bash
docker run -v $(pwd):/zap/wrk/:rw --network="host" zaproxy/zap-stable zap-baseline.py -t https://localhost:8000 -r scan-report.html
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
>>>>>>> a9e859d473d4d9799bf65137c4c23deacca7f113
