node {
  def commit_id
  stage('Preparation') {
    checkout scm
    sh "git rev-parse --short HEAD > .git/commit-id"
    commit_id = readFile('.git/commit-id').trim()
  }
  stage('test') {
    nodejs(nodeJSInstallationName: 'node16') {
      sh 'npm install --only=dev'
      sh 'npm test'
    }
  }
  stage('docker build/push') {
    docker.withRegistry('https://116927014662.dkr.ecr.ap-northeast-2.amazonaws.com/helloworld', 'ecr') {
      def app = docker.build("docker-nodejs-demo:${commit_id}", '.').push()
    }
  }
}