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
                      sudo cp /home/ec2-user/jenkins/workspace/demo/target/*.war /var/lib/tomcat10/webapps/
                  """
                dir("/var/lib/tomcat10/webapps/"){
                   sh"jar -xvf .war"
              }
            }
        }

    }
}
