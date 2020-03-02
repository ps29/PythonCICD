#!/usr/local/bin/groovy
pipeline {
    agent { node { label 'testing' } }

    environment {
        TEST_PREFIX = "test-IMAGE"
        
    }

    stages {

         stage("Getting Information Regarding Build") {
            steps {
                 echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                
                
            }
        }

        
          stage("Running Unittest") {
            steps {
                sh "/usr/local/bin/nosetests  /home/ps/PythonCICD/tests/test_helloworld.py"
                
                
            }
        }

        stage("Package Installation") {
            steps {
                sh "/usr/bin/pip3 install -r /home/ps/PythonCICD/requirements.txt"
                
            }
          } 

        stage("Deploy") {
            steps {
                sh "pwd"
                sh "/usr/bin/python3  /usr/local/bin/nosetests /home/ps/PythonCICD/helloworld/app.py"
                
            }
            post {
                always {
                    echo "always forever"
                  }
                success {
                    // we only worry about archiving the jar file if the build steps are successful
                    archiveArtifacts(artifacts: 'helloworld/*.py', allowEmptyArchive: true)
                }
              failure {
                  echo "failed"
               }
           }
        }

        stage("Production") {
        //when {
          //      environment TEST_PREFIX: "test-IMAGE"
                
           // }
            steps {
                echo "task fro production"
                
             }
           }
        
  
    }
}
