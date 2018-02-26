pipeline {
	agent any
	
	stages {
		stage('build'){
			steps {
				echo "building"
			}
		}
		stage('test'){
			steps{
				echo "testing"
			}
		}
		stage('deploy'){
			steps{
				echo "deploy"
				sh "git clone git@github.com:Dszordan/JenkinsPluginsTest.git"
				sh "tar -czf ../artifact.tar.gz -C $WORKSPACE/JenkinsPluginsTest . --exclude=.git* --exclude=Jenkins*"
				sh "ssh deployer@10.0.1.5 -i ~/.ssh/deploykey mkdir /var/www/html/dev/$BUILD_NUMBER"
				sh "scp -i ~/.ssh/deploykey ../artifact.tar.gz deployer@10.0.1.5:/var/www/html/dev/$BUILD_NUMBER"
				sh "ssh deployer@10.0.1.5 -i ~/.ssh/deploykey tar -xzvf /var/www/html/dev/$BUILD_NUMBER/artifact.tar.gz -C /var/www/html/dev/$BUILD_NUMBER/"
				sh "ssh deployer@10.0.1.5 -i ~/.ssh/deploykey rm /var/www/html/dev/$BUILD_NUMBER/artifact.tar.gz"
				sh "rm -rf JenkinsPluginsTest"
			}
		}
	}
}