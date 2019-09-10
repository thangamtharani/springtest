node {
    // reference to maven
    // ** NOTE: This 'maven-3.6.1' Maven tool must be configured in the Jenkins Global Configuration.   
    def mvnHome = tool 'M2'

    // holds reference to docker image
    def dockerImage
    // ip address of the docker private repository
    
    def dockerRepoUrl = "localhost:8083"
    def dockerImageName = "hello-world-java"
    def dockerImageTag = "${dockerRepoUrl}/${dockerImageName}:${env.BUILD_NUMBER}"
    
    stage('Clone Repo') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/thangamtharani/springtest.git'
      // Get the Maven tool.
      // ** NOTE: This 'maven-3.6.1' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M2'
    }    
  
    stage('Build Project') {
      // build project via maven
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
    }
	
/*	stage('Run Unit Tests & Sonar'){
      parallel(
        publishJunitTestsResultsToJenkins: {
          echo "Publish junit Tests Results"
		  junit '/target/surefire-reports/TEST-*.xml'
		  archive 'target/*.jar'
        },
        publishJunitTestsResultsToSonar: {
		script {
          openshift.withCluster() {
            openshift.newApp('sonarqube-openshift-docker~https://github.com/OpenShiftDemos/sonarqube-openshift-docker')
          }
        }
          echo "This is branch b"
      })
    }
		
    stage('Build Docker Image') {
      // build docker image
      sh "whoami"
     // sh "ls -all /var/run/docker.sock"
      sh "mv ./target/hello*.jar ./data" 
      
      dockerImage = docker.build("hello-world-java")
	   sh "docker run -p 8080:8080 -it --rm hello-world-java"
	  
    }
   
    stage('Deploy Image'){
      
      // deploy docker image to nexus

      echo "Docker Image Tag Name: ${dockerImageTag}"

      sh "docker login -u admin -p admin123 ${dockerRepoUrl}"
      sh "docker tag ${dockerImageName} ${dockerImageTag}"
      sh "docker push ${dockerImageTag}"
    }*/
}
