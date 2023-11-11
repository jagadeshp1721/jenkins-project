//groovy lang
node{

    def mavenHome = tool name: "maven3.9.4"

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
