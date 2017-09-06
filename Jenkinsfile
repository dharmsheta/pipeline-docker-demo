node {
   stage('Preparation') {
      // Get some code from a GitHub repository
      git 'https://github.com/jglick/simple-maven-project-with-tests.git'
      sh 'mvn -version'
   }

   stage('Build') {
        docker.withRegistry('https://localhost:5000') {
         docker.image('maven:3.3.3').inside {
           sh 'mvn -version'
           sh "mvn -Dmaven.test.failure.ignore clean package"
         }
        }
   }

   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
       archive 'pom.xml'
   }
}
