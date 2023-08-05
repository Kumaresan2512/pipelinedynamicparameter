def parameters = [
  "parameter1": "default value 1",
  "parameter2": "default value 2"
]

pipeline {
  agent any
  stages {
    stage("Set parameters") {
      steps {
        withEnv(parameters) {
          echo "Parameter 1: ${params.parameter1}"
          echo "Parameter 2: ${params.parameter2}"
        }
      }
    }
  }
}
