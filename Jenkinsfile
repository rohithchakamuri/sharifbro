pipeline{
    environment { 
        registry = "akanshagiriya/docker-jenkins-integration-sample" 
        registryCredential = 'e708ae51-1ee3-4c9f-b4ea-83806b26e462'
        dockerImage = ''
    }
    agent any
        stages{
            stage('build'){
                steps{
                    sh 'mvn install'
                }
            }

            stage('Building our image') { 
                steps { 
                    script { 
                        dockerImage = docker.build registry 
                    }
                }
            }

            stage('pushing the image to docker hub'){
                steps { 
                    script { 
                        docker.withRegistry( '', registryCredential ) { 
                            dockerImage.push() 
                        }
                    } 
                }   
            }

             stage('Sonar Integration') {
                steps{
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=Sonarqube-Practice \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=bb2cf27ac2d543689832762e0f2fbf091cff5167
                    '''
                } 
            }





        }
}
