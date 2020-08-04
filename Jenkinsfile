pipeline {
environment {
registry = "regibayoandocker98/build"
registryCredential = 'dockerhub_id'
dockerImage = ''
}
agent { label 'slave1' }
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/regibayoan/jenkins-ci-cd-pipeline-3'
}
}
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":latest"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:latest"
}
}
}
}
