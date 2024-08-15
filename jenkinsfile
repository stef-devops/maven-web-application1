node{

def mavenhome = tool name: "3.9.8"
stage('checkoutgit'){
git branch: 'development', url: 'https://github.com/stef-devops/maven-web-application1.git'
}

stage('maven'){
sh "$mavenhome/bin/mvn clean package"
}

stage('sonarqube'){
sh "$mavenhome/bin/mvn clean sonar:sonar"
}

stage('nexus'){
sh "$mavenhome/bin/mvn clean deploy"
}

stage('deploy'){
    sshagent(['e2ce7b1f-c212-4431-b5e4-becd627049de']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.207.162.92:/opt/apache-tomcat-10.1.28/webapps"    // some block
}
}
}
