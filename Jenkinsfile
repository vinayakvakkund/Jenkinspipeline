node {

stage('Test')
 {
    echo "printing name '${name}'"
	echo "check out git"
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '4ce69453-07f9-4599-8432-c523e5db4333', url: 'https://github.com/vinayakvakkund/FirstApp.git']]])
 }
stage('Compile') 
 {
 echo "printing name '${name}'"
 bat 'mvn -f SpringMVC/pom.xml clean install'
 }
 }