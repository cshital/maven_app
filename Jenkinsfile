pipeline {
    agent any
    tools{
        maven 'maven-3.9.8'
    }
 
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/cshital/maven_app.git', branch: env.BRANCH
            }
        }
 
        stage('Build') {
            steps {
                script {
                    echo "Building pull request branch: ${env.BRANCH}"
                    sh 'mvn clean install'   
                }
            }
        }
 
        stage('Test') {
            steps {
                script {
                    echo "Running tests on pull request branch: ${env.BRANCH}"
                    sh 'mvn test'
                }
            }
        }

        stage('Output') {
            steps{
                script{
                    sh 'java src/main/java/com/example/App.java'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
        
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }
 
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
