@Library('bshprac') _
pipeline {
    agent any
    environment
    {
        SONARSERVER = 'sonar2'
        SONARSCANNER = 'sonarscanner'
    }
    
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
         stage('CODE ANALYSIS with SONARQUBE')
        {
          
		  environment 
          {
             scannerHome = tool "${SONARSCANNER}"
          }

          steps
        {
            withSonarQubeEnv("${SONARSERVER}") 
            {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=JenkinsPipelineUnit \
                   -Dsonar.projectName=JenkinsPipelineUnit \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                 
            }

            timeout(time: 10, unit: 'MINUTES')
            {
               waitForQualityGate abortPipeline: true
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
