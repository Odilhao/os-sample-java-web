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
 nexusArtifactUploader artifacts: [[artifactId: 'os-sample-java-web-war-${BUILD_ID}', classifier: 'latest', file: 'target/ROOT.war', type: 'war']], credentialsId: '7534a4df-22db-4cb1-9b4e-6398541b74d9', groupId: 'org.oc-ci.main', nexusUrl: '${NEXUS_URL}', nexusVersion: 'nexus3', protocol: 'http', repository: 'upload-jenkins', version: '0.1'
   }
    }
