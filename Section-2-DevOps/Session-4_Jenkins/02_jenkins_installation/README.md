# ⚙️ Module 02: Jenkins Installation & Configuration

<div align="center">

![Jenkins](https://img.shields.io/badge/Jenkins-Installation-blue?style=for-the-badge&logo=jenkins&logoColor=white)
![Security](https://img.shields.io/badge/Security-Configuration-red?style=for-the-badge&logo=security&logoColor=white)

**🎯 Install Jenkins | 🔒 Configure Security | 🚀 Initial Setup**

</div>

---

## 📋 Module Overview

This module covers the complete installation and initial configuration of Jenkins on your AWS infrastructure. You'll learn both manual installation methods and automated approaches, plus essential security configurations.

### 🎯 **Learning Objectives**
- ✅ Install Jenkins on Amazon Linux 2
- ✅ Configure Jenkins initial setup and plugins
- ✅ Implement security best practices
- ✅ Set up user authentication and authorization
- ✅ Configure system settings and global tools

---

## 📚 Theory: Jenkins Installation & Security

### **Jenkins Installation Methods**

#### **1. Package Manager Installation (Recommended)**
- 🚀 **Fastest Setup** - Using yum/apt package managers
- 🔄 **Easy Updates** - Automatic dependency management
- 🔒 **Stable Releases** - LTS (Long Term Support) versions
- 📦 **System Integration** - Proper service management

#### **2. WAR File Deployment**
- 🎯 **Portable** - Run on any Java-enabled system
- 🔧 **Customizable** - Full control over configuration
- 📊 **Development** - Good for testing and development
- ⚡ **Quick Start** - Minimal setup required

#### **3. Docker Container**
- 🐳 **Containerized** - Isolated environment
- 🔄 **Scalable** - Easy horizontal scaling
- 📦 **Consistent** - Same environment everywhere
- 🚀 **Cloud Native** - Perfect for Kubernetes

### **Jenkins Security Architecture**

<div align="center">

![Jenkins Architecture](../images/jenkins-architecture.svg)

</div>

#### **Authentication Methods:**
- 🔐 **Jenkins Database** - Built-in user management
- 🏢 **LDAP/Active Directory** - Enterprise integration
- 🔑 **OAuth/SAML** - Single Sign-On (SSO)
- 🌐 **Matrix-based Security** - Fine-grained permissions

#### **Authorization Strategies:**
- 👤 **Anyone can do anything** - Development only
- 👥 **Legacy mode** - Backward compatibility
- 🔒 **Matrix-based security** - User/group permissions
- 📊 **Project-based Matrix** - Per-project permissions

---

## 🛤️ Module Structure

<table>
<tr>
<th width="10%">Project</th>
<th width="30%">Name</th>
<th width="40%">Description</th>
<th width="20%">Skills</th>
</tr>

<tr>
<td><strong>2.1</strong></td>
<td><strong><a href="./2.1_install_jenkins">Install Jenkins</a></strong></td>
<td>Install Jenkins on Amazon Linux 2 with proper configuration and plugin setup</td>
<td>Jenkins Installation, System Configuration, Plugin Management</td>
</tr>

<tr>
<td><strong>2.2</strong></td>
<td><strong><a href="./2.2_enabling_security">Enable Security</a></strong></td>
<td>Configure Jenkins security, user authentication, and authorization settings</td>
<td>Security Configuration, User Management, Access Control</td>
</tr>

</table>

---

## 🔧 **Jenkins Installation Process**

### **Step-by-Step Installation:**

#### **1. System Preparation**
```bash
# Update system packages
sudo yum update -y
```

#### **2. Jenkins Repository Setup**
```bash
# Add Jenkins repository
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

# Import Jenkins GPG key
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# Upgrade system packages
sudo yum upgrade
```

#### **3. Java Installation**
```bash
# Install Java 17 Amazon Corretto
sudo yum install java-17-amazon-corretto -y
```

#### **4. Jenkins Installation**
```bash
# Install Jenkins
sudo yum install jenkins -y

# Start Jenkins service
sudo systemctl start jenkins

# Check Jenkins status
sudo systemctl status jenkins

# Enable Jenkins to start on boot
sudo systemctl enable jenkins
```

#### **5. Verify Installation**
```bash
# Verify Java installation
java -version

# Check Jenkins service status
sudo systemctl status jenkins

# Verify Jenkins is listening on port 8080
sudo netstat -tlnp | grep 8080

# Get initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

#### **6. Firewall Configuration (Optional)**
```bash
# Open port 8080 for Jenkins (if firewall is enabled)
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload

# Verify port is open
sudo firewall-cmd --list-all
```

### **Initial Jenkins Setup**

#### **1. Unlock Jenkins**
```bash
# Get initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

#### **2. Plugin Installation**
- **Suggested Plugins** (Recommended for beginners)
- **Custom Plugin Selection** (For experienced users)

#### **Essential Plugins:**
- 🔧 **Build Tools**: Maven, Gradle, Ant
- 📊 **SCM**: Git, GitHub, Bitbucket
- 🧪 **Testing**: JUnit, TestNG, Coverage
- 📧 **Notifications**: Email, Slack, Teams
- ☁️ **Cloud**: AWS, Docker, Kubernetes

---

## 🔒 **Security Configuration**

### **Security Best Practices**

#### **1. User Management**
- 👤 **Admin User**: Full system access
- 👥 **Developer Users**: Project-specific access
- 🔍 **Read-only Users**: View-only access
- 🤖 **Service Accounts**: API and automation access

#### **2. Access Control**
- 🔒 **Principle of Least Privilege**
- 📊 **Role-based Access Control (RBAC)**
- 🌐 **Network-level Security**
- 🔑 **API Token Management**

#### **3. System Security**
- 🔐 **CSRF Protection**: Enabled by default
- 🛡️ **Agent-to-Master Security**: Strict mode
- 📊 **Script Security**: Sandbox execution
- 🔒 **Markup Formatter**: Safe HTML only

---

## 📊 **Jenkins Configuration Files**

### **Important Directories:**
```
/var/lib/jenkins/          # Jenkins home directory
├── config.xml             # Main configuration
├── jobs/                  # Job configurations
├── plugins/               # Installed plugins
├── users/                 # User configurations
├── secrets/               # Security keys
├── workspace/             # Build workspaces
└── logs/                  # System logs
```

### **Configuration Management:**
- 📝 **config.xml**: Main Jenkins configuration
- 🔧 **Global Tool Configuration**: JDK, Maven, Git paths
- 🔌 **Plugin Management**: Install, update, disable plugins
- 👥 **User Management**: Create, modify, delete users

---

## 🚀 Getting Started

### **Prerequisites**
- ✅ AWS EC2 instance from Module 01
- ✅ SSH access to the instance
- ✅ Basic Linux command knowledge
- ✅ Understanding of system administration

### **Installation Verification**
```bash
# Check Jenkins service
sudo systemctl status jenkins

# Check Java version
java -version

# Check Jenkins logs
sudo journalctl -u jenkins -f

# Test web access
curl -I http://localhost:8080
```

---

## 📊 Expected Outcomes

After completing this module, you will have:

### **Jenkins Installation**
- ✅ **Jenkins Running** on port 8080
- ✅ **Essential Plugins** installed and configured
- ✅ **Admin User** created with secure password
- ✅ **System Tools** configured (JDK, Maven, Git)

### **Security Configuration**
- ✅ **Authentication** enabled with user database
- ✅ **Authorization** configured with matrix-based security
- ✅ **CSRF Protection** enabled
- ✅ **Security Realm** properly configured

### **Skills Gained**
- ✅ **Jenkins Installation** on Linux systems
- ✅ **Security Configuration** best practices
- ✅ **Plugin Management** and system administration
- ✅ **Troubleshooting** common installation issues

---

## 🔍 Verification Checklist

### **Installation Verification**
- [ ] Jenkins web interface accessible on port 8080
- [ ] Admin user can log in successfully
- [ ] Essential plugins are installed and active
- [ ] System tools (Java, Maven, Git) are configured
- [ ] Jenkins service starts automatically on boot

### **Security Verification**
- [ ] Anonymous access is disabled
- [ ] User authentication is required
- [ ] Admin user has full permissions
- [ ] CSRF protection is enabled
- [ ] Security warnings are resolved

---

## 🚨 Troubleshooting Guide

### **Common Installation Issues**

#### **Jenkins Won't Start**
```bash
# Check Java installation
java -version

# Check Jenkins logs
sudo journalctl -xeu jenkins.service

# Check Jenkins application logs
sudo tail -f /var/log/jenkins/jenkins.log

# Set JAVA_HOME if needed
echo 'JAVA_HOME="/usr/lib/jvm/java-17-amazon-corretto.x86_64"' | sudo tee -a /etc/sysconfig/jenkins

# Restart Jenkins
sudo systemctl daemon-reload
sudo systemctl restart jenkins
```

#### **Web Interface Not Accessible**
```bash
# Check if Jenkins is running
sudo systemctl status jenkins

# Check if port 8080 is in use
sudo netstat -tlnp | grep 8080

# Check security group (AWS EC2)
# Ensure port 8080 is open in your EC2 security group

# Test local connectivity
curl -I http://localhost:8080
```

#### **Permission Issues**
```bash
# Fix Jenkins directory permissions
sudo chown -R jenkins:jenkins /var/lib/jenkins/
sudo chown -R jenkins:jenkins /var/cache/jenkins/
sudo chown -R jenkins:jenkins /var/log/jenkins/

# Restart Jenkins
sudo systemctl restart jenkins
```

#### **Web Interface Not Accessible**
```bash
# Check firewall settings
sudo firewall-cmd --list-all

# Check security group (AWS)
aws ec2 describe-security-groups --group-ids sg-xxxxxxxxx

# Test local connectivity
curl -I http://localhost:8080
```

#### **Plugin Installation Failures**
```bash
# Check internet connectivity
curl -I https://updates.jenkins.io

# Clear plugin cache
sudo rm -rf /var/lib/jenkins/plugins/*.jpi.tmp

# Restart Jenkins
sudo systemctl restart jenkins
```

### **Security Issues**

#### **Forgot Admin Password**
```bash
# Disable security temporarily
sudo vi /var/lib/jenkins/config.xml
# Set <useSecurity>false</useSecurity>

# Restart Jenkins
sudo systemctl restart jenkins

# Re-enable security through web interface
```

#### **User Cannot Access Jenkins**
- Check user permissions in security matrix
- Verify user is in correct groups
- Check authentication realm configuration
- Review security logs

---

## 📚 Additional Resources

### **Documentation**
- 📖 [Jenkins Installation Guide](https://www.jenkins.io/doc/book/installing/)
- 📖 [Jenkins Security](https://www.jenkins.io/doc/book/security/)
- 📖 [Plugin Management](https://www.jenkins.io/doc/book/managing/plugins/)

### **Security Resources**
- 🔒 [Jenkins Security Best Practices](https://www.jenkins.io/doc/book/security/best-practices/)
- 🔒 [Securing Jenkins](https://wiki.jenkins.io/display/JENKINS/Securing+Jenkins)
- 🔒 [Authentication and Authorization](https://www.jenkins.io/doc/book/security/managing-security/)

---

## ➡️ Next Steps

Once Jenkins is installed and secured:

1. **Test Login** - Verify admin access works
2. **Configure Global Tools** - Set up JDK, Maven, Git paths
3. **Create Test User** - Verify security configuration
4. **Proceed to Module 03** - [Basic Jobs](../03_basic_jobs/README.md)

---

<div align="center">

### 🎯 **Jenkins Installation Complete!**
*Your Jenkins server is ready for job creation and pipeline development.*

**Next: [Module 03 - Basic Jobs](../03_basic_jobs/README.md)**

</div>
