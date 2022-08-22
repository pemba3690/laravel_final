pipeline {
  agent any
  stages {
    stage("verify tooling") {
      steps {
        sh '''
           sudo docker version
           sudo docker compose version
           sudo curl --version
        '''
      }
    }
    stage('Prune Docker data') {
      steps {
        sh 'sudo docker system prune -a --volumes -f'
      }
    }
    stage('Start container') {
      steps {
       sh 'sudo docker-compose build '
        sh 'sudo docker-compose up -d '
        sh 'sudo docker-compose ps'
      }
    }
    stage('Run tests against the container') {
      steps {
        sh 'sudo curl http://localhost:8848 '
      }
    }
  }
  post {
    always {
      sh 'sudo docker compose ps'
    }
  }
}


