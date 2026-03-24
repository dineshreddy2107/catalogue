pipeline {
    agent {
        label 'agent-1'
    }
    environment {
        appVersion = ''
        REGION = "us-east-1"
        ACC_ID = "315949462026"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
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

        
       stage('Install Dependencies') {
        steps{
            script {
                sh """
                 npm install 

                """
            }
        }
       }
       stage('Docker Build') {
        steps {
            script{
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh """
                            aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                            docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .
                            docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                        """
                }
            }
        }
       }


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
