pipeline{
    agent {
        label 'MAVEN'
    }
    stages{
        stage('git_clone'){
            steps{
                git branch: 'first_rel', url: 'https://github.com/annem-sriram/openmrs-core.git'
            }
        }
        stage('build'){
        steps{
            sh 'mvn clean package'
            }
        }
        stage('archive-artifacts'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
        stage('unit-tests'){
            steps{
                junit '**/*.xml'
            }
        }
    }
}