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
# Read the allow-role-policy.json. This can be customized.
policy=$(cat ./allow-role-policy.json | jq)
# Create the AWS-IAM role with the name lambda-ex and the above read-in policy. Name and Policy can be customized.
aws iam create-role --role-name lambda-ex --assume-role-policy-document $policy  
```

<!-- Below is the referred links. Not appearing in the rendered-markdown-->
[jq]: https://formulae.brew.sh/formula/jq

[Install AWS CLI v.2]: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html

[Configure your AWS credentials]: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html

