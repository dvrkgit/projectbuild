pipeline {

    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }

    environment {
        TOMCAT_URL = "http://tomcat:8080/manager/text"
        APP_NAME   = "hello"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/dvrkgit/projectbuild.git'
            }
        }

        stage('Build WAR using Maven') {
            steps {
                sh '''
                mvn clean package
                ls -l target
                '''
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                sh '''
                curl -v -u tomcat:tomcat \
                -T target/*.war \
                "$TOMCAT_URL/deploy?path=/$APP_NAME&update=true"
                '''
            }
        }
    }

    post {
        success {
            echo "CI/CD Pipeline executed successfully"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
