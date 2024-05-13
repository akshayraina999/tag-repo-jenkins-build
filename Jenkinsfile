pipeline {
  agent any

  triggers {
        githubPush()
  }

  stages {
    stage ("Deploy 1") {
      when { tag "dev-*" }
      steps {
        echo "hello world 6"
      }
    }

    stage ("Deploy 2") {
      when { tag "release-*" }
      steps {
        echo "new release 2"
      }
    }
 }
}


