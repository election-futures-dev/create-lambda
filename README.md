# create-lambda
Create AWS Lambda using AWS CLI

## Prerequisite
- [ ] Install [jq] to parse the json content into `CLI` 
```bash
brew install jq
```
- [ ] [Install AWS CLI v.2]
```bash
$ curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
$ sudo installer -pkg AWSCLIV2.pkg -target /
```

- [ ] [Configure your AWS credentials]
```bash
aws configure
``` 

## Steps to Create Lambda
- [ ] Create Role
```bash
# Declare role-name
role_name="lambda-allow-basic"    
# Read the ./allow-role-policy.json.
policy=$(cat ./allow-role-policy.json | jq)
# Create the AWS-IAM role with the name lambda-ex and the above read-in policy. role-name and policy can be customized.
aws iam create-role --role-name $(echo "$role_name") --assume-role-policy-document $policy  
```

- [ ] Zip the `index.js`
```bash
zip index.zip index.js
```

- [ ] Create `lambda`
```bash
# Declare function-name & runtime
func_name="this-is-test-lambda"
runtime="nodejs12.x"
# Creae lambda with the func_name. --role ARN must be changed with the one created from the first step.  
aws lambda create-function --function-name $(echo "$func_name") --zip-file fileb://index.zip --handler index.handler --runtime $(echo "$runtime") --role arn:aws:iam::221262875767:role/lambda-allow-basic
```

<!-- Below is the referred links. Not appearing in the rendered-markdown-->
[jq]: https://formulae.brew.sh/formula/jq

[Install AWS CLI v.2]: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html

[Configure your AWS credentials]: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html

