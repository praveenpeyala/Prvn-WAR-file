pipeline {
  agent { master }
  stages {
     stage('S1-Cont. Downld') 
       {
        steps 
          {
              git 'https://github.com/praveenpeyala/Prvn-WAR-file.git'
          }
       }
     stage('S2-Cont. Build')
       {
        steps
          {
              sh 'mvn clean package'
              input 'Approve this build to go for deploy phase'
          }
       }
    stage('S3-Cont. Deploy')
      {
        steps
          {
              deploy adapters: [tomcat8(credentialsId: '3b8c23a9-21f9-4012-b3a9-f4ae496c4b08', path: '', url: 'http://172.31.35.114:8080/')], contextPath: 'Tomcat-QA-Pipeline_Script-Deploy', war: '**/*.war'
          }
      }
    stage('S4-Cont. Test')
      {
        steps
          {
              echo 'The war file has passed all the tests...Now you can go for deployment of that war file in Production Server'
              input 'Approve this test cases to go for delivery phase'
          }
      }
    stage('S5-Cont. Delivery')
      {
        steps
          {
              deploy adapters: [tomcat8(credentialsId: '3b8c23a9-21f9-4012-b3a9-f4ae496c4b08', path: '', url: 'http://172.31.46.155:8080/')], contextPath: 'Tomcat-PROD-Pipeline_Script-Delivery', war: '**/*.war'
              emailext attachLog: true, body: 'This Email is sent out from Jenkins - Job: $PROJECT_NAME of Build # $BUILD_NUMBER where the Job-Build is $BUILD_STATUS:', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:', to: 'praveenpeyala10@gmail.com'
          }
      }
   }
}
