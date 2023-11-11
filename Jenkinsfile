//groovy lang
node{

    def mavenHome = tool name: "maven3.9.4"

      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"

    //checkout stage
    stage('checkout code'){
        git 'https://github.com/jagadeshp1721/jenkins-project.git'
    }
    
    //build stage
    stage('Build'){
       sh "$mavenHome/bin/mvn clean package"
    }

    //Generate SonarQube Report
    stage ('SonarQube Report'){
        sh "$mavenHome/bin/mvn sonar:sonar"
    }
    
    //Upload Artifact into Artifactory repo
     stage ('Upload Artifact into Artifactory repo'){
        sh "$mavenHome/bin/mvn deploy"
    }

    //Deploy App Into Tomcat Server
    stage('Deploy app into tomcat server'){
        sshagent(['53b341f9-6be9-439b-8397-655dd4430b68']) {
    // some block
        sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline-scriptedway/target/maven-web-application.war root@192.168.0.183:/root/apache-tomcat-9.0.80/webapps"
    }
    }

}
