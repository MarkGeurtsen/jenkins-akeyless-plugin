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
          // your steps that use the env vars go inside this block
          sh '''
            echo "Using DB user: $DB_USER"
            # do real work with $DB_PASS and $API_KEY
          '''
        }
      }
    }
}
