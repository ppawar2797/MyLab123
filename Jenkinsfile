pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    // Adding Environment Directive.
    environment{
        ArtifactId = readMavenPom.getArtifactId()
        Version = readMavenPom.getVersion()
        Name = readMavenPom.getName()
        GroupId = readMavenPom.getGroupId()
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

        //Stage3 : Publish to Nexus
        stage ('Publish to Nexus'){
            steps{
                nexusArtifactUploader artifacts:
                [[artifactId: 'VinayDevOpsLab',
                classifier: '',
                file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war',
                type: 'war']], 
                credentialsId: 'e93fc5ac-e369-4472-be45-c42de54b359e',
                groupId: 'com.vinaysdevopslab', 
                nexusUrl: '172.20.10.145:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'VinaysDevOpsLab-SNAPSHOT', 
                version: '0.0.4-SNAPSHOT'
            }
        }
        
        //Stage 4 : Print Environment Variables
        stage ('Print Environment variables') {
            steps {
                echo "Artifact Id is '${ArtifactId}'"
                echo "Version  is '${ArtifactId}'"
                echo "GroupId is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }

        //Stage 5
        stage ('Deploy'){
            steps {
                echo 'Deploying......'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
   //     stage ('Sonarqube Analysis'){
    //        steps {
    //            echo ' Source code published to Sonarqube for SCA......'
    //            withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
     //                sh 'mvn sonar:sonar'
    //            }

    //        }
    //    }

        
        
    }

}
