pipeline {
environment {
imagename = "kanchansoni/java-maveen"
registryCredential = 'dockerhub'
dockerImage = ''
}
agent any
stages {
stage('Cloning Git') {
steps {
  echo "taking login" 
git([url: 'https://github.com/KanchanSoni16/helloword-java.git', branch: 'main', credentialsId: 'Github'])
}
}
stage('Building image') {
steps{
script {
  sh 'docker build -t kanchansoni/test .'
dockerImage = docker.build imagename
}
}
}
stage('Deploy Image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push("$BUILD_NUMBER")
dockerImage.push('latest')
}
}
}
}
stage('Remove Unused docker image') {
steps{
sh "docker rmi $imagename:$BUILD_NUMBER"
sh "docker rmi $imagename:latest"
}
}
}
}
