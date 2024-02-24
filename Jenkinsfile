pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'  // Instalira npm zavisnosti, uključujući Playwright
            }
        }

        stage('Run Playwright Tests') {
            steps {
                sh 'npx playwright test'  // Pokreće Playwright testove
            }
        }

        // Ostale faze po potrebi
    }

    post {
        // Obrada rezultata, notifikacija, čišćenje, itd.
    }
}
