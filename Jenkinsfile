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
        stage('Sonar analysis')
         environment {
            scannerHome= tool 'balakrishnan21_sonarscanner'
         }
        steps {
            echo '<--------------- Sonar Analysis started  --------------->'
            withSonarQubeEnv('balakrishnan21_sonarqube_server') {
            sh "${scannerHome} /bin/sonar-scanner"
            }
    } 
        echo '<--------------- Sonar Analysis stopped  --------------->' 
 }
