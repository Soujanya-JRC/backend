pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }
    environment{
        DEBUG = 'true'
        appVersion = '' // this will beocme global, we can use across pipeline
    }
    stages {
        stage('Read the version') {
            steps {
                 script{
                    def packaeJSON = readJSON file: 'package.json'
                    appVersion = packaeJSON.version
                    echo "APP version: ${appVersion}"
                 }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                
            }
        }
        stage('Deploy') {
            when {
                branch 'production'
            }
            steps {
                sh "echo this is deploy"
            }
        }
    
        stage('print params'){
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        }
        stage('Approval'){
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }
    }
    post {
        always{
            echo "this section run always"
            deleteDir()
        }
        success{
            echo "this section run when pipeline success"
        }
        failure{
            echo "this section run when pipeline fails"
        }
    }

}