pipeline {
	agent any
	
	environment {
		LANG='en_US.UTF-8'
		LC_ALL='en_US.UTF-8'
	}
	tools {
	maven 'Maven'
	}
	
	stages {
		stage('Checkout') {
			steps {
				git branch: 'main', url: 'https://github.com/SaiHarithK/t6.git'
			}
		}
		stage('build') {
			steps {
				sh 'mvn clean package'
			}
		}
		
		stage('Archive') {
			steps {
				archiveArtifacts artifacts: 'target/*.war', fingerprint: true
			}
		}
		stage('Check WAR') {
    steps {
        sh 'ls -l target'
    }
}
		
		stage('Deploy') {
			steps {
				
				sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
			}
		}
	}
}
