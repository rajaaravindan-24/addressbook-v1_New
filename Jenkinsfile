pipeline {
    agent none

    tools {
        maven 'mymaven'
       
    }
   parameters {
         string(name: 'Env', defaultValue: 'Test', description: 'Version to deploy')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Decide to run test cases')
        choice(name: 'APPVERSION', choices: ['1.1', '1.2', '1.3'], description: 'Select application version')

    }
    stages {
        
        stage('Compile') {
            agent any
            steps {
                echo 'Compiling the Code in ${params.Env} environment'
                sh 'mvn compile'
            }
        }
        stage('Code Review') {
             agent any
            steps {
                echo 'Reviewing the Code'
                sh "mvn pmd:pmd"
            }
        }
        stage('Unit Test') {
            agent any
            when {
                expression { params.executeTests }
            }
            steps {
                echo 'Unit Testing the Code'
                sh 'mvn test'
            }
        }
        stage('Coverage Analysis') {
             agent any
            steps {
                echo 'Static Code Coverage Analysis of the Code'
                sh 'mvn verify'
            }
        }
        stage('Package') {
             agent {label 'linux_slave'}
            steps {
                echo 'Packaging the Code version ${params.APPVERSION}'
                sh 'mvn package'
            }
        }
        stage('Publish the artifacts') {
            agent any
            steps {
                echo 'Publishing the artifact to Jfrog'
                sh 'mvn -U deploy -s settings.xml'
            }
        }
    }
}
