node{
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/vishnukraj1111/my-app'
   }
   stage('Mvn Package'){
       def mvnHome = tool name: 'maven35', type: 'maven'
       def mvnCMD = "${mvnHome}/bin/mvn"
            sh "${mvnCMD} clean package"
   }
   stage('Mvn Unit Test'){
       def mvnHome = tool name: 'maven35', type: 'maven'
       def mvnCMD = "${mvnHome}/bin/mvn"
            sh "${mvnCMD} clean test"
   }
   stage('Mvn Intergration Test'){
       def mvnHome = tool name: 'maven35', type: 'maven'
       def mvnCMD = "${mvnHome}/bin/mvn"
            sh "${mvnCMD} clean verify"
   }
   stage('Build Docker Image'){
     sh 'docker build -t vishnukraj1/my-app:1.0 .'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u vishnukraj1 -p ${dockerHubPwd}"
     }
     sh 'docker push  vishnukraj1/my-app:1.0'
   }
    stage('Run Container on Dev Server'){
     sh 'docker run -itd --name my-app -p 8081:8080 vishnukraj1/my-app:1.0'
   }
}
