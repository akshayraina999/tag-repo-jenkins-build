pipeline {
  agent any
  stages {
    stage ("Deploy 1") {
      when { tag "dev-*" }
      steps {
        echo "hello world 2"
      }
    }

    stage ("Deploy 2") {
      when { tag "release-*" }
      steps {
        echo "new release 1"
      }
    }
 }
}


