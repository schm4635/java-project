properties([pipelineTriggers(githubPush()])])

node('linux') {
  stage('Unit Tests') {
      git 'https://github.com/schm4635/java-project.git'
      sh 'ant -buildfile test.xml'
      sh 'ant -f test.xml -v'
  }
  stage('Build') {
      sh 'ant'
      sh 'ant -f build.xml -v'
  }
  stage('Deploy') {
      
  } 
  stage('Report') {
	withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAI6SM72DTXYBGS24Q', credentialsId: 'lQackKr6KQGsRxf8s5H+28Ae3l3Ne+nOwyyawarh', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {       
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
	} 
}
}
