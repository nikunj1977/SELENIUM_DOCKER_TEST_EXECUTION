pipeline{
	agent any
	stages{
		stage("PULL LATEST IMAGE"){
			steps{
				echo 'STEP_1 --> PULLING LATES IMAGE FROM DOCKERHUB...'	
				bat "docker pull nbtest011/seleniumdocker_latest"
			}
		}
		stage("STARTING SELENIUM GRID"){
			steps{
				echo 'STEP_2 --> STARTING HUB TO TRIGGER CHROME AND FIREFOX BROWSERS...'
				bat "docker-compose up -d hub chrome firefox"
			}
		}
		stage("TEST EXECUTION"){
			steps{
				echo 'STEP_3 --> RUNNING TESTS...'
				bat "docker-compose up search-module-Firefox search-module-Chrome"
			}
		}
	}
	post{
		always{
			echo 'STEP_4 --> ARCHIVING TEST RESULTS...'
			archiveArtifacts artifacts: 'output/**'
			echo 'STEP_5 --> KILLIING OFF ALL RUNNING CONTAINERS...'
			bat "docker-compose down"
		}
	}
}