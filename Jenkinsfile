pipeline {
      agent {
	      label {
                      label 'built-in'
                    }
            }
         stages {
		 
		 stage ('node') {
			 agent {
				 label {
					 label "172.31.37.109"
				       }
			      }
			 steps {
				 sh "cd /mnt/jenkins-slave/"
				 sh "mkdir project"
				 sh "cd project"
				 sh "rm -rf *"
				 sh "wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.67/bin/apache-tomcat-9.0.67.zip "
				 sh "unzip apache-tomcat-9.0.67.zip"
				 sh "cd apache-tomcat-9.0.67/"
				 sh "chmod 777 *"
				 		 
				 				 
			       }
		 }   
		 stage ('mvn install') {
				agent {
				 label {
					 label "built-in"
				       }
			      }
			
					steps {
						sh "mvn install"
			      		      }
		                         }	
		stage ('copy file to node') {
			
					steps {
						sh "scp -i /root/MyWS-1.pem /root/.jenkins/workspace/GOL-Deploy/gameoflife-web/target/gameoflife.war ec2-user@172.31.37.109:/mnt/jenkins-slave/workspace/GOL-Deploy/apache-tomcat-9.0.67/webapps/"
					      }
					}
		
		 stage ('node-1') {
			 agent {
				 label {
					 label "172.31.37.109"
				       }
			      }
			 steps {
				 sh "cd /root"
				 sh "cd /mnt/jenkins-slave/project/apache-tomcat-9.0.67/bin/"
				 sh " chmod 777 *"
				 sh "./startup.sh"
				 
			       }
		 }
	 }
	
}

