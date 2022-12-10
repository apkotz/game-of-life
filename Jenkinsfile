Pipeline {
		agent {
			label {
				label "built-in"
				customWorkspace "/mnt/projects"
			}
		}
		stages {
		stage ('deploy war on tomcat-node-1'){
			agent {
				label {
					label "Node-1"
					
				}
			}
			steps {
				sh "sudo rm -rf /home/ec2-user/tomcat"
				sh "sudo mkdir /home/ec2-user/tomcat/"
				sh "sudo chown -R ec2-user:ec2-user /home/ec2-user/tomcat/"
				dir ("/home/ec2-user/tomcat/"){
					sh "sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.70/bin/apache-tomcat-9.0.70.zip"
					sh "sudo unzip apache-tomcat-9.0.70.zip"
				}
				sh "sudo /home/ec2-user/tomcat/apache-tomcat-9.0.70/bin/./startup.sh"
			}
		}
		stage ('deploy war on tomcat-node-2'){
			agent {
				label {
					label "Node-2"
					
				}
			}
			steps {
				sh "sudo rm -rf /home/ec2-user/tomcat"
				sh "sudo mkdir /home/ec2-user/tomcat/"
				sh "sudo chown -R ec2-user:ec2-user /home/ec2-user/tomcat/"
				dir ("/home/ec2-user/tomcat/"){
					sh "sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.70/bin/apache-tomcat-9.0.70.zip"
					sh "sudo unzip apache-tomcat-9.0.70.zip"
				}
				sh "sudo /home/ec2-user/tomcat/apache-tomcat-9.0.70/bin/./startup.sh"
			}
		}
		stage('copy war to webapps'){
		agent {
			label {
				label "built-in"
			}
		}
		steps {
			sh " cd /mnt/projects/gameoflife/"
			sh " mvn clean install"
			sh "sudo scp -i /root/MyWs-1.pem /mnt/projects/gameoflife-web/target/gameoflife.war ec2-user@172.31.34.207"
			sh "sudo scp -i /root/MyWs-1.pem /mnt/projects/gameoflife-web/target/gameoflife.war ec2-user@172.31.43.114"
			
		
		}
		}
	
	}

}
