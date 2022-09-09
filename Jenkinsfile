pipeline {
  agent {
    kubernetes {
      yamlFile 'pod.yaml'
    }
  }
  stages {
    stage('Build and push with Kaniko') {
      steps {
        container(name: 'kaniko', shell: '/busybox/sh') {
          sh '''#!/busybox/sh
            /kaniko/executor --context `pwd` --destination bjgomes/tomcat:latest
          '''
        }
      }
    }
    stage('Deploy to kubernetes') {
      steps {
        container(name: 'kubectl', shell: '/busybox/sh') {
          sh '''#!/busybox/sh
            kubectl apply -f manifest.yaml
          '''
        }
      }
    }
  }
}
