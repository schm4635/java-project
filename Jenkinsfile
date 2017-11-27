properties([pipelineTriggers(githubPush()])])

node('linux') {
  stage('Unit Tests') {
      git 'https://github.com/schm4635/java-project.git'
      sh 'ant -buildfile test.xml'
  }
  stage('Build') {
      sh 'ant -f build.xml -v'
  }
  stage('Deploy') {
      
  stage('Report') {
      junit 'env'
  }
}
