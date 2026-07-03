pipeline {
    agent any
    tools {
        maven 'M3915'
        // Removed the broken jdk 'JDK17' line
    }
    environment {
        // This forces Maven to use the correct Java 17 home path explicitly
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-arm64' 
        PATH      = "${env.JAVA_HOME}/bin:${env.PATH}"
    }
    
    stages {
        stage('Environment Check') {
            steps {
                sh 'sleep 120'
                sh 'mvn -version'
                sh 'java -version' // This will verify if Java 17 is active
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('Test') {
            steps {
                
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                // Fixed wildcard expansion issue and added background execution '&'
                sh 'java -jar target/hello-demo-0.0.1-SNAPSHOT.jar &' 
            }
        }
    }
}

