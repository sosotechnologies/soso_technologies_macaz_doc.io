```Jenkinsfile
pipeline {
    agent any
    tools {
	    maven "SOSOMAVEN3"
	    jdk "SosoJDK8"
	}

    environment {
        JenkinsECRCredential = 'ecr:us-east-1:sosoawstoken'
        sosoappRegistry = "088789840359.dkr.ecr.us-east-1.amazonaws.com/soso-repository"
        sosotechRegistry = "https://088789840359.dkr.ecr.us-east-1.amazonaws.com"
    }

    stages{
        stage('Fetch code') {
          steps{
              git branch: 'master', url:'https://github.com/sosotechnologies/jenkins-ecr-cicd-pipeline.git'
          }  
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }

        }

        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }

        stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'sososonar4.7'
            }
            steps {
               withSonarQubeEnv('sososonar') {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=sosotech \
                   -Dsonar.projectName=sosotech \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              }
            }
        }

        stage("Quality Gate") {
        steps {
            timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
            }
        }
    }

    stage('Build App Image') {
      steps {
       
        script {
            dockerImage = docker.build( sosoappRegistry + ":$BUILD_NUMBER", "./sosotech-Dockerfiles/sosoapp/multistagebuild/")
             }

     }
    
    }

    stage('Upload App Image') {
          steps{
            script {
              docker.withRegistry( sosotechRegistry, JenkinsECRCredential ) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
          }
     }

  }
}
```

kubectl version --short --client
