pipeline {
  agent any
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Install') {
      steps {
        sh 'composer install --no-interaction --prefer-dist --no-progress'
        sh '[ -f .env ] || cp .env.example .env'
        sh 'php artisan key:generate --force'
      }
    }
    stage('Test') {
      steps { sh 'DB_CONNECTION=sqlite DB_DATABASE=:memory: php artisan test' }
    }
  }
}
