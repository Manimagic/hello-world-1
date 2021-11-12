node{
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/ravdy/hello-world.git'
            }
        }
        stage("Maven Clean Build"){
            def mavenHome = tool name:"Maven-3.6.1", type:"maven"
            def mavenCMD = "${mavenHome}/bin/mvn "
            sh "${mavenCMD} clean package"
        }
        stage("deploy"){
            steps{
              sshagent(['deploy_user']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@13.229.183.126:/opt/apache-tomcat-8.5.55/webapps"
                 
                }
            }
        }
     }
