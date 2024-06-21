pipeline {
    agent {
        dockerContainer {
            image 'xerksez/obraz:latest'
        }
    }
    stages {
        stage('Pobieranie kodu') {
            steps {
                git 'https://github.com/xerksez/appjenkinsgit'
            }
        }
        stage('Instalacja i uruchomienie aplikacji') {
            steps {

                sh 'npm install'
                sh 'npm start'
            }
        }
        stage('Testy jednostkowe') {
            steps {
                sh 'npm test'
                junit 'results/**/*.xml'
            }
        }
        stage('ESLint') {
            steps {
                sh 'eslint .'
            }
        }
    }
}
