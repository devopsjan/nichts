pipeline {
   agent any
   tools { 
        maven "M3"
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
         sh "mvn -Dmaven.test.failure.ignore clean package"
      }
   }
   post {
      always {
        junit '**/target/surefire-reports/TEST-*.xml'
      }
   }
}
