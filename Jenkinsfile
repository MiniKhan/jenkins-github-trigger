pipeline {
    agent any 
    tools {
        maven "Maven"
    }

    stages {
        stage("Checkout") {
            steps {
                // Replace with your actual repo URL and branch
                git url: 'https://github.com/MiniKhan/jenkins-github-trigger.git', branch: 'main'
            }
        }

        stage("Test") {
            steps {
                sh "mvn test"
            }
        }

        stage("Build") {
            steps {
                sh "mvn package"
            }
        }

        stage("Deploy on Test") {
            steps {
                echo "======== Deployed to Testing Server ========"
                deploy adapters: [tomcat9(
                    credentialsId: 'Tomcat9Details', 
                    path: '', 
                    url: 'http://192.168.56.4:8081/')], 
                    contextPath: '/app', 
                    war: '**/*.war'
            }
        }

        stage("Deploy on Prod") {
            steps {
                echo "======== Successfully deployed to Production Server ========"
            }
        }
    }

    post {
        always {
            echo "======== always ========"
        }
        success {
            echo "======== Pipeline executed successfully ========"
        }
        failure {
            echo "======== Pipeline execution failed ========"
        }
    }
}
