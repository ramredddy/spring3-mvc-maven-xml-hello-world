pipeline {
    agent any

    tools {
        maven "maven3"
    }

    stages {
        stage('scm') {
            steps {
                git credentialsId: 'github_credentials', url: 'https://github.com/jmstechhome17/spring3-mvc-maven-xml-hello-world.git'
            }
        }
		stage('build') {
		   steps{
		     sh 'mvn package'
		   }
		}
		stage('deploy') {
		 steps {
		 
		  withCredentials([usernameColonPassword(credentialsId: 'tomcat_credentails', variable: 'tomcat_credentails')]) {
		 		    sh "curl -v -u $tomcat_credentails -T /var/lib/jenkins/workspace/git-jenkins-maven-tomcat/target/spring3-mvc-maven-xml-hello-world-1.2.war 'http://15.206.79.124:8081/manager/text/deploy?path=/pipeline_spring&update=true'"

                    }

		 }
		}
    }
}
