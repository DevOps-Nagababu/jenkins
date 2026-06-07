pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }
    environment {
        COURSE = 'Jenkins'
    }

    options {
        disabledConcurrentBuilds()  // this is will disable 2 builds at a time this will be helpful for prod env
        timeout(time: 5, unit: 'SECONDS')
    }
     parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    stages {
        stage('Build') {
            steps {
                script{
                     sh """
                        echo "Building"
                        echo $COURSE
                        sleep 10
                     """
                    // exit 1 (failuer) for testing
                }
            }
        }

        stage('Test') {
            steps {
                 script{
                     sh """
                        echo "Testing"
                        echo "Hello ${params.PERSON}"
                        echo "Biography: ${params.BIOGRAPHY}"
                        echo "Toggle: ${params.TOGGLE}"
                        echo "Choice: ${params.CHOICE}"
                        echo "Password: ${params.PASSWORD}"
                     """
                }
            }
        }

        stage('Deploy') {
            steps {
                 script{
                     sh """
                        echo "Deploying"
                     """
                }
            }
        }

        //  post Build it will execute alwasy

        post {
            alwasy {
                echo 'I will execute always'
            }
            // this secction will be useful for sedning alter to team via email or teams message
            success { 
                echo "pipeline success"
            }
            failure{
                echo "pipeline failure"
            }
        }
    
    }
}