pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'What is the application version?')

    }

    environment{
        def appVersion = '' // global variable which can be accessed anywhere within the file
        nexusUrl = 'nexus.guru97s.cloud:8081'
    }
    stages {
        stage('Print The Version'){
            steps {
                script{
                    echo "Application Version: ${params.appVersion}"
                }
            }
        }
        stage('Init'){
            steps {
                sh """
                cd terraform
                terraform init

                """
            }
        }
        stage('Plan'){
            steps {
                sh """
                cd terraform
                terraform plan -var="app_version=${params.appVersion}"

                """
            }
        }
        /* stage('Deploy'){
            steps {
                sh """
                cd terraform
                terraform init

                """
            }
        } */
    }
     post { 
        always { 
            echo 'I will always say Hello again!'
            //deleteDir()
        }
        success { 
            echo 'I will run only when pipeline is success'
        }
        failure { 
            echo 'I will run only when pipeline is failure'
        }
      }
}