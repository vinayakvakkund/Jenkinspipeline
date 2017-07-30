node {
 def server = Artifactory.server "Artifactory"
    // Create an Artifactory Maven instance.
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo
	def descriptor = Artifactory.mavenDescriptor()
	
stage('Test')
 {
    echo "printing name '${name}'"
	echo "check out git"
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '4ce69453-07f9-4599-8432-c523e5db4333', url: 'https://github.com/vinayakvakkund/FirstApp.git']]])
 }
 
 stage('Artifactory configuration') {
        // Tool name from Jenkins configuration
        rtMaven.tool = "MyMaven"
		descriptor.setVersion "the.group.id:the.artifact.id", "1.0.1"
		descriptor.transform()
        // Set Artifactory repositories for dependencies resolution and artifacts deployment.
        rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
        rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
    }
 
stage('Compile') 
 {
 echo "printing name '${name}'"
 buildInfo = rtMaven.run pom: 'SpringMVC/pom.xml', goals: 'clean install -Dbuild.number=${BUILD_NUMBER}'
 //buildInfo=bat 'mvn -f SpringMVC/pom.xml clean install'
 }
 stage('Publish build info') {
         
        server.publishBuildInfo buildInfo
    }
 }