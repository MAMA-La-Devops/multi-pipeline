pipeline {
    agent any
    options {
        timestamps()
        }
    tools {
        maven "maven3.8.6"
    }
    stages {
        stage(‘1SCM’){
            steps{
                sh 'echo "apps latest version committed"'
                 git credentialsId: 'github-credentials', url: 'https://github.com/MAMA-La-Devops/multi-pipeline'
            }
        }
        stage(‘2Build’){
            steps {
                sh "mvn clean install"
                }
            }
        
        stage(‘3QualityTest’){
            steps {
                sh "echo 'quality test'"
                sh "mvn sonar:sonar"
                }
            }
        stage(‘4UploadArtifacts’){
            steps {
                sh "echo 'Artifactory'"
                sh "mvn deploy"
                }
            }
        
        
         stage(‘UATDeploy’){
            steps {
                sh "echo 'deploy to tomcat'"
                deploy adapters: [tomcat9(credentialsId: 'tomcatcredentials', path: '', url: 'http://52.16.87.175:8080/')], contextPath: null, war: 'target/*.war'
                } 
            } 
        
        }
    }
