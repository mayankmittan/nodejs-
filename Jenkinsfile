pipeline {

agent any

tools {nodejs 'nodejs'}

stages {

stage('Checkout') {

steps {

git branch: 'master',

credentialsId: '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',

url: "https://github.com/mittanmayank/nodejs.git"

}

}

stage('Install') {

steps {

sh 'npm install'

}

}



stage('Sonar Analysis') {
environment {
SCANNER_HOME = tool 'sonar'
PROJECT_NAME = "nodejs"
}
steps {
withSonarQubeEnv('my_sonar') {
sh '''$SCANNER_HOME/bin/sonar-scanner \
-Dsonar.java.binaries=build/classes/java/ \
-Dsonar.projectKey=$PROJECT_NAME \
-Dsonar.sources=.'''
}
}
}


stage('Build') {

steps {

sh 'npm run-script build'

}

}

stage('Deploy') {

steps {

sh 'npm start &
sleep 1
echo $! > .pidfile
set +x'

}

}

}

}
