pipeline {
  agent any

  stages {
    stage('Get Secret') {
      steps {
        withAkeyless(
          akeylessSecrets: [
            [path: '/1-static-secret/MyFirstSecret', secretValues: [
              [secretKey: 'username', envVar: 'DB_USER', isRequired: true],
              [secretKey: 'password', envVar: 'DB_PASS', isRequired: true]
            ]]
          ]
        ) {
          sh '''
            echo "Using DB user: $DB_USER"
            echo "Using DB password: $DB_PASS"
          '''
        }
      }
    }
  }
}
