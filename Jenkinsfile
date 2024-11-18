pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/1raulit/Task4.git', credentialsId: 'github-token'
            }
        }

        stage('Build') {
            steps {
                // Сборка проекта
                bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" Task4.sln /t:Build /p:Configuration=Debug'
            }
        }

        stage('Test') {
            steps {
                // Запуск тестов
                bat 'x64\\Debug\\Task4.exe --gtest_output=xml:x64\\Debug\\Task4_report.xml'
            }
        }
    }

    post {
        always {
            // Публикация результатов тестов
            junit 'x64/Debug/Task4_report.xml'
        }
    }
}
