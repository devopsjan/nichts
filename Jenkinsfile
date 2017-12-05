pipeline {
   agent any
   def mvnHome
   stages {
      stage('Preparation') {
         checkout scm
         // Get the Maven tool.
         // ** NOTE: This 'M3' Maven tool must be configured
         // **       in the global configuration.           
         mvnHome = tool 'M3'
      }
      stage('Build') {
         // Run the maven build
         if (isUnix()) {
            sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
         } else {
            bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   post {
      always {
        junit '**/target/surefire-reports/TEST-*.xml'
      }
   }
}
