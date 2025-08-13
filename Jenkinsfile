pipeline {
    agent none

    tools {
        maven 'mymaven'
       
    }

    stages {
        
        stage('Compile') {
            agent any
            steps {
                echo 'Compiling the Code'
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
                echo 'Packaging the Code'
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
