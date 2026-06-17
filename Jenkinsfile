pipeline {
	agent any
	environment {
    LANG = 'en_US.UTF-8'
    LC_ALL = 'en_US.UTF-8'
}
	
	tools{
		maven 'Maven'
		
		}
		
		stages{
			stage('Checkout')
			{
			steps{
				git branch:'main',url:'https://github.com/prasadmv-collab/anex.git'
				}
			}
			
			stage('Build')
			{
			steps{
				sh 'mvn clean install'
				}
			}
			
			stage('Test')
			{
			steps{
			sh 'mvn test'
			}
			}
			
			stage('archive')
			{
			steps{
				archiveArtifacts artifacts: 'target/*.war',
				fingerprint:true
				}
			}
			
			stage('Deploy')
			{
			steps{
				sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
			}
			}
			
			}
			
			post{
			
			success{
			echo 'Build successfull'
			}
			failure{
			echo 'Build failure'
			}
			}
			}
