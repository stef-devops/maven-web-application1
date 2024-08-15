node{

    echo "The node name is= ${env.NODE_NAME}"
    echo "The job name is= ${env.JOB_NAME}"
    echo "The build number is= ${env.BUILD_NUMBER}"
    
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
//jacoco changeBuildStatus: true, deltaBranchCoverage: '10', deltaClassCoverage: '10', deltaComplexityCoverage: '10', deltaInstructionCoverage: '10', deltaLineCoverage: '10', deltaMethodCoverage: '10', maximumBranchCoverage: '10', maximumClassCoverage: '10', maximumComplexityCoverage: '10', maximumInstructionCoverage: '10', maximumLineCoverage: '10', maximumMethodCoverage: '10', minimumBranchCoverage: '10', minimumClassCoverage: '10', minimumComplexityCoverage: '10', minimumInstructionCoverage: '10', minimumLineCoverage: '10', runAlways: true
    //    jacoco changeBuildStatus: true, deltaBranchCoverage: '80', deltaClassCoverage: '80', deltaComplexityCoverage: '80', deltaInstructionCoverage: '80', deltaLineCoverage: '80', deltaMethodCoverage: '80', maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80', runAlways: true
}

