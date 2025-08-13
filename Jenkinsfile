pipeline {
    agent any

    stages {
        
        stage('Compile') {
            steps {
                echo 'Compiling the Code'
                sh 'mvn compile'
            }
        }
        stage('Code Review') {
            steps {
                echo 'Reviewing the Code'
                sh "mvn pmd:pmd"
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Unit Testing the Code'
                sh 'mvn test'
            }
        }
        stage('Coverage Analysis') {
            steps {
                echo 'Static Code Coverage Analysis of the Code'
                sh 'mvn verify'
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging the Code'
                sh 'mvn package'
            }
        }
        stage('Publish the artifacts') {
            steps {
                echo 'Publishing the artifact to Jfrog'
                sh 'mvn -U deploy -s settings.xml'
            }
        }
    }
}
