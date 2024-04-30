pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('pmd') {
      steps {
        sh 'mvn pmd:pmd'
      }
    }
   stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }
     stage('Generate Reports') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }
    stage('Javadoc') {
            steps {
                sh 'mvn javadoc:javadoc javadoc:jar'
            }
        }
  }
post {
  always {
    archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true
  }
}
}
