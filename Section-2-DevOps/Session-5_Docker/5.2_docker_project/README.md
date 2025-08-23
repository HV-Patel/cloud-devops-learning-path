# 🐳 Docker Project - Address Book Application

<div align="center">

![Docker](https://img.shields.io/badge/Docker-Simple-blue?style=for-the-badge&logo=docker&logoColor=white)
![Tomcat](https://img.shields.io/badge/Tomcat-9.0-orange?style=for-the-badge&logo=apache&logoColor=white)
![Java](https://img.shields.io/badge/Java-17-red?style=for-the-badge&logo=java&logoColor=white)

**🎯 Simple Docker Setup | 🚀 Just Dockerfile | 📦 Easy to Understand**

</div>

---

## 📚 **Docker Images - Simple Theory**

### **What is a Docker Image?**
A Docker image is like a **blueprint** or **template** that contains everything needed to run an application:
- Application code
- Runtime environment  
- System libraries
- Dependencies
- Configuration files

### **How Docker Images Work:**

```mermaid
graph LR
    A[Dockerfile] --> B[Docker Image]
    B --> C[Docker Container]
    
    A1[Recipe/Instructions] --> A
    B1[Template/Blueprint] --> B  
    C1[Running Application] --> C
```

**Think of it like:**
- **Dockerfile** = Recipe (instructions)
- **Docker Image** = Cake mix (ready template)
- **Docker Container** = Baked cake (running application)

---

## 📖 **Docker Keywords Explained**

| Keyword | What it Does | Simple Example |
|---------|-------------|----------------|
| **FROM** | Choose base image | `FROM tomcat:9.0` = Start with Tomcat server |
| **COPY** | Copy files into image | `COPY app.war /webapps/` = Put your app in server |
| **RUN** | Execute commands during build | `RUN apt-get update` = Install software |
| **EXPOSE** | Tell which port to use | `EXPOSE 8080` = App runs on port 8080 |
| **CMD** | Default command when container starts | `CMD ["java", "-jar", "app.jar"]` = Start the app |
| **WORKDIR** | Set working directory | `WORKDIR /app` = Go to /app folder |
| **ENV** | Set environment variables | `ENV JAVA_HOME=/usr/lib/jvm/java` = Set Java path |
| **ADD** | Copy files (with extra features) | `ADD file.tar.gz /app/` = Copy and extract |
| **ENTRYPOINT** | Main command (cannot be overridden) | `ENTRYPOINT ["java"]` = Always run Java |
| **VOLUME** | Create mount point for data | `VOLUME /data` = Persistent storage |

### **Most Common Keywords (80% of Dockerfiles):**
1. **FROM** - Base image
2. **COPY** - Copy your files  
3. **EXPOSE** - Port number
4. **CMD** - Start command

---

## 🌐 **Bonus: Apache HTTPD Example**

### **Simple Web Server with Docker:**

```dockerfile
# Dockerfile.httpd - Simple Apache HTTP Server
FROM httpd:2.4

# Copy HTML files to Apache document root
COPY index.html /usr/local/apache2/htdocs/

# Expose port 80
EXPOSE 80
```

### **Quick HTTPD Setup:**
```bash
# Build Apache image
docker build -f Dockerfile.httpd -t my-httpd .

# Run Apache container
docker run -d -p 8080:80 --name my-apache my-httpd

# Access at: http://localhost:8080
```

### **Or Use Script:**
```bash
chmod +x httpd-build.sh
./httpd-build.sh
```

### **HTTPD vs Tomcat:**
| Feature | HTTPD | Tomcat |
|---------|-------|--------|
| **Use Case** | Static websites | Java web apps |
| **Size** | Smaller | Larger |
| **Speed** | Faster for static | Better for Java |
| **Complexity** | Simple | More features |

---

## 🐳 Docker Containerization Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        🐳 DOCKER CONTAINERIZATION FLOW                     │
└─────────────────────────────────────────────────────────────────────────────┘

📁 Source Code        🔨 Maven Build        📦 Docker Build        🚀 Container Run
     │                      │                     │                      │
     │ Java Application     │                     │                      │
     │ pom.xml             │                     │                      │
     └────────────────────► │                     │                      │
                             │                     │                      │
                             │ mvn clean package   │                      │
                             │                     │                      │
                             │ ✅ addressbook.war   │                      │
                             └───────────────────► │                      │
                                                   │                      │
                                                   │ docker build         │
                                                   │ FROM tomcat:9.0      │
                                                   │ COPY *.war           │
                                                   │                      │
                                                   │ ✅ Docker Image      │
                                                   └────────────────────► │
                                                                          │
                                                                          │ docker run
                                                                          │ -p 9090:8080
                                                                          │
                                                                          │ ✅ Live App
                                                                          │ localhost:9090

┌─────────────────────────────────────────────────────────────────────────────┐
│  🎯 Result: Portable Container | 📦 Consistent Environment | 🚀 Easy Deploy │
└─────────────────────────────────────────────────────────────────────────────┘
```

*Simple Docker workflow: Source → Build → Containerize → Run*

---

## 🚀 Simple Steps

### **Quick Setup**
```bash
# 1. Clone repository
git clone https://github.com/manikcloud/cloud-devops-learning-path.git

# 2. Navigate to project
cd cloud-devops-learning-path/Section-2-DevOps/Session-5_Docker/5.2_docker_project

# 3. Build Java app
mvn clean package

# 4. Build Docker image
docker build -t addressbook-app .

# 5. Run container
docker run -d -p 9090:8080 --name addressbook addressbook-app

# 6. Access application
# Open: http://localhost:9090/addressbook/
```

### **Or Use Script**
```bash
# After cloning and navigating to project directory:
chmod +x simple-build.sh
./simple-build.sh
```

### **Stop/Start**
```bash
docker stop addressbook    # Stop
docker start addressbook   # Start
docker rm addressbook      # Remove
```

---

## 🐳 Simple Dockerfile

```dockerfile
# Use official Tomcat image as base
FROM tomcat:9.0-jdk17

# Remove default webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the WAR file to Tomcat webapps directory
COPY target/addressbook.war /usr/local/tomcat/webapps/addressbook.war

# Expose port 8080
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
```

**That's it!** Simple and effective.

---

## 🛠️ Essential Commands

### **Build and Run**
```bash
mvn clean package
docker build -t addressbook-app .
docker run -d -p 9090:8080 --name addressbook addressbook-app
```

### **Check Status**
```bash
docker ps              # Running containers
docker logs addressbook # View logs
```

### **Development Cycle**
```bash
# Make changes, then:
mvn clean package
docker build -t addressbook-app .
docker stop addressbook && docker rm addressbook
docker run -d -p 9090:8080 --name addressbook addressbook-app
```

---

## 🔍 Troubleshooting

**Container won't start:**
```bash
docker logs addressbook
```

**Application not accessible:**
```bash
docker ps | grep addressbook
curl http://localhost:9090/addressbook/
```

**Build fails:**
```bash
mvn clean package
ls target/addressbook.war
```

---

## 📋 Quick Reference

### **Project Files**
```
5.2_docker_project/
├── src/                     # Java source code
├── pom.xml                  # Maven configuration
├── Dockerfile               # Tomcat container definition
├── Dockerfile.httpd         # Apache HTTPD container definition
├── index.html               # Simple HTML for HTTPD example
├── simple-build.sh          # Tomcat automation script
├── httpd-build.sh           # HTTPD automation script
└── README.md               # This guide
```

### **URLs**
- **Application:** http://localhost:9090/addressbook/
- **Repository:** https://github.com/manikcloud/cloud-devops-learning-path

---

*Simple, clean, and effective Docker containerization!* 🎉
