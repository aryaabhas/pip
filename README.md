pipeline {
agent any
tools {
maven 'MAVEN_HOME'
jdk 'JDK17'
}
stages {
stage('Checkout') {
steps {
git branch: 'main',
url: 'https://github.com/Priyanshu-Madhup/exp6.git'
}
}
stage('Build') {
steps {
dir('demo') {
bat 'mvn clean package'
}
}
}
stage('Test') {
steps {
dir('demo') {
bat 'mvn test'
}
}
}
}
post {
always {
junit allowEmptyResults: true,
testResults: '**/target/surefire-reports/*.xml'
}
}
}
