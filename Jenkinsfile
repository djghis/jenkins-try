CODE_CHANGES = getGitChanges() // can be define with groovy. 
pipeline {
  
    agent any

    stages {
        
        stage('Build') {
            when {
                expression {
                    BRANCH_NAME == 'dev' && CODE_CHANGES == true
                }
            }
            steps {
                echo 'Building..'
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
