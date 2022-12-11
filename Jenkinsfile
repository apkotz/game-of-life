pipeline {
			agent {
					label {
								label "Node-1"
								customWorkspace "/home/ec2-user/mnt"
						}
			}
			
			environment  {
					serverhome = "/home/ec2-user/servers/apache-tomcat-9.0.67"
			}
			
			tools {
					 maven "maven-3.8.6"
			}

			stages {
								
					stage ("build"){
					
						steps {
								sh "cd game-of-life && mvn clean install"
								
						}
						
					}
					stage ("install tomcat"){
					
						steps {
								sh "mkdir /home/ec2-user/mnt/servers"
								sh "cd /home/ec2-user/mnt/servers"
				
								sh "sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.70/bin/apache-tomcat-9.0.70.zip"
								sh "sudo unzip apache-tomcat-9.0.70.zip"
			
								
								
						}
						
					}
					
					stage ("deploy"){
						
						steps {
						
							sh "cp -r game-of-life/gameoflife-web/target/gameoflife.war $serverhome/webapps"
															
						}
					
					}
					
					stage ("start-server"){
						
						steps {
						
							sh "cd $serverhome/bin && ./startup.sh && tail -100f ../logs/catalina.out"
															
						}
					
					}
			
			}
}
