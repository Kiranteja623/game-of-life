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
                    sh "mvn clean install"
          }
        }
          }
}
