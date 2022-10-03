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
				 sh "wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.67/bin/apache-tomcat-9.0.67.zip "
				 sh "unzip apache-tomcat-9.0.67.zip"
				 sh "cd /apache-tomcat-9.0.67/"
				 sh "chmod 777 bin"
				 sh "cd bin"
				 
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
						sh "scp -i /root/MyWS-1.pem /root/.jenkins/workspace/GOL-Deploy/gameoflife-web/target/gameoflife.war ec2-user@172.31.37.109:/mnt/jenkins-slave/apache-tomcat-9.0.67/webapps"
					      }
					}
		
		 stage ('node') {
			 agent {
				 label {
					 label "172.31.37.109"
				       }
			      }
			 steps {
				 sh "cd /mnt//mnt/apache-tomcat-9.0.67/bin/"
				 sh "./startup.sh"
				 
			       }
		 }
	 }
	
}
