def templateName = 'ciccdd' 
pipeline {
    agent any
     tools
        {
            maven 'M2'
        }
  stages {
  stage('Build') {
     steps {
    git url: "https://github.com/santhoshp5/springtest.git"
    sh "mvn clean package"
    stash name:"jar", includes:"target/hello-world-0.1.0.jar"
     }
  }
 
  stage('Build Image') {
     steps {
    unstash name:"jar"
    sh "oc start-build ciccdd --from-file=target/hello-world-0.1.0.jar --follow"
     }
  }
  stage('Deploy') {
    steps {
        script {
            openshift.withCluster() {
                openshift.withProject() {
                  def rm = openshift.selector("dc", templateName).rollout().latest()
                  }
            }
        }
      }
  }
  }
}
