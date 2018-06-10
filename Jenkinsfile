pipeline {
    agent any
    tools{
        jdk 'java8'
        maven 'Maven'
    }
    stages {
        stage('Initialize'){
           steps { 
               echo "Initializing the build process"
               sh ''' 
                    echo "PATH=${PATH}"
                    echo "M2_HOME=${M2_HOME}"
               '''
        }
        }
        stage('Build Process Start'){
          steps{ 
              echo('Build Process Complete')
              sh 'mvn clean package checkstyle:checkstyle'
            
            post {
                success{               
                echo "Generate Checkstyle Report"
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
                echo "Generate Junit Report"
                junit '**/target/surefire-reports/*.xml'
                echo "Archive Artifact"
                archiveArtifacts '**/*.war'
            }}

          }
        }
        stage('Deploy to staging'){
           steps{
                echo "Build complete"
                build 'Staging-Deployment'
           }
        }   
         }

    
}