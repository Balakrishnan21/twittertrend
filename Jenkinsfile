pipeline{
    agent {
        node {
            label "jenkins_slave"
        }
        }
       
    stages {
        stage('build') {
            steps{
                echo "------------ build started ---------"
                sh 'mvn clean install -Dmaven.test.skip=true'
                echo "------------ build completed ---------"
        }
      }    
       stage ("Sonar Analysis") {
            environment {
               scannerHome = tool 'Balakrishnan21-sonarscanner'
            }
            steps {
                echo '<--------------- Sonar Analysis started  --------------->'
                withSonarQubeEnv('Balakrishnan21-sonarqube-server') {    
                    sh "${scannerHome}/bin/sonar-scanner"
                }    
              echo '<--------------- Sonar Analysis stopped  --------------->' 
            }   
        }
}
}
