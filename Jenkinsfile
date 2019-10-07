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
        stage("append build number"){
            steps{
                script{
                    sh ''' cd /var/lib/jenkins/workspace/build-deploy-pipeline/target/ '''
                    sh ''' ls '''
                    sh '''mv *.war spring-boot-rest-example-0.5.0-$BUILD_NUMBER.war '''
                }
            }
        }
        stage("s3 upload"){
            steps{
                script{
                    
                        s3Upload(bucket: 'pratyush-bucket', workingDir:'target', includePathPattern:'**/*.war');

                }
            }
        }
    }
}    

