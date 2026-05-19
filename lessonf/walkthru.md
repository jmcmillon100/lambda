Phase 1 — Create DynamoDB Table

Navigation
    DynamoDB
    Create Table

    Table Name: token-tracking
    Partition Key: token_id
    Type:: String
    Capacity Mode: On-demand

Table Purpose

Each token gets tracked:

    {
      "token_id": "abc123",
      "username": "student1",
      "issued_at": "2026-05-19T20:00:00Z",
      "used": false
    }


Phase 2 — Modify get_token.py

Now the script becomes:

    auth utility
    telemetry producer

Add DynamoDB Write---> After successful authentication:
modify your get_token.py


    import uuid
    from datetime import datetime
    
    dynamodb = boto3.resource("dynamodb")
    table = dynamodb.Table("token-tracking")
    
    token_id = str(uuid.uuid4())
    
    table.put_item(
        Item={
            "token_id": token_id,
            "username": username,
            "issued_at": datetime.utcnow().isoformat(),
            "used": False
        }
    )


Phase 3 — Mark Token Used

When Lambda receives valid request: Update DynamoDB:
Lambda: update.py



