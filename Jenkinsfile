@Library('bshprac') _
pipeline {
    agent any
    // environment
    // {
    //     SONARSERVER = 'sonar2'
    //     SONARSCANNER = 'sonarscanner'
    // }
    
    stages {
        stage('Github Pull')
         {
             steps{
             
                // Get some code from a GitHub repository
                git 'https://github.com/jenkinsci/JenkinsPipelineUnit'

             } 
         }
            // stage('gradle init')
            // {
            //     steps{
            //         //sh "./gradlew init"
            //         script{
            //         init()
            //         }
            //     }
            // }
            stage('gradle build')
            {
                steps{
                    //sh "./gradlew build"
                    script{
                    build()
                }}
            }
            stage("gradle test")
            {
                steps{
                //sh "./gradlew test"
                script{
                test()}
            }
        }
        
    
       stage('SonarQube analysis')
       {
        git 'https://github.com/Sanky2024/vprciproject.git'
  
        steps
        {
            withSonarQubeEnv('sonar2')
    { // Will pick the global server connection you have configured
      sh './gradlew sonarqube'
    }
        }
    
  }
        stage('publish')
        {
            steps{
                sh './gradlew publish'
            }
        }
    }
}
