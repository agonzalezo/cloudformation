## Manage stacks
aws cloudformation list-stacks --output text
aws cloudformation create-stack --stack-name ec2-04 --template-body file://template-ec2.yml
aws cloudformation delete-stack --stack-name webserver
aws cloudformation delete-stack --stack-name netsys-vpc
#

aws cloudformation deploy --stack-name ec2-04 --template-file template-ec2.yml --parameter-overrides KeyPairParameter=keypair-pruebas-cf VpcIdParameter=vpc-04e74c746436e103a AmiIdParameter=ami-052efd3df9dad4825 Environment=prod

aws cloudformation deploy --stack-name netsys-vpc --parameter-overrides EnvironmentName=DEV1 --template-file Infra/vpc.yml

aws cloudformation deploy --stack-name webserver --template-file Infra/ec2-public.yml --parameter-overrides EnvironmentName=DEV1

aws cloudformation deploy --stack-name ec2-private --template-file Infra/ec2-private.yml --parameter-overrides EnvironmentName=DEV1