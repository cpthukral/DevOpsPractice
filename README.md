# DevOpsPractice

A comprehensive CI/CD practice repository focused on Jenkins automation and DevOps best practices.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
- [Jenkins Configuration](#jenkins-configuration)
- [CI/CD Pipeline](#cicd-pipeline)
- [Usage](#usage)
- [Contributing](#contributing)
- [Resources](#resources)

---

## Overview

This repository is a practical learning environment for implementing continuous integration and continuous deployment (CI/CD) pipelines using **Jenkins**. It covers essential DevOps concepts, automated build processes, testing strategies, and deployment automation.

**Key Focus Areas:**
- Jenkins pipeline configuration
- Build automation
- Automated testing
- Artifact management
- Deployment strategies
- Infrastructure as Code (IaC) practices

---

## Prerequisites

Before getting started, ensure you have the following installed:

- **Jenkins** (version 2.x or higher)
- **Git** (for version control)
- **Docker** (optional, for containerized deployments)
- **Maven/Gradle** (for Java projects) or your project's build tool
- **Java** (JDK 8 or higher)
- Basic understanding of CI/CD concepts

---

## Project Structure

```
DevOpsPractice/
├── README.md
├── Jenkinsfile                 # Pipeline configuration
├── src/                        # Source code
│   ├── main/
│   └── test/
├── scripts/                    # Automation scripts
│   ├── build.sh
│   ├── test.sh
│   └── deploy.sh
├── config/                     # Configuration files
│   ├── jenkins/
│   └── pipeline/
├── docker/                     # Docker configurations
│   └── Dockerfile
└── docs/                       # Documentation
    └── SETUP.md
```

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/VeerVSR/DevOpsPractice.git
cd DevOpsPractice
```

### 2. Install Dependencies

```bash
# For Maven projects
mvn clean install

# For Gradle projects
gradle build
```

### 3. Configure Jenkins

- Install required Jenkins plugins (Pipeline, Git, Docker, etc.)
- Create a new Pipeline job in Jenkins
- Configure Git repository URL
- Set up webhook for automatic triggers (optional)

### 4. Set Up Environment Variables

Create a `.env` file with necessary configurations:

```env
BUILD_ENV=development
DOCKER_REGISTRY=your-registry
ARTIFACT_PATH=/var/lib/jenkins/artifacts
```

---

## Jenkins Configuration

### Required Plugins

- Pipeline
- Git
- Docker
- Email Extension
- Credentials Binding
- JUnit

### Install Plugins

```bash
# Via Jenkins CLI
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin pipeline docker git email-ext credentials-binding junit
```

### Jenkins Credentials Setup

1. Manage Jenkins → Manage Credentials
2. Add credentials for:
   - Git repository access
   - Docker registry (if applicable)
   - Deployment server SSH keys

---

## CI/CD Pipeline

### Pipeline Stages

1. **Checkout** - Clone source code from Git
2. **Build** - Compile and package the application
3. **Test** - Run unit and integration tests
4. **Analyze** - Code quality analysis (SonarQube, etc.)
5. **Deploy** - Push artifacts to staging/production
6. **Notify** - Send notifications (email, Slack, etc.)

### Basic Jenkinsfile Example

```groovy
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/VeerVSR/DevOpsPractice.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'bash scripts/deploy.sh'
            }
        }
    }
    
    post {
        always {
            junit 'target/surefire-reports/**/*.xml'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
```

---

## Usage

### Running the Pipeline

1. Navigate to Jenkins Dashboard
2. Select your job
3. Click **Build Now** to trigger the pipeline
4. Monitor the build progress in the console output

### Manual Build

```bash
# Build locally
./scripts/build.sh

# Run tests
./scripts/test.sh

# Deploy
./scripts/deploy.sh
```

### Viewing Logs

```bash
# Jenkins logs
tail -f /var/log/jenkins/jenkins.log

# Pipeline execution logs
# Available in Jenkins UI under job console output
```

---

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Create a feature branch (`git checkout -b feature/your-feature`)
2. Commit your changes (`git commit -am 'Add new feature'`)
3. Push to the branch (`git push origin feature/your-feature`)
4. Submit a pull request

---

## Resources

### Official Documentation

- [Jenkins Official Documentation](https://www.jenkins.io/doc/)
- [Jenkins Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/)
- [Jenkins Best Practices](https://www.jenkins.io/doc/book/security/)

### Learning Resources

- [Jenkins Tutorial for Beginners](https://www.jenkins.io/doc/tutorials/)
- [CI/CD Best Practices](https://www.jenkins.io/doc/book/pipeline/)
- [Docker & Jenkins Integration](https://www.jenkins.io/doc/book/installing/)

### Useful Tools

- [Jenkins CLI](https://www.jenkins.io/doc/book/managing/cli/)
- [Groovy Documentation](https://groovy-lang.org/)
- [Git Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)

---

## License

This project is open source and available under the MIT License.

---

## Contact

For questions or support, please reach out to the repository maintainer or open an issue.

**Repository:** [DevOpsPractice](https://github.com/VeerVSR/DevOpsPractice)

---

*Last Updated: 2026-04-28*
