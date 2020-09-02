pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    tools {
        maven 'M2_HOME'
    }
    
   

    stages {
        
       stage('build') {
            steps {
                echo 'Hello build'
                sh 'mvn clean'
                sh  'mvn install'
                sh 'mvn package'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test'
                
            }
        }
        stage ('build and publish image') {
      steps {
        script {
          checkout scm
          docker.withRegistry('', 'dockerID') {
          def customImage = docker.build("galegson/holi-pipeline:${env.BUILD_ID}")
          customImage.push()
          }
    }
        
    }
}
        stage ( 'deployment trigger') {
            steps {
                build 'hol-CD'
            }
        }        
}
}
