
### 1. **Freestyle Project**
Freestyle projects are the most basic type of Jenkins job. They are flexible and can be configured to run various types of build steps.

**Example:**
A simple project to build a Java application using Maven.

**Steps:**
1. **Source Code Management (SCM):**
   - Checkout code from a Git repository.
2. **Build Step:**
   - Execute shell command to run `mvn clean install`.
3. **Post-Build Actions:**
   - Archive the artifacts (e.g., JAR/WAR files).

```groovy
// Shell Command
mvn clean install
```

### 2. **Pipeline (Declarative)**
Declarative Pipelines provide a more structured and simpler way to define a CI/CD pipeline as code.

**Example:**
A CI/CD pipeline for a Node.js application.

**Jenkinsfile:**
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'npm run deploy'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
```

### 3. **Pipeline (Scripted)**
Scripted Pipelines offer more flexibility and are written in Groovy. They are useful for complex pipelines with conditional logic.

**Example:**
A pipeline for a Python application that includes conditional deployment.

**Jenkinsfile:**
```groovy
node {
    stage('Checkout') {
        checkout scm
    }
    stage('Build') {
        sh 'pip install -r requirements.txt'
    }
    stage('Test') {
        try {
            sh 'pytest'
        } catch (Exception e) {
            currentBuild.result = 'UNSTABLE'
        }
    }
    stage('Deploy') {
        if (currentBuild.result == 'SUCCESS') {
            sh 'deploy.sh'
        }
    }
    stage('Cleanup') {
        sh 'rm -rf workspace'
    }
}
```

### 4. **Multibranch Pipeline**
Multibranch Pipelines automatically create Jenkins pipelines for branches in SCM repositories. This is useful for projects with multiple branches.

**Example:**
A Java application where each branch gets its own pipeline.

**Jenkinsfile:**
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: '*/main', url: 'https://github.com/example/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
```

### 5. **Pipeline with Docker**
Using Docker within a Jenkins pipeline to ensure a consistent build environment.

**Example:**
A pipeline that builds and tests a Node.js application inside a Docker container.

**Jenkinsfile:**
```groovy
pipeline {
    agent {
        docker { image 'node:14' }
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
    }
}
```

### 6. **Blue Ocean Pipeline**
Blue Ocean provides a modern user interface for Jenkins Pipelines, making it easier to visualize complex pipelines.

**Example:**
A visualized pipeline for a Java Spring Boot application.

**Jenkinsfile:**
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/spring-boot-app.git'
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean install'
            }
        }
        stage('Test') {
            steps {
                sh './mvnw test'
            }
        }
        stage('Deploy') {
            steps {
                sh './mvnw deploy'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
```

