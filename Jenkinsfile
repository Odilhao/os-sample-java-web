node {
   def mvnHome
   stage('Preparation') {
      git 'https://github.com/Odilhao/os-sample-java-web.git'
      mvnHome = tool 'M3'
   }
   stage('Build') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
           archive 'target/*.jar'
   }
           stage('Publish') {
 nexusArtifactUploader artifacts: [[artifactId: 'os-sample-java-web-war-${BUILD_ID}', classifier: 'latest', file: 'target/ROOT.war', type: 'war']], credentialsId: '83e208c4-0567-31c6-b0ff-d2c9ae65258b', groupId: 'org.cx.main', nexusUrl: 'nexus.apps.cx.4linux.com.br', nexusVersion: 'nexus3', protocol: 'http', repository: 'cx', version: '0.1'
   }
    }
