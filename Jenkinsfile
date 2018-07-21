pipeline {
  agent any
  stages {
    stage('Poll SCM') {
      steps {
        git(url: 'https://github.com/Sea-feliz/Jenkins_docker.git', branch: 'master')
      }
    }
    stage('Docker Build') {
      steps {
        sh '''sh cd nhttpd
IMAGE=$(cat Dockerfile | head -1 | sed -e 's/#//')
docker build -t $IMAGE .'''
      }
    }
    stage('Docker publish') {
      steps {
        sh '''sh cd nhttpd
IMAGE=$(cat Dockerfile | head -1 | sed -e 's/#//')
docker push $IMAGE'''
      }
    }
    stage('Deployment') {
      steps {
        sh '''sh cd nhttpd
IMAGE=$(cat Dockerfile | head -1 | sed -e 's/#//')
kubectl set image deployment/student nhttpd=$IMAGE'''
      }
    }
  }
}
