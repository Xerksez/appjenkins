pipeline {
    agent {
        docker {

            image 'xerksez/obraz:latest'

            args '-u root' // Jeśli potrzebujesz uruchamiać polecenia jako root (opcjonalne)

            // args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Pobieranie kodu') {
            steps {
                // Pobierz kod z repozytorium GitHub
                git 'https://github.com/xerksez/appjenkinsgit'
            }
        }
        stage('Instalacja i uruchomienie aplikacji') {
            steps {
                // Kompilacja (np. npm install) i uruchomienie aplikacji
                sh 'npm install'
                sh 'npm start'
            }
        }
        stage('Testy jednostkowe') {
            steps {
                // Wykonaj testy jednostkowe (np. npm test) i raportuj
                sh 'npm test'
                junit 'results/**/*.xml'
            }
        }
        stage('ESLint') {
            steps {
                // Sprawdź kod za pomocą ESLint
                sh 'eslint .'
            }
        }
    }
}
