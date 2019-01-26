node {
    def app

    stage('Clone repository') {
        

        checkout scm
    }
     stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
    stage('Build Docker Image'){
     sh 'docker build -t tawfik/app:2.0.0 .'
   }

    stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u tawfik -p ${dockerHubPwd}"
     }
     sh 'docker push tawfik/app:2.0.0'
   }
}
