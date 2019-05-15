node('linux') {   
	stage('Create Test Stack') {
		//def dockerIP = sh returnStdout: true, script:"aws ec2 describe-instances --region us-east-1 | jq '.Reservations[].Instances[] |  select(.State.Name==\"running\").PublicIpAddress'"
		//def output = sh returnStdout: true, script: "aws ec2 describe-instances --region us-east-1 | jq '.Reservations[].Instances[] |  select(.State.Name==\"running\").PublicIpAddress'"

		sh 'aws cloudformation create-stack --region us-east-1 --stack-name final-test --template-body file://docker-single-server.json --parameters ParameterKey=KeyName,ParameterValue=SEIS665-02-Spring2019-VA ParameterKey=YourIp,ParameterValue=3.86.103.132/32'
				
		//wait for the stack-create-complete
		sh 'aws cloudformation wait stack-update-complete --stack-name final_test --region us-east-1'
				
		//describe the final-test stack
		sh 'aws cloudformation describe-stacks  --stack-name final_test --region us-east-1'
		
		sshagent(['eba62a9a-3dc3-43f0-8bfc-94a5b168d766']) {
			
			sh '''
		       dockerIP=$(returnStdout: true, script:"aws ec2 describe-instances --region us-east-1 | jq '.Reservations[].Instances[] |  select(.State.Name==\"running\").PublicIpAddress'")
			   ssh -o StrictHostKeyChecking=no ubuntu@$dockerIP uptime			
			'''		
			
		}		
	}
}
