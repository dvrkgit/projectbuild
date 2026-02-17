pipeline {

    agent any

    tools {
        jdk 'JDK11'
        maven 'Maven'
    }

    environment {
        TOMCAT_URL = "http://tomcat:8080/manager/text"
        APP_NAME   = "hello"
    }

    stages {

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
            echo "Pipeline success"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
