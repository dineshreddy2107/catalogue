pipeline {
    agent {
        label 'agent-1'
    }
    environment {
        appVersion = ''
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    /* parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    } */
    stages {
       
        stage('Read package.json') {
            steps {
                script {
                    // Read the entire package.json file into a Groovy map/object
                    def packageJSON = readJSON file: 'package.json'

                    // Access specific properties, for example, the version or name
                     appVersion = packageJSON.version
                    echo "Package version: ${appVersion}"
                    
                }
            }
        }

        
       /*  stage('Example') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        } */
        stage('Test ') {
            steps {
                script {
                echo "Testing..."
                }
            }
        }
        stage('Deploy') {
            steps {
               script {
                echo "Deploying..."
                }
            }
        }
    }
    post {
        always{
            echo 'I will always say hello again!'
            deleteDir()
        }
        success {
            echo 'Hello Successs'
        }
    }
}
