node
{
  def mavenHome=tool name: "maven3.6.2"

 stage('Checkout')
 {
 	git branch: 'master', credentialsId: '4310e204-6e15-49c8-aa3e-4d63aef877d3', url: 'https://github.com/devops1github1/maven-web-application-development.git'

 }
 stage('Build')
 {
 sh  "${mavenHome}/bin/mvn clean package"
 }

 stage('ExecuteSoanrQubeReport')
 {
 sh  "${mavenHome}/bin/mvn sonar:sonar"
 }

 stage('UploadArtifactintoNexus')
 {
 sh  "${mavenHome}/bin/mvn deploy"
 }

 stage('DeployAppintoTomcat')
 {
    sshagent(['ed833a5b-4248-40cd-b77a-1c4699baaedd']) {

    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.167.87.65:/opt/apache-tomcat-9.0.64/webapps/"
    }
 }

 stage('SendEmailNotification')
 {
 emailext body: '''Deployment Done...
Krishna''', subject: 'Deployment Done', to: 'devopsgithub100@gmail.com'
 }

}