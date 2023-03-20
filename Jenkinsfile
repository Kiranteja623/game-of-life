pipeline {
  agent { node { label "ubuntu"} }
     stages  { 
       stage ('vcs') { 
         steps { 
             git url: "https://github.com/Kiranteja623/game-of-life.git",
                 branch: "master"
               }
                    }
        stage ('build the package') { 
          steps { 
                    sh "mvn install"
          }
        }
        stage ('jfrog') { 
          steps {
          rtServer (
                    id: "JFROG_CLOUD",
                    url: 'https://kiranteja.jfrog.io/artifactory',
                    credentialsId: 'JFROG_CLOUD'
                )
                rtMavenDeployer (
                    id: "JFROG_CLOUD",
                    serverId: "JFROG_CLOUD_ADMIN",
                    releaseRepo: 'libs-release',
                    snapshotRepo: 'libs-snapshot'
                )

                rtMavenResolver (
                    id: "JFROG_CLOUD",
                    serverId: "JFROG_CLOUD_ADMIN",
                    releaseRepo: 'libs-release',
                    snapshotRepo: 'libs-snapshot'
                )
        }
      }
      stage ('maven deploy') {
        steps {
                  sh "mvn install"
                  rtMavenRun (
                      tool: 'maven_3.6.3',
                      pom: 'pom.xml',
                      goals: 'clean install',
                      deployerId: "JFROG_CLOUD"
                  )
        }
      }
      stage('package') {
        steps {
                sh "mvn clean install"
                rtPublishBuildInfo (
                    serverId: "JFROG_CLOUD_ADMIN"
                )
          
            }
      }
        }
          }
