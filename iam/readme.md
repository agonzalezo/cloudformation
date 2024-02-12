## Manage stacks
aws cloudformation list-stacks --output text
aws cloudformation delete-stack --stack-name iam-user
aws cloudformation create-stack --stack-name iam-user --template-body file://newUser.yml
#

aws cloudformation deploy --stack-name iam-user --template-file newUser.yml --parameter-overrides UserName=user01 GroupName=group01