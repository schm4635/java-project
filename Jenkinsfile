properties([pipelineTriggers([githubPush()])])

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
	sh 'sudo aws s3 cp build.xml s3://jenkins-s3bucket-1lo2csybybwad/'
  } 
  stage('Report') {
	  withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '895c75f8-7512-4f0e-882a-65f5d71bcc4a', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
	} 
  }
}

