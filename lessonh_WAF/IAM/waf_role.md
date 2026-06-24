You need IAM Policy this the WAF Lambda..
this is for both parts of the lab

      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "logs:FilterLogEvents"
            ],
            "Resource": "*"
            # later use "Resource": "arn:aws:logs:us-east-1:123456789012:log-group:/aws/waf/*"
          },
          {
            "Effect": "Allow",
            "Action": [
              "bedrock:InvokeModel"
            ],
            "Resource": "*"
          },
            #Later
            #{
             # "Effect": "Allow",
             # "Action": [
             #   "events:PutEvents"
              # ],
            # "Resource": "*"
            #},
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:PutItem"
              "dynamodb:GetItem",
              "dynamodb:Query",
              "dynamodb:Scan"
            ],
            "Resource": "arn:aws:dynamodb:<region>:<account-id>:table/waf-events"
          }
        ]
      }
