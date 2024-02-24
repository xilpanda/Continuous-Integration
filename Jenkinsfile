pipeline {
    agent any

    tools {
        // Node.js konfiguracija je definisana u Jenkinsu
        // 'NodeJS-configuration-name' ime Node.js konfiguracije
        nodejs 'NodeJS-configuration-name'
    }

    stages {
        stage('Checkout') {
            steps {
                // Preuzmite najnoviji kod iz SCM-a
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Instalira potrebne npm zavisnosti, uključujući Playwright
                sh 'npm install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                // Pokreće Playwright testove koristeći definisanu npm skriptu 'test'
                sh 'npm run test'
            }
        }
    }

    post {
        always {
            // Ovde dodajem korake koji se izvršavaju nakon testova
                   
            
            // Koraci za čišćenje, notifikacije, itd.
        }

        success {
            // Koraci za uspješno izvršenje pipeline-a
            echo 'Testovi su uspješno prošli!'
        }

        failure {
            // Koraci za neuspješno izvršenje pipeline-a
            echo 'Došlo je do greške tokom izvršavanja testova.'
        }
    }
}
