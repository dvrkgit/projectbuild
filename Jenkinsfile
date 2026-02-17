pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK11'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/dvrkgit/projectbuild.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                sh '''
                curl -f -u tomcat:tomcat \
                -X POST \
                --data-binary @target/hello-world.war \
                "http://tomcat:8080/manager/text/deploy?path=/hello&update=true"
                '''
            }
        }
    }
}
