pipeline {
    agent any
    tools { 
        maven 'MAVEN_HOME' 
        jdk 'JAVA_HOME' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

         stage ('GIT CHECKOUT') {
            steps {
                
                   git(
                     url: 'https://github.com/nishant260393/mvn_sonar.git',
                     credentialsId: 'nishant260393@gmail.com',
    )


            }
        }
		 
		 stage('Build') {
        steps {
            withSonarQubeEnv('sonar') {
                sh '/opt/maven/bin/mvn clean verify sonar:sonar'
            }
        }
    }
    stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
		 
        stage ('Deploy') {
            steps {
                sh '''
				    
                    mvn clean install
                    echo "BUILD SUCCESSFULL"
                ''' 
            }
        }
    }
	
}
