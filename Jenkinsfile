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
                    sh '''s3Upload(file:'spring-boot-rest-example-0.5.0.war', bucket:'pratyush-bucket', path:'/var/lib/jenkins/workspace/buildPipeline/target/spring-boot-rest-example-0.5.0.war
')'''
                }
            }
        }
    }
}    

