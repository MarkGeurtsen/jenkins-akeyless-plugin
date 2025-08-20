pipeline {
    agent any

    
    stages {

        stage('Get Secret') {
            steps {
                script {
                    
                    withAkeyless(
                    configuration: [
                      akeylessCredentialId: 'akeyless-access', // Jenkins Credentials ID for Akeyless auth
                      akeylessUrl: 'https://api.akeyless.io',
                      timeout: 60,
                      skipSslVerification: false
                    ],
                    akeylessSecrets: [
                      // Example: JSON secret with keys 'username' and 'password'
                      [path: '/app/db-credentials', secretValues: [
                        [secretKey: 'username', envVar: 'DB_USER', isRequired: true],
                        [secretKey: 'password', envVar: 'DB_PASS', isRequired: true]
                      ]],
                      // Example: single-value secret (retrieve all as 'data')
                      [path: '/app/api-key', secretValues: [
                        [secretKey: 'data', envVar: 'API_KEY', isRequired: true]
                      ]]
                    ]
                  )
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
