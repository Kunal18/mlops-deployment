# MLOps Deployment

This repository contains the setup and configuration files for deploying an MLOps pipeline using FastAPI and Docker on AWS EC2.
Each instance is running the ELK stack as well.

## Project Structure

```
mlops-deployment/
├── app/
│ ├── main.py
│ └── ...
├── fastapi-logs/
│ ├── ...
├── filebeat/
│ ├── ...
├── .gitignore
├── Dockerfile
├── README.md
├── docker-compose.yaml
├── heroku.yml
└── requirements.txt
```

## Prerequisites

- AWS Account
- Docker
- Python 3.8+

## Setup

1. **Clone the repository:**

    ```bash
    git clone https://github.com/shivanshvermaa/mlops-deployment.git
    cd mlops-deployment
    ```

2. **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

## Running Locally

1. **Build and run Docker containers:**

    ```bash
    docker-compose up --build
    ```

2. **Access the FastAPI application:**

    Open your browser and navigate to `http://localhost:8000`

## Deployment to AWS EC2

### Step 1: Launch an EC2 Instance

1. **Log in to AWS Management Console.**
2. **Navigate to EC2 Dashboard.**
3. **Click on "Launch Instance".**
4. **Choose an Amazon Machine Image (AMI), preferably Ubuntu.**
5. **Select an instance type (e.g., t2.micro).**
6. **Configure instance details, add storage, and add tags if needed.**
7. **Configure the security group to allow HTTP (port 80), HTTPS (port 443), and SSH (port 22) access.**
8. **Review and launch the instance.**
   
## Configuration

The application uses environment variables for configuration. You can set these variables in a `.env` file or directly in your environment. Example `.env` file:

```
AWS_S3_OBJECT_NAME=<OBJECT_NAME>
AWS_S3_BUCKET_NAME=<BUCKET_NAME>
AWS_SECRET_KEY=<SECRET_KEY>
AWS_ACCESS_KEY_ID=<ACCESS_KEY>
```

### Step 2: Connect to the EC2 Instance

1. **Open your terminal.**
2. **Connect to your instance using SSH:**

    ```bash
    ssh -i /path/to/your-key-pair.pem ubuntu@your-ec2-public-dns
    ```

### Step 3: Install Docker and Docker Compose on EC2 Instance

1. **Update the package index:**

    ```bash
    sudo apt-get update
    ```

2. **Install Docker:**

    ```bash
    sudo apt-get install -y docker.io
    ```

3. **Start Docker and enable it to start on boot:**

    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

4. **Install Docker Compose:**

    ```bash
    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```

### Step 4: Clone Repository and Run Application

1. **Clone the repository:**

    ```bash
    git clone https://github.com/shivanshvermaa/mlops-deployment.git
    cd mlops-deployment
    ```

2. **Build and run Docker containers:**

    ```bash
    sudo docker-compose up --build -d
    ```

3. **Access the FastAPI application:**

    Open your browser and navigate to `http://your-ec2-public-dns:80` to see the health status
   
    Open your browser and navigate to `http://your-ec2-public-dns/docs` to see the documentation

