pipeline{
    agent {
        label 'MAVEN'
    }
     parameters {
        choice choices: ['main', 'first_release'], description: 'Pick the branch', name: 'Select_Branch'
        string defaultValue: 'package', description: 'Choose the Maven Goal', name: 'Select_MavenGoal'
    }
    stages{
        stage('git_clone'){
            steps{
                git branch: "${params.SELECT_BRANCH}", url: 'https://github.com/annem-sriram/openmrs-core.git'
            }
        }
        stage('build'){
        steps{
            sh "mvn ${params.Select_MavenGoal}"
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