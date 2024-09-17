Setting up **WSO2 API Manager** can be done in various environments: Linux, Windows, Docker, and Kubernetes. Here's a step-by-step guide for each method:

---

## 1. **Setting up WSO2 API Manager on Linux**

### Prerequisites
- **Java**: Install Java Development Kit (JDK 11 or later).
  ```bash
  sudo apt update
  sudo apt install openjdk-11-jdk
  java -version
  ```

- **Database**: WSO2 API Manager uses a database to store data. Install **MySQL**, **PostgreSQL**, or any other supported DB.

### Steps
1. **Download WSO2 API Manager**:
   - Go to [WSO2 API Manager](https://wso2.com/api-management/) and download the latest version.
   - Alternatively, you can download it from the terminal:
     ```bash
     wget https://product-dist.wso2.com/products/api-manager/<version>/wso2am-<version>.zip
     ```

2. **Extract the ZIP File**:
   ```bash
   unzip wso2am-<version>.zip
   cd wso2am-<version>/bin
   ```

3. **Start WSO2 API Manager**:
   ```bash
   ./wso2server.sh
   ```

4. **Access the API Manager**:
   - Open your browser and navigate to `https://localhost:9443/carbon` for the management console.
   - The default credentials are **admin** / **admin**.

---

## 2. **Setting up WSO2 API Manager on Windows**

### Prerequisites
- **Java**: Install JDK 11 or later on Windows and configure the environment variable:
  - Download from [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) or [OpenJDK](https://openjdk.java.net/).
  - Set `JAVA_HOME` environment variable and add it to the `PATH`.

### Steps
1. **Download WSO2 API Manager**:
   - Go to [WSO2 API Manager](https://wso2.com/api-management/) and download the Windows distribution.

2. **Extract the ZIP File**:
   - Right-click the downloaded ZIP file and select **Extract** to your preferred location.

3. **Run the Server**:
   - Open **Command Prompt** and navigate to the `bin` directory of the extracted folder:
     ```cmd
     cd wso2am-<version>\bin
     wso2server.bat
     ```

4. **Access the API Manager**:
   - Open a browser and go to `https://localhost:9443/carbon`.
   - Default credentials: **admin** / **admin**.

---

## 3. **Setting up WSO2 API Manager using Docker**

### Prerequisites
- Install **Docker** and **Docker Compose**.
  - Instructions for Docker: [Docker Install](https://docs.docker.com/get-docker/).
  - Verify Docker installation:
    ```bash
    docker --version
    ```

### Steps
1. **Download WSO2 API Manager Docker Image**:
   - WSO2 provides official Docker images. Pull the latest API Manager image from Docker Hub:
     ```bash
     docker pull wso2/wso2am:<version>
     ```

2. **Run the API Manager Container**:
   - Start the container with the following command:
     ```bash
     docker run -d -p 9443:9443 --name wso2am wso2/wso2am:<version>
     ```

3. **Access the API Manager**:
   - Open `https://localhost:9443/carbon` in your browser.
   - Default credentials: **admin** / **admin**.

### Using Docker Compose

1. **Create `docker-compose.yml`**:
   ```yaml
   version: '3'
   services:
     wso2am:
       image: wso2/wso2am:<version>
       ports:
         - "9443:9443"
   ```

2. **Run Docker Compose**:
   ```bash
   docker-compose up -d
   ```

3. **Access the API Manager**:
   - Same as above (`https://localhost:9443/carbon`).

---

## 4. **Setting up WSO2 API Manager on Kubernetes**

### Prerequisites
- Install **Kubernetes** (e.g., **Minikube**, **MicroK8s**, or any managed Kubernetes service like **GKE**, **AKS**, or **EKS**).
- Install **kubectl**.
- Install **Helm**.

### Steps

1. **Add the WSO2 Helm Repository**:
   - WSO2 provides Helm charts for deploying API Manager on Kubernetes.
     ```bash
     helm repo add wso2 https://helm.wso2.com
     helm repo update
     ```

2. **Install WSO2 API Manager using Helm**:
   - Create a Kubernetes namespace:
     ```bash
     kubectl create namespace wso2
     ```
   - Install the API Manager using the Helm chart:
     ```bash
     helm install wso2am wso2/am --namespace wso2
     ```

3. **Check Deployment Status**:
   - Verify that the pods are running:
     ```bash
     kubectl get pods -n wso2
     ```

4. **Access the API Manager**:
   - For **Minikube** or **MicroK8s**, you can get the external IP using:
     ```bash
     minikube service wso2am --url
     ```
   - For other Kubernetes clusters, check the external IP for the service:
     ```bash
     kubectl get svc -n wso2
     ```
   - Access the management console using the external IP at `https://<external-ip>:9443/carbon`.
   - Default credentials: **admin** / **admin**.

### Customizing Helm Installation
- You can customize the Helm installation by creating a `values.yaml` file and modifying settings such as external databases, scaling, or storage.

---

### Conclusion

WSO2 API Manager can be deployed across various platforms, each with its own setup process. For production environments, using Kubernetes or Docker is recommended as they offer better scalability and management, while Linux and Windows installations are suitable for development or testing purposes.