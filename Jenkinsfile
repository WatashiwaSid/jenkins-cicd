pipeline {
    agent any
    
     environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/WatashiwaSid/jenkins-cicd'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
        
        stage('Sonarcube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Petclinic \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=Petclinic '''
                }
            }
        }
        
        stage('Build and Test') {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('Deploy') {
            steps {
                sh "sudo cp target/*.war /opt/apache-tomcat-9.0.65/webapps"
            }
        }
        
    }
}
