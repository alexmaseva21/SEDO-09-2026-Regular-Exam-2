// Runs shell commands on Linux agents and batch commands on Windows agents
def runCmd(String cmd) {
    if (isUnix()) {
        sh cmd
    } else {
        bat cmd
    }
}

pipeline {
    agent any

    // Check the repository for new commits on main every minute
    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/alexmaseva21/SEDO-09-2026-Regular-Exam-2.git'
            }
        }

        stage('Restore dependencies') {
            steps {
                script { runCmd 'dotnet restore' }
            }
        }

        stage('Build') {
            steps {
                script { runCmd 'dotnet build --no-restore --configuration Release' }
            }
        }

        stage('Run unit tests') {
            steps {
                script { runCmd 'dotnet test Homies.Tests/Homies.Tests.csproj --no-build --configuration Release --verbosity normal' }
            }
        }

        stage('Run integration tests') {
            steps {
                script { runCmd 'dotnet test Homies.IntegrationTests/Homies.IntegrationTests.csproj --no-build --configuration Release --verbosity normal' }
            }
        }
    }
}
