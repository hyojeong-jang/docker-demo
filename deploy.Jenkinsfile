node {
  def commit_id
  stage('Preparation') {
    checkout scm
    sh "git rev-parse --short HEAD > .git/commit-id"
    commit_id = readFile('.git/commit-id').trim()
    commit_id = "dddf480"
  }
  stage('Deploy') {
    // def image
    // docker.withRegistry("https://116927014662.dkr.ecr.ap-northeast-2.amazonaws.com", "ecr:ap-northeast-2:ecr") {
    //   image = docker.image("helloworld:${commit_id}")
    //   image.pull()
    // }
    //     docker.withServer('tcp://ec2-13-125-33-73.ap-northeast-2.compute.amazonaws.com', 'docker') {
    //     docker.image('mysql:5').withRun('-p 3306:3306') {
    //         /* do things */
    //     }
    // }
    sshagent(credentials: ['ec2']){
      sh 'ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-79-235-250.ap-northeast-2.compute.amazonaws.com "whoami"'
      sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-79-235-250.ap-northeast-2.compute.amazonaws.com 'docker pull 116927014662.dkr.ecr.ap-northeast-2.amazonaws.com/helloworld:dddf480'"
      // sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-79-235-250.ap-northeast-2.compute.amazonaws.com 'docker run ${image.imageName()}'"
      sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-79-235-250.ap-northeast-2.compute.amazonaws.com 'docker run helloworld:dddf480'"
    }
  }
}
