# Price Watchdog AWS Lambda

Here's a step-by-step guide on how to proceed with the Amazon price monitoring project using AWS Lambda, Python, S3, DynamoDB, and SNS:


### Step 1: AWS Configuration

1. **Creation of an S3 Bucket:**
   - Go to the AWS Management Console and open the S3 service.
   - Create a new bucket to save the price monitoring data.

2. **Configuration of DynamoDB:**
   - Open the DynamoDB service and create a new table to store price data.
   - Use a field like "ProductID" as the primary key.

3. **Creation of an SNS Topic:**
   - Go to SNS in the AWS Management Console and create a new topic for notifications.

### Step 2: Lambda Function Creation

1. **Opening Lambda:**
   - Go to the AWS Management Console and open the Lambda service.

2. **Creation of a new Lambda function:**
   - Click on "Create function" and choose "Author from scratch."
   - Assign a name to the function, choose Python as the runtime, and assign an IAM role with permissions to access S3, DynamoDB, and SNS.

3. **Adding CloudWatch Events Trigger:**
   - In the "Designer" section of your Lambda function, click on "Add trigger."
   - Select "CloudWatch Events" and configure a rule to trigger the function every day.

4. **Writing Lambda Code:**
   - Write the Python code for the Lambda function. Use the `boto3` library to access S3, DynamoDB, and SNS.
   - Scrape product pages on Amazon to obtain prices.
   - Compare current prices with those stored in DynamoDB.
   - If prices have changed, update DynamoDB and send an SNS notification.

```python
import boto3
import requests

def lambda_handler(event, context):
    # Code to get prices from Amazon, compare, and send notifications
    # ...

    # Example of saving data to S3
    s3 = boto3.client('s3')
    s3.put_object(Bucket='your-s3-bucket', Key='price-data.json', Body='data')

    # Example of updating data in DynamoDB
    dynamodb = boto3.resource('dynamodb')
    table = dynamodb.Table('your-dynamodb-table-name')
    table.put_item(Item={'ProductID': '123', 'Price': 29.99})

    # Example of sending an SNS notification
    sns = boto3.client('sns')
    sns.publish(TopicArn='arn:aws:sns:region:account-id:your-sns-topic', Message='Prices have changed!')

    return {
        'statusCode': 200,
        'body': 'Lambda function executed successfully!'
    }
```

### Step 3: Lambda Function Testing

1. **Manual Testing:**
   - Use the "Test" button in the Lambda console to manually test your function.

2. **Automated Testing:**
   - Wait for the CloudWatch Events trigger to fire your function and check the logs for any errors.

### Step 4: Monitoring and Optimization

1. **Resource Monitoring:**
   - Check CloudWatch metrics for your Lambda function and associated resources to ensure you stay within the free tier limits.

2. **Code Optimization:**
   - Optimize the code of your Lambda function to reduce execution times and resource usage.

Now you should have a working project that allows you to monitor prices on Amazon using AWS Lambda. Good luck!
