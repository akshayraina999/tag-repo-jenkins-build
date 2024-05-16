def config = readYaml file: 'config.yaml'

pipeline {
  agent any

  // environment {
  //       TAG_NAME = "${env.GIT_TAG_NAME}"
  //   }

  parameters {
        string(name: 'GIT_REPO_URL', description: 'URL of the Git repository', defaultValue: config.GIT_REPO_URL)
        string(name: 'DOCKER_IMAGE_NAME', description: 'Name of the Docker image to build', defaultValue: config.DOCKER_IMAGE_NAME)
    }


  triggers {
        githubPush()
  }


  stages {
    
    stage('Checkout') {
            steps {
                script {
                    def tag = sh(returnStdout: true, script: 'git describe --tags --abbrev=0').trim()
                    echo "Tag name: ${tag}"
                    checkout scm: [$class: 'GitSCM', userRemoteConfigs: [[url: "${params.GIT_REPO_URL}"]], branches: [[name: "refs/tags/${tag}"]]], poll: false
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

    stage("Build and Deploy") {
      when { tag "dev-*" }
            steps {
                script {
                    def tag = sh(returnStdout: true, script: 'git describe --tags --abbrev=0').trim()
                    sh "docker build -t ${params.DOCKER_IMAGE_NAME}:${tag} ."
                    // Additional deployment steps can be added here
                }
            }
        }

    // stage("Deploy 1") {
    //         when { tag "dev-*" }
    //         steps {
    //             script {
    //                 def tag = sh(returnStdout: true, script: 'git describe --tags --abbrev=0').trim()
    //                 sh "docker build -t test:${tag} ."
    //             }
    //         }
    //     }
        
    stage ("Deploy 2") {
      when { tag "release-*" }
        steps {
          echo "new release 3"
        } 
      }
  }
}


