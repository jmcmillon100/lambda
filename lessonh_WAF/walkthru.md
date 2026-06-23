
Let's work on WAF.

1. WAF logs are already going to CloudWatch.
2. A Lambda reads the last few minutes of WAF log events.
3. Lambda extracts:

    source IP
    country
    URI
    HTTP method
    WAF action
    terminating rule
    
4. Lambda sends those details to Bedrock.
5. Bedrock returns a SOC-style summary.
6. Lambda prints the summary to CloudWatch.

No DynamoDB yet. No EventBridge yet. First, prove Bedrock can analyze the WAF event.

Required IAM permissions

The Lambda execution role needs:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:FilterLogEvents"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeModel"
      ],
      "Resource": "*"
    }
  ]
}


Lambda environment variables

Use these:

WAF_LOG_GROUP=/aws/waf/chewbacca-waf
BEDROCK_MODEL_ID=anthropic.claude-3-haiku-20240307-v1:0
LOOKBACK_MINUTES=10

Make this: Python Lambda: waf_bedrock_analyzer.py



