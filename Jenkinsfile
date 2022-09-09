pipeline {
  agent {
    kubernetes {
      yamlFile 'pod.yaml'
    }
  }
  stages {
    stage('Build with Kaniko') {
      steps {
        container(name: 'kaniko', shell: '/busybox/sh') {
          sh '''#!/busybox/sh
            echo "FROM jenkins/inbound-agent:latest" > Dockerfile
            /kaniko/executor --context `pwd` --destination bjgomes/hello-kaniko:latest
          '''
        }
      }
    }
  }
}
