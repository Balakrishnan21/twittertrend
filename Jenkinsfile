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
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "------------ build completed ---------"
        }
      }
    } 
 }
