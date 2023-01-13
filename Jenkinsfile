pipeline {
    agent {
	    label "OPENJDK-17-MVN-3.6.3"
	}
    stages {
        stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/annem-sriram/openmrs-core.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "SRI_JFROG",
                    releaseRepo: "devops-libs-release-local",
                    snapshotRepo: "devops-libs-snapshot-local"
                )

                
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN_3.6.3', 
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                    
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "SRI_JFROG"
                )
            }
        }
    }
}