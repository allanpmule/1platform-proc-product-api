pipeline {
  agent {
    node {
      label 'ecs-cluster'
    }

  }
  stages {
    stage('Preparation') {
      steps {
        git(changelog: true, url: 'git@github.com:mulesoft-consulting/1platform-proc-product-api.git', branch: 'develop', credentialsId: '40094f04-235d-4342-8fa9-6bc6a368b8d9')
      }
    }
    stage('Build Development') {
      steps {
        sh 'sh \'mvn -B -DskipTests clean package\''
      }
    }
    stage('test') {
      steps {
        sh 'sh \'mvn test\''
      }
    }
    stage('Deployment Development') {
      steps {
        sh 'sh "mvn -V -e -DskipTests deploy -DmuleDeploy -Dmule.version=\'$MULE_VERSION\' -Danypoint.username=$CLOUDHUB_CRED_USR -Danypoint.password=$CLOUDHUB_CRED_PSW -Dcloudhub.app=\'$DEPLOY_NAME\' -Dcloudhub.environment=\'$ENV\' -Denv.ANYPOINT_CLIENT_ID=$ANYPOINT_CRED_USR -Denv.ANYPOINT_CLIENT_SECRET=$ANYPOINT_CRED_PSW -Dcloudhub.bg=\'$BG\' -Dcloudhub.worker=$WORKER"'
      }
    }
  }
  environment {
    cloudhub = 'credentials'
  }
}