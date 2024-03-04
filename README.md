# Netflix_c
This project is a simple clone of the Netflix.com page. The motivation behind this project is to have hands on experience with DevSecOps tools and processes and also to practice different react properties and features.

# Deploy Netflix Clone on Cloud

### **Phase 1: Initial Setup and Deployment**

**Step 1: Launch EC2 (Ubuntu 22.04):**

- Provision an EC2 instance on AWS with Ubuntu 22.04.
- Connect to the instance using SSH.

**Step 2: Clone the Code:**

- Update all the packages and then clone the code.
- Clone your application's code repository onto the EC2 instance:
    
    ```bash
    git clone https://github.com/Maharshi-Mimo/Netflix_c.git
    ```

**Step 3: Get the API Key:**

- Open a web browser and navigate to [TMDB](https://github.com/Maharshi-Mimo/Netflix_c.git) (The Movie Database) website.
- Click on "Login" and create an account.
- Once logged in, go to your profile and select "Settings."
- Click on "API" from the left-side panel.
- Create a new API key by clicking "Create" and accepting the terms and conditions.
- Provide the required basic details and click "Submit."
- You will receive your TMDB API key.

**Step 4: Install Docker and Run the App Using a Container:**

- Set up Docker on the EC2 instance:
    
    ```bash
    
    sudo apt-get update
    sudo apt-get install docker.io -y
    sudo usermod -aG docker $USER  # Replace with your system's username, e.g., 'ubuntu'
    newgrp docker
    sudo chmod 777 /var/run/docker.sock
    ```

- Build and run the application using Docker container

    ```bash
    docker build --build-arg TMDB_V3_API_KEY=<your-api-key> -t netflix .
    docker run -d --name netflix -p 8081:80 netflix:latest
    
    #to delete
    #docker stop <containerid>
    #docker rmi -f netflix
    ```
### **Phase 2: Security**

1. **Install SonarQube and Trivy:**

- Install SonarQube and Trivy on the EC2 instance to scan for vulnerabilities.
        
- sonarqube
        ```bash
        docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
        ```        
        To access sonarqube: <EC2_pulic_ip>:9000 (by default username & password is admin)

- To install Trivy. 
 ```bash
        sudo apt-get install wget apt-transport-https gnupg lsb-release
        wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
        echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
        sudo apt-get update
        sudo a
 ```
2. **Integrate SonarQube and Configure:**
    - Integrate SonarQube with your CI/CD pipeline.
    - Configure SonarQube to analyze code for quality and security issues.