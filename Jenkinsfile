//THIS Jenkinsfile will probably not work as there are lots of options there to show what is available as this is my 1st one.

// you can find variables on host (this case localhost:8080)/en-vars.html

//def gv here to make it globally available and assign the script to the variable in the "init" stage
def gv
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

    parameters {
        string(name: 'VERSION', defaultValue: '', description: 'something for me to remember what was done bacuse I will forgot how and why!')
        choice (name: 'VERSION', choices: ['1.1,1', '1.1.2', '1,3,0'],  description: 'something for me to remember what was done bacuse I will forgot how and why!')
        booleanParam (name: 'executeTests', defaultValue: true, description: '')

    stages {

        //stage added to load a groovy script in gv variable
        stage('Init') {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        
        stage('Build') {
            when {
                expression {
                    BRANCH_NAME == 'dev' && CODE_CHANGES == true
                }
            }
            steps {
                 script {
                     gv.buildApp()  //nameof the function in groovy file.
                 }
                echo "Building version ${NEW_VERSION}"  //double quotes"" needed for string interpolation
            }
        }
        stage('Test') {
            when {
                expression {
                    BRANCH_NAME == 'dev'
                    params.executeTests
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
                echo "deploying version ${params.VERSION}"
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
