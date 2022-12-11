Pipeline {
		agent {
			label {
				label "built-in"
				customWorkspace "/mnt/projects"
			}
		}
		tools {
			maven "maven-3.8.6"
		}
		
		stages {
		stage('dependency install') {
			steps {
				sh " cd /mnt/projects/game-of-life/"
				sh " mvn clean install"
			}
		}
		stage ('deploy war on tomcat-node-1'){
			agent {
				label {
					label "Node-1"
					
				}
			}
			environment {
			serverhome = "/mnt/build-tools/apache-maven-3.8.6"
		}
		tools {
			maven "maven-3.8.6"
		}
			steps {
				
				sh "mkdir /mnt/projects"
				sh "cd /mnt/projects"
				
				sh "sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.70/bin/apache-tomcat-9.0.70.zip"
				sh "sudo unzip apache-tomcat-9.0.70.zip"
			
				sh "sudo /mnt/projects/apache-tomcat-9.0.70/bin/./startup.sh"
			}
		}
		
		stage('copy war to webapps'){
		agent {
			label {
				label "built-in"
			}
		}
		steps {
			
			sh "sudo scp -i /root/MyWs-1.pem /mnt/projects/gameoflife-web/target/gameoflife.war ec2-user@172.31.34.207"
			sh "sudo scp -i /root/MyWs-1.pem /mnt/projects/gameoflife-web/target/gameoflife.war ec2-user@172.31.43.114"
			
		
		}
		}
	
	}

}

