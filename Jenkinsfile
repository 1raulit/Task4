pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/1raulit/Task4.git', credentialsId: 'github-token'
            }
        }
        
        stage('Restore NuGet Packages') {
            steps {
                // Восстановление NuGet пакетов
                bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" -t:restore Task4.sln'
            }
        }

        stage('Build') {
            steps {
                // Сборка проекта
                bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" Task4.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Запуск тестов
                bat 'x64\\Release\\Task4.exe --gtest_output=xml:x64\\Release\\Task4_report.xml'
            }
        }
    }

    post {
        always {
            // Публикация результатов тестов
            junit 'x64/Release/Task4_report.xml'
        }
    }
}
