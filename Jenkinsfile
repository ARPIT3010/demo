pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Clean Build'
                bat 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                bat 'mvn test'
            }
        }
       
        stage('Package') {
            steps {
                echo 'Packaging'
                bat 'mvn package -DskipTests'
            }
        }
        
         stage('JaCoCo') {
            steps {
                echo 'Code Coverage'
                jacoco()
            }
        }
        stage("SonarQube analysis") {
            steps {
              withSonarQubeEnv('project-1') {
                  bat 'mvn sonar:sonar'
              }
            }
          }
        stage('Deploy') {
            steps {
                echo '## TODO DEPLOYMENT ##'
            }
        }
    }
    
    post {
        always {
            echo 'JENKINS PIPELINE'
            archiveArtifacts artifacts: 'target/jacoco.exec', onlyIfSuccessful: true
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
