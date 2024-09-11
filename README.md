

aws cloudformation deploy \
      --stack-name MyVPC \
      --capabilities CAPABILITY_NAMED_IAM \
      --template-file cloud-dev-assessment-01.yaml


aws ssm start-session \
    --target i-059b5ee5d5cb7dc9e \
    --document-name AWS-StartPortForwardingSessionToRemoteHost \
    --parameters host="192.168.60.32",portNumber="80",localPortNumber="8080"

aws ssm start-session \
    --target i-059b5ee5d5cb7dc9e \
    --document-name AWS-StartPortForwardingSessionToRemoteHost \
    --parameters host="192.168.60.169",portNumber="80",localPortNumber="8090"

aws ssm start-session \
    --target i-059b5ee5d5cb7dc9e \
    --document-name AWS-StartPortForwardingSessionToRemoteHost \
    --parameters host="192.168.60.32",portNumber="22",localPortNumber="8081"

aws ssm start-session \
    --target i-059b5ee5d5cb7dc9e \
    --document-name AWS-StartPortForwardingSessionToRemoteHost \
    --parameters host="192.168.60.169",portNumber="22",localPortNumber="8091"


aws ssm start-session \
    --target i-059b5ee5d5cb7dc9e \
    --document-name AWS-StartPortForwardingSessionToRemoteHost \
    --parameters host="myvpc6-acg-rds-instance.cis0e5kajlrt.ap-southeast-1.rds.amazonaws.com",portNumber="3306",localPortNumber="8083"

aws ssm start-session \
    --target i-059b5ee5d5cb7dc9e \
    --document-name AWS-StartPortForwardingSessionToRemoteHost \
    --parameters host="myvpc6-acg-read-replica-rds-instance.cis0e5kajlrt.ap-southeast-1.rds.amazonaws.com",portNumber="3306",localPortNumber="8093"

