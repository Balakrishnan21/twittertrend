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
                sh 'mvn clean install'
                echo "------------ build completed ---------"
        }
      }
    } 
 }
