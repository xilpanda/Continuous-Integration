# CI/CD Pipeline sa Playwright Testiranjem

## Pregled

Ovaj dokument sadrži opis postupka postavljanja Jenkins CI/CD pipeline-a sa integracijom Playwright testova za automatizovano testiranje web aplikacija.

## Instalacija i Konfiguracija Jenkinsa

1. **Instalacija Jenkinsa na Ubuntu Server:**
    - Preuzimanje i dodavanje ključa Jenkins repozitorijuma:
      ```
      wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
      ```
    - Dodavanje Jenkins repozitorijuma u sistem:
      ```
      sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
      ```
    - Ažuriranje paketa i instalacija Jenkinsa:
      ```
      sudo apt-get update
      sudo apt-get install jenkins
      ```

2. **Pokretanje Jenkinsa:**
    - Jenkins servis je pokrenut i konfigurisan da se automatski pokreće pri startu sistema:
      ```
      sudo systemctl start jenkins
      sudo systemctl enable jenkins
      ```

3. **Pristup Jenkins Web Interfejsu:**
    - U browseru unijeti adresu `http://<Jenkins-Server-IP>:8080` da bi se pristupilo Jenkinsu.

## Konfiguracija Jenkins Projekta

1. **Kreiranje Novog Jenkins Projekta:**
    - Na Jenkins dashboardu, izabrati "New Item", upisati ime projekta, i odabrati "Freestyle project".

2. **Konfiguracija SCM-a:**
    - U sekciji "Source Code Management", izabrati "Git" i unijeti URL Git repozitorijuma, kao i granu koja se prati (`main`).

3. **Dodavanje Build Koraka:**
    - U sekciji "Build", dodati korak "Execute shell" i unijeti komande potrebne za pokretanje Playwright testova:
      ```
      npm install
      npm run test
      ```

## Jenkinsfile i Playwright Integracija

1. **Kreiranje Jenkinsfile-a:**
    - U root direktorijumu projekta kreiran je `Jenkinsfile` sa definicijom pipeline-a:
      ```groovy
      pipeline {
          agent any
          stages {
              stage('Install') {
                  steps {
                      sh 'npm install'
                  }
              }
              stage('Test') {
                  steps {
                      sh 'npm run test'
                  }
              }
          }
      }
      ```
    - Ovaj `Jenkinsfile` definiše dvije faze: Instalaciju zavisnosti i pokretanje Playwright testova.

2. **Playwright Test Skripta:**
    - U `package.json` fajlu definisan je skript za pokretanje Playwright testova:
      ```json
      "scripts": {
          "test": "playwright test"
      }
      ```
    - Testovi su kreirani za testiranje web aplikacije dostupne na `https://example.cypress.io/todo`.

## Izvršavanje i Monitoring

- Nakon commit-a izmjena u Git repozitorijumu, Jenkins automatski pokreće konfigurisan pipeline.
- Rezultati build-a i testova mogu se pratiti u Jenkins web interfejsu kroz "Console Output" za svaki build.

## Zaključak

Ovim postupkom uspostavljen je CI/CD sistem koji automatski testira web aplikaciju korišćenjem Playwright-a, omogućavajući brže i pouzdanije isporuke softvera.


