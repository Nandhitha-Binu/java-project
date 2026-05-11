pipeline{
    agent {
        label "node1"
    }   
    tools{
        maven "maven123"
    }
    options{
         skipDefaultCheckout(true)
    }
    stages{
        stage("clone"){
            steps{
                checkout scm
            }
        }
        stage("build"){
            steps{
                echo "build stage"
                sh"mvn clean package"
            }
        }
        stage("deploy"){
            steps{
                echo "hello"
                sh"""
                      sudo cp target/*.war /var/lib/tomcat10/webapps/
                      
                      sudo systemctl restart tomcat10

                      sleep 10

                      sudo  cp -r /var/lib/tomcat10/webapps/java-tomcat-maven-example/* /var/lib/tomcat10/webapps/ROOT/

                  """
                   
              }
            }
        stage("cleanup"){
           steps{
               sh"""

                 sudo rm -rf /var/lib/tomcat10/webapps/java-tomcat-maven-example
                 sudo rm -rf /var/lib/tomcat10/webapps/java-tomcat-maven-example.war

                 sudo systemctl restart tomcat10
                """

              }
          }
