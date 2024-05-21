pipeline {
    agent any
    tools{
        jdk "jdk17"
        gradle "gradle"
    }
    stages {
        stage('git checkout') {
            steps {
             git 'https://github.com/rajdeepsingh642/cicdpipeline-train-schedule-autodeploy.git'   
            }
        } 
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
      
      
      }
        
           
        }
    }

    
 
