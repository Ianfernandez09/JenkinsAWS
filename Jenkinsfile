pipeline {
  agent any
  stages {
    stage('Ping') {
      steps {
        sh 'ansible all -i hosts -m ping -f 5'
      }
    }

    stage('Instalar Docker') {
      steps {
        ansiblePlaybook 'dependencias.yml'
        sh 'ansible all -i worker1 -a "sudo systemctl enable docker"'
      }
    }

    stage('Enviar Compose e iniciar Contenedor') {
      steps {
        sh 'ansible all -i worker1 -m copy -a "src=docker-compose.yml dest=/tmp/docker-compose.yml"'
        ansiblePlaybook 'iniciar_docker2.yml'
      }
    }

  }
}