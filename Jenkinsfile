// you can find variables on host (this case localhost:8080)/en-vars.html
CODE_CHANGES = getGitChanges() // can be define with groovy. 
pipeline {
  
    agent any
    environment {  //You can create your own variables here.
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('reference/ID from credentials') // this methods bind the credentials in jenkins to your script if you download a plugin called
        //credentials bindings
    }

    tools {
        //works only with GRADLE, MAVEN and JDK (Java Developer Kit)
        maven 'Maven'  //has to be pre installed in jenkins between quotes you provide the Name given in Jenkins
    }

    stages {
        
        stage('Build') {
            when {
                expression {
                    BRANCH_NAME == 'dev' && CODE_CHANGES == true
                }
            }
            steps {
                echo 'Building..'
                echo "Building version ${NEW_VERSION}"  //double quotes"" needed for string interpolation
            }
        }
        stage('Test') {
            when {
                expression {
                    BRANCH_NAME == 'dev'
                }
            }
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "${SERVER_CREDENTIALS}"
            }
        }
    }

    post {
        //something that happen after the othr command ran.
        always {
            
        }
        success {
            
        }
        failure {
            
        }
        //others are available see docs https://www.jenkins.io/doc/book/pipeline/syntax/
       
    }
}
