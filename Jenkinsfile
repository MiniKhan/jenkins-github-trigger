pipeline{
    
    agent any 
    tools {
        maven "Maven 3.9.9"
    }

    stages{
        stage("Test")
        {
            steps{
                sh "mvn test"
                echo "========executing A========"
                sh 'mvn --version'
            }
           
        }
         stage("Build")
        {
            steps{
                sh "mvn package"
                echo "========executing A========"
            }
           
        }
         stage("Deploy on Test")
        {
            steps{
                echo "========executing A========"
                //deploy on testing container
                deploy adapters: [tomcat9(credentialsId: 'Tomcat9Details', path: '', url: 'http://192.168.56.4:8081/')], contextPath: '/app', war: '**/*.war'
            }
           
        }
         stage("Deploy on Prod")
        {
            steps{
                //deploy on production container
                echo "========Successfully deployed to Production Server========"
            }
           
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
