def registry = 'https://balakrishnan21.jfrog.io'
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
        stage("Jar Publish") {
        steps {
            script {
                    echo '<--------------- Jar Publish Started --------------->'
                     def server = Artifactory.newServer url:registry+"/artifactory" ,  credentialsId:"jfrog-access"
                     def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                     def uploadSpec = """{
                          "files": [
                            {
                              "pattern": "jarstaging/(*)",
                              "target": "ttrend-libs-release-local/{1}",
                              "flat": "false",
                              "props" : "${properties}",
                              "exclusions": [ "*.sha1", "*.md5"]
                            }
                         ]
                     }"""
                     def buildInfo = server.upload(uploadSpec)
                     buildInfo.env.collect()
                     server.publishBuildInfo(buildInfo)
                     echo '<------------- Jar Publish Ended ------------>'  
            
            }
        }   
    }
        
  }
}
