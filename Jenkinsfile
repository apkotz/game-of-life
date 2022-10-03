pipeline {
      agent {
	      label {
                      label 'built-in'
                    }
            }
         stages {
		 
		 stage ('mvn install') {
			
					steps {
						sh "mvn install"
			      		      }
		                         }	
		stage ('copy file to node') {
			
					steps {
						sh "scp -i /root/MyWS-1.pem /root/.jenkins/workspace/GOL-Deploy/game0flife ec2-user@172.31.37.109:/mnt/jenkins-slave/"
					      }
					}
		
		 stage ('node') {
			 agent {
				 label {
					 label "172.31.37.109"
				       }
			      }
			 steps {
				 sh "yum install httpd -y"
				 sh "service httpd start"
				 sh "cp /mnt/jenkins-slave/index.html /var/www/html/"
				 sh "chmod -R 777 /var/www/html/index.html"
			       }
		 }
	 }
	
}

