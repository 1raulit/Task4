pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Клонування репозиторію з використанням облікових даних
                git url: 'https://github.com/1raulit/Task4.git', credentialsId: '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'
            }
        }
        
        stage('Build') {
            steps {
                // Збірка проекту з використанням MSBuild з правильним екрануванням
                bat "\"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe\" Task4.sln /t:Build /p:Configuration=Release"
            }
        }

        stage('Test') {
            steps {
                // Запуск тестів з використанням Google Test
                bat "x64\\Release\\Task4.exe --gtest_output=xml:x64\\Release\\Task4_report.xml"
            }
        }
    }

    post {
        always {
            // Публікація результатів тестів у форматі JUnit
            junit 'x64/Release/Task4_report.xml'
        }
    }
}
