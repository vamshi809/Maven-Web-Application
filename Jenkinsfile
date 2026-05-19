node{

def mavenHome = tool name: 'maven 3.9.15'
stage('codecheckout')
{

git branch: 'development', credentialsId: 'e7e618d1-9942-4cd5-bb4b-e090ffe87bd5', url: 'https://github.com/vamshi809/Maven-Web-Application.git'


}



stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}

stage('SonarQube Report')

{

sh "${mavenHome}/bin/mvn clean sonar:sonar"

}

stage('Upload into Nexus')
{
sh "${mavenHome}/bin/mvn clean deploy"

}

stage('Deploy Application into Tomcat')
{

sshagent(['4c1783ea-bafc-449b-8839-276a3116c45e']) {

sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ubuntu@13.126.120.180:/home/ubuntu/apache-tomcat-9.0.118/webapps/"

    

}
