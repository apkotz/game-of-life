pipeline {
			agent {
					label {
								label "Node-1"
								customWorkspace "/home/ec2-user/projects"
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
