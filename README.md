# hubot-lambda
[![Build Status](https://travis-ci.org/davemkirk/hubot-lambda.svg?branch=master)](https://travis-ci.org/davemkirk/hubot-lambda)

[![NPM](https://nodei.co/npm/hubot-lambda.png?downloads=true)](https://nodei.co/npm/hubot-lambda/)

A [Hubot](https://hubot.github.com/) script for invoking [AWS Lambda](http://aws.amazon.com/lambda/) functions

## Why

- Separate invocation privileges from execution privileges.
- New languages will almost certainly be added to AWS Lambda, in this case hubot-lambda would enable easy cross language Hubot integrations. (Amazon recently announced that support for Java Lambda functions are coming soon. https://aws.amazon.com/blogs/aws/aws-lambda-update-production-status-and-a-focus-on-mobile-apps/)
- Potentially a robust mechanism for enabling ad-hoc hubot script additions/modifications without recycling the hubot process. (I'd like some feedback on this one)  

## Installation

Add `hubot-lambda` to your package.json, run `npm install` and add hubot-lambda to `external-scripts.json`.

Add hubot-lambda to your `package.json` dependencies.

```
"dependencies": {
  "hubot-lambda": "0.0.0"
}
```

Add `hubot-lambda` to `external-scripts.json`.

```
> cat external-scripts.json
> ["hubot-lambda"]
```

##### Required ENV Variables

```
> export HUBOT_LAMBDA_AWS_ACCESS_KEY_ID="XXXX"
> export HUBOT_LAMBDA_AWS_SECRET_ACCESS_KEY="XXXX"
```

##### Optional ENV Variables

`HUBOT_LAMBDA_PRODUCTION_QUALIFIER` is set to "prod" if not specified. This
refers to an alias for the lambda function to allow for control of what version
should be used in production. See [AWS Lambda Function Versioning and Aliases](http://docs.aws.amazon.com/lambda/latest/dg/versioning-aliases.html)

```
> export HUBOT_LAMBDA_PRODUCTION_QUALIFIER="XXXX"
```

##### Required AWS User Policy
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "lambda:InvokeFunction"
      ],
      "Resource": "*"
    }
  ]
}
```


Usage
-----

- `hubot lambda <functionName> <arg1>:<value> <arg2>:<value>`

Example
-----

- `hubot lambda helloWorld message:Yo`



## Developing hubot-lambda

##### Running from working dir
-----
```
vagrant up
vagrant ssh
cd hubot
./bin/hubot
```

##### Troubleshooting
-----
>HUBOT_LOG_LEVEL=debug ./bin/hubot

