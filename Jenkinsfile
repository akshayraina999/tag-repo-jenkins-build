pipeline {
  agent any

  // environment {
  //       TAG_NAME = "${env.GIT_TAG_NAME}"
  //   }

  triggers {
        githubPush()
  }

  stages {
    
    stage('Checkout') {
            steps {
                script {
                    def tagPattern = ~/^refs\/tags\/(.*)$/ // Define a regex pattern to match tag names
                    def tagName = env.BRANCH_NAME =~ tagPattern ? tagPattern.matcher(env.BRANCH_NAME).replaceAll('$1') : null // Extract the tag name
                    echo "Tag name: ${tagName}"
                }
            }
        }
    // stage('Checkout') {
    //         steps {

    //           echo "${env.GIT_TAG_NAME}"
    //             // checkout([$class: 'GitSCM', 
    //             //           branches: [[name: "*/tags/${env.GIT_TAG_NAME}"]], 
    //             //           userRemoteConfigs: [[url: 'https://github.com/akshayraina999/tag-repo-jenkins-build.git']]])

    //             // checkout scm: [$class: 'GitSCM', userRemoteConfigs: [[url: 'https://github.com/akshayraina999/tag-repo-jenkins-build.git']], branches: [[name: "refs/tags/${env.GIT_TAG_NAME}"]]], poll: false
    //         }
    //     }
    stage ("Deploy 1") {
      when { tag "dev-*" }
        steps {
	         script {
            sh "docker build -t test:${env.GIT_TAG_NAME} ."
	         }
        }
    }
    stage ("Deploy 2") {
      when { tag "release-*" }
        steps {
          echo "new release 3"
        } 
      }
  }
}


