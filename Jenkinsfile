pipeline {
  agent any

  stages {
    stage('Check GW URL') {
      steps {
        echo "Gateway URL is: ${GW_URL}"
      }
    }
    stage('Get Secret') {
      steps {
        // no need for script{} unless you're doing Groovy logic/defs
        withAkeyless(
          configuration: [
            akeylessCredentialId: 'akeyless-access',   // Jenkins Credentials ID
            akeylessUrl: 'https://hvp.akeyless.io',
            timeout: 60,
            skipSslVerification: false
          ],
          akeylessSecrets: [
            [path: '/1-static-secret/MyFirstSecret', secretValues: [
              [secretKey: 'username', envVar: 'DB_USER', isRequired: true],
              [secretKey: 'password', envVar: 'DB_PASS', isRequired: true]
            ]]
          ]
        ) {
          // your steps that use the env vars go inside this block
          sh '''
            echo "Using DB user: $DB_USER"
            # do real work with $DB_PASS and $API_KEY
          '''
        }
      }
    }

    stage('Build')  { steps { echo 'Building...'  } }
    stage('Test')   { steps { echo 'Testing...'   } }
    stage('Deploy') { steps { echo 'Deploying...' } }
  }
}
