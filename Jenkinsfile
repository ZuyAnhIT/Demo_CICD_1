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

        stage('Copy to IIS folder') {
            steps {
                echo 'Copying publish to IIS folder...'
                bat '''
                    iisreset /stop
                    rd /S /Q "C:\\wwwroot\\HelloJenkins_1"
                    mkdir "C:\\wwwroot\\HelloJenkins_1"
                    xcopy "%WORKSPACE%\\publish" "C:\\wwwroot\\HelloJenkins_1" /E /I /Y /R
                '''
            }
        }

        stage('Deploy to IIS') {
            steps {
                echo 'Creating IIS website (if not exists)...'
                powershell '''
                    Import-Module WebAdministration
                    if (-not (Test-Path IIS:\\Sites\\HelloJenkins_1)) {
                        New-Website -Name "HelloJenkins_1" -Port 85 -PhysicalPath "C:\\wwwroot\\HelloJenkins_1" -ApplicationPool "DefaultAppPool"
                    }
                '''
            }
        }
    }
}
