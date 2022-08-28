node {
  def commit_id
  stage('Preparation') {
    checkout scm
    sh "git rev-parse --short HEAD > .git/commit-id"
    commit_id = readFile('.git/commit-id').trim()
    commit_id = "dddf480"
  }
  stage('Deploy') {
    def image
    docker.withRegistry("https://116927014662.dkr.ecr.ap-northeast-2.amazonaws.com", "ecr:ap-northeast-2:ecr") {
      image = docker.image("helloworld:${commit_id}")
      image.pull()
    }
    sshagent(['ecr']){
      sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-79-235-250.ap-northeast-2.compute.amazonaws.com 'docker run helloworld:${image.imageName()}'"
    }
  }

}