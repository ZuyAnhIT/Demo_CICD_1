pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning source code...'
                git branch: 'main', url: 'https://github.com/ZuyAnhIT/Demo_CICD_1.git'
            }
        }

        stage('Restore Packages') {
            steps {
                echo 'Restoring NuGet packages...'
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Publish') {
            steps {
                echo 'Publishing project...'
                bat 'dotnet publish -c Release -o ./publish'
            }
        }

        stage('Deploy to IIS') {
            steps {
                echo 'Copying to IIS folder...'
                bat '''
                    rd /S /Q "C:\\wwwroot\\Demo_CICD_1"
                    mkdir "C:\\wwwroot\\Demo_CICD_1"
                    xcopy /E /I /Y "publish\\*" "C:\\wwwroot\\Demo_CICD_1"
                '''
            }
        }
    }
}
