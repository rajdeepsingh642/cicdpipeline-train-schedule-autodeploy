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
        stage('build docker image and tag') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-hub') {
                    sh "docker build -t rajdeepsingh642/train-schedule-app:latest ."
                    
                       }
                }
             
            }
        }
            
             stage('Docker image push') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-hub') {
                    sh "docker push rajdeepsingh642/train-schedule-app:latest"
                    
                       }
                }
             
            }
             }
    
              stage('DeployToProduction') {
                steps{
                    withKubeConfig(caCertificate: '', clusterName: ' kubernetes', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://192.168.177.132:6443') {
                sh "kubectl apply -f train-schedule-kube-canary.yml"
                sh "kubectl apply -f train-schedule-kube.yml"
               }
           
            }
        }
           
                }
        }
    

    
 
