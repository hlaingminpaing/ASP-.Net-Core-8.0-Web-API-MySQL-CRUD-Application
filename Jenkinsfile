pipeline {
    agent any

    environment {
        DOTNET_ROOT = "/usr/bin/dotnet"
        PATH = "${DOTNET_ROOT}:${env.PATH}"
        CONNECTION_STRING = "Server=crud.cvrlgpla3e5u.ap-southeast-1.rds.amazonaws.com;Database=crud;User=root;Password=asd123123;"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/hlaingminpaing/ASP-.Net-Core-8.0-Web-API-MySQL-CRUD-Application.git'
            }
        }

        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Apply Migrations') {
            steps {
                sh "dotnet ef database update --connection '${env.CONNECTION_STRING}'"
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish --configuration Release --output ./publish'
            }
        }

        stage('Deploy') {
            steps {
                // Assuming you have a deployment script or steps
                sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}

