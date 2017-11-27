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
      junit 'reports/*.xml'
  }
}
	stage ('Test'){    
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAJCEQ2HLUKZ3X5ZUA', credentialsId: '14dd1bff-3295-4649-a919-3fc6ad57f627', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {    
			sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'    
		} 
	}
}
