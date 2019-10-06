pipeline {
    
    agent any
    
    stages{
        stage("git pull"){
            steps{
                script{
                    git branch: "master", changelog: false, url: "https://github.com/pratyushgarg15/spring-boot-rest-example.git" 
                }   
            }
        }
        stage("maven"){
            steps{
                script{
                    withMaven (maven: "maven-3.6.2")
                    {
                    sh(script:"""
                             mvn clean package
                    """)
                    }
                }
            }
        }
        stage("s3 upload"){
            steps{
                script{
                    withAWS(region:'us-east-1',credentials:'aws-key'){
                        s3Upload(bucket: 'pratyush-bucket', workingDir:'buildPipeline', includePathPattern:'**/*.war');

                    }
                }
            }
        }
    }
}    

