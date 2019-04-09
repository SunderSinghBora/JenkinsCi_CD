node {
    
    
    stage('checkout') {
    
    git 'https://github.com/SunderSinghBora/JenkinsCi_CD.git'
}
        
        stage('Build'){
            
            bat label: '', script: 'mvn clean verify'
        }
        
        stage('Archive'){
            
            archiveArtifacts artifacts: 'target/*.?ar',
										onlyIfSuccessful: true
        }
        
		stage('Tests'){
		
			step([
    			    $class: 'JUnitResultArchiver',
    			    testResults: 'target\\surefire-reports/TEST-*.xml'
			    ])
		}
		
		stage('Notification'){
		
			emailext body: 'Test Complete', subject: 'Test Complete', to: 'sunder.bora@nagarro.com'
		}
		
		stage('Codecoverage'){
			
			publishHTML([
			                allowMissing: true,
			                alwaysLinkToLastBuild: false,
			                keepAll: true,
			                reportDir: 'target\\site\\jacoco',
			                reportFiles: 'index.html',
			                reportName: 'HTML Report',
			                reportTitles: ''
			         ])
		}
	
}
