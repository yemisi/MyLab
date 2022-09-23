pipeline{
    //Directives
    agent any
    tools {
        maven 'maven-3.8.6'
    }
    environment {
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // // Stage3 : Publish the artifact to Nexus
        // stage ('Publish to Nexus'){
        //     steps {
        //         nexusArtifactUploader artifacts:
        //         [[artifactId: 'YemiDevOpsLab', 
        //         classifier: '', 
        //         file: 'target/YemiDevOpsLab-0.0.1-SNAPSHOT.war', 
        //         type: 'war']], 
        //         credentialsId: '876d2b6b-b5b1-4d33-b853-909f5f657b6d', 
        //         groupId: 'com.yemisdevopslab', 
        //         nexusUrl: '172.20.10.131:8081', 
        //         nexusVersion: 'nexus3', 
        //         protocol: 'http', 
        //         repository: 'YemisDevOpsLab-SNAPSHOT', 
        //         version: '0.0.1-SNAPSHOT'
        //     }
        // }

        // Stage3 : Publish the artifact to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts:
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: 'target/${ArtifactId}-${Version}.war', 
                type: 'war']], 
                credentialsId: '876d2b6b-b5b1-4d33-b853-909f5f657b6d', 
                groupId: '${GroupId}', 
                nexusUrl: '172.20.10.131:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'YemisDevOpsLab-SNAPSHOT', 
                version: '${Version}'
            }
        }

        // Stage 4 : Print Environment variables
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }
        // // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo ' Source code published to Sonarqube for SCA......'
        //         withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //              sh 'mvn sonar:sonar'
        //         }

        //     }
        // }
 
    }

}