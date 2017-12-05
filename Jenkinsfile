pipeline {
   agent any
   def mvnHome
   tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    stages {
       stage ('Initialize') {
           steps {
               sh '''
                  echo "PATH = ${PATH}"
                  echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
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
