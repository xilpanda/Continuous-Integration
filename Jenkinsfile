pipeline {
    agent any

    tools {
        // Dodajem ovu liniju da koristite Node.js konfiguraciju definisanu u Jenkins
        nodejs 'MyNode'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                // 'npm install' će koristiti Node.js i npm definisane u 'MyNode' konfiguraciji
                sh 'npm install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                // 'npx playwright test' će takođe koristiti Node.js i npm iz 'MyNode'
                sh 'npx playwright test'
            }
        }

        // Ostale faze po potrebi
    }

    post {
        // Obrada rezultata, notifikacija, čišćenje, itd.
    }
}
