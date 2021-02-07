pipeline {
  agent any
  stages {
    stage('CODE') {
      steps {
        echo 'Pull maven project from git'
        git(url: 'https://github.com/dinesh99088/offers', branch: 'master', changelog: true, poll: true)
        echo 'Run the maven compile command'
        sh 'mvn compile'
      }
    }

    stage('TEST') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

    stage('validate') {
      steps {
        fileExists '*jar'
      }
    }

    stage('Artifacts') {
      steps {
        archiveArtifacts(artifacts: '*jar', allowEmptyArchive: true, caseSensitive: true, followSymlinks: true, onlyIfSuccessful: true, defaultExcludes: true, fingerprint: true)
      }
    }

  }
}