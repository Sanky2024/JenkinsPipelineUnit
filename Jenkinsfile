@Library('bshprac') _
pipeline {
    agent any

    
    stages {
        stage('Github Pull')
         {
             steps{
             
                // Get some code from a GitHub repository
                git 'https://github.com/jenkinsci/JenkinsPipelineUnit'

             } 
         }
            stage('gradle init')
            {
                steps{
                    //sh "./gradlew init"
                    script{
                    init()
                    }
                }
            }
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
        stage('publish')
        {
            steps{
                sh './gradlew publish'
            }
        }
    }
}
