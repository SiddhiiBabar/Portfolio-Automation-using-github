# 🚀 Portfolio Deployment Automation

This project demonstrates the **automation and deployment of a portfolio website** using DevOps tools and AWS services.

The website source code was taken from an existing portfolio template and modified/configured for deployment and automation.

## 🛠️ Technologies Used

* Git & GitHub
* Jenkins
* Docker
* Nginx
* GitHub Actions
* AWS EC2
* AWS S3
* HTML, CSS, JavaScript

## 🔄 Project Workflow

```text
Website Source Code
        ↓
      GitHub
        ↓
   Jenkins / GitHub Actions
        ↓
   Docker Build
        ↓
 Docker Container / AWS S3
        ↓
   Deployed Website
```

## 🐳 Docker Deployment

A Docker image is created using the Dockerfile.

### Build Docker Image

```bash
docker build -t portfolio-image .
```

### Run Docker Container

```bash
docker run -d \
--name portfolio-container \
-p 8081:80 \
portfolio-image
```

### Check Running Container

```bash
docker ps
```

The website can be accessed using:

```text
http://<EC2-Public-IP>:8081
```

## 🔧 Jenkins CI/CD

Jenkins is used to automate the Docker deployment process.

### Pipeline Stages

1. Clone the source code
2. Build Docker image
3. Stop the old container
4. Remove the old container
5. Run the new container

Example Jenkins pipeline:

```groovy
pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio-image .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop portfolio-container || true
                    docker rm portfolio-container || true

                    docker run -d \
                    --name portfolio-container \
                    -p 8081:80 \
                    portfolio-image
                '''
            }
        }
    }
}
```

## ☁️ AWS S3 Deployment

The website can also be deployed to an **AWS S3 bucket** using GitHub Actions.

The workflow performs:

* Checkout source code
* Configure AWS credentials
* Upload website files to S3
* Sync updated files automatically

Example command:

```bash
aws s3 sync . s3://<S3-BUCKET> --delete
```

AWS credentials are stored securely using **GitHub Secrets**.

## 🔐 GitHub Secrets

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
S3_BUCKET
```

## 📂 Project Structure

```text
Portfolio-Automation-using-github/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── assets/
├── forms/
├── index.html
├── portfolio-details.html
├── service-details.html
├── starter-page.html
├── Dockerfile
├── jenkinsfile
└── README.md
```

## 🎯 What I Implemented

* Used GitHub for source code management
* Created a Dockerfile for containerization
* Built Docker images
* Deployed the website using Docker
* Configured Jenkins CI/CD pipeline
* Configured GitHub Actions
* Automated AWS S3 deployment
* Used GitHub Secrets for AWS credentials
* Hosted the application on AWS EC2 using Docker

## 📚 Key Learning

This project helped me understand:

* Docker containerization
* Jenkins CI/CD
* GitHub Actions
* AWS S3 deployment
* AWS EC2
* Nginx
* Git and GitHub
* Automated deployment

## 👩‍💻 Author
**Siddhi Babar**

GitHub: [SiddhiiBabar](https://github.com/SiddhiiBabar)
