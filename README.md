# Amazon Pinpoint API

## Introduction

This sample includes code that helps users leverage AWS services for data streaming, storage, and retrieval of event information using a simple API call. Specifically, a user can use a API call to check the status of a message sent via Amazon Pinpoint. 

When a customer receives a time sensitive email or SMS, the customer experience can be impacted. For instance, consider an e-commerce platform sending out shipping notifications. By quickly verifying that the message was delivered, businesses can preemptively address any potential issues, ensuring customer satisfaction. Amazon Pinpoint tracks email and SMS delivery and engagement events, which can be streamed using Amazon Kinesis Firehose for storage or further processing. However, third party applications don’t have a direct API to query and obtain the latest status of a message. This solution allows you to verify the message via API Gateway. 


## Architecture

![image](https://github.com/aws-samples/pinpoint-api-blog/assets/88910408/f16e7cd9-5765-4742-8057-1aa2dcd52fbf)

## Getting started

## Requirements
To deploy this sample solution code, you will need:
1. AWS Account ([setup](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)) with enough permission to deploy the application.
2. [AWS CLI version 2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) with [named profile setup](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html). 
3. An Amazon Pinpoint project that has never been configured with an event stream (PinpointEventStream)“
4. The Pinpoint ID from the Amazon Pinpoint project that you want to monitor. The Pinpoint ID can be found in the AWS Pinpoint console on the project’s main page (it will look something like “79788ecad55555513b71752a4e3ea1111”). Copy this ID to a text file, as you will need it shortly. Note, you must use the ID from a Pinpoint project that has never been configured with the PinpointEventStream option.

### Deployment Steps
1. Download the AWS CloudFormation Template "PinpointAPIBlog.yaml" from this repository to your computer.
2. Open the AWS CloudFormation console in the AWS region to which you want to deploy the solution.
3. Create a New Stack:
    * Choose Create Stack and select With new resources (standard) to start the stack creation process.
    * Under Prerequisite - Prepare template, select Template is ready.
    * Under 'Specify template', choose Upload a template file, and then upload the CloudFormation template file you downloaded in Step 1.
4. Configure the Stack:
    * Provide a stack name, such as “pinpoint-yourprojectname-monitoring” and paste the Pinpoint project (application) ID. Next.
    * Review the stack settings, and make any necessary changes based on your specific requirements. Next.
5. Initiate the Stack Creation: Once you've configured all options, acknowledge that AWS CloudFormation might create IAM resources with custom names, and then choose Create stack.
    * AWS CloudFormation will  provision and configure the resources defined in the "PinpointAPIBlog.yaml" template. This may take up to 20 minutes. You can view the status in the AWS CloudFormation console.

### Testing

1. Follow these instructions to test an email message: https://docs.aws.amazon.com/pinpoint/latest/userguide/messages-email.html
2. Follow these instructions to test an SMS message: https://docs.aws.amazon.com/pinpoint/latest/userguide/messages-sms.html
3. * Verify Lambda Execution:
    * Navigate to the AWS CloudWatch console.
    * Locate and review the logs for the Lambda functions specified in the solution (`aws/lambda/{functionName}`) to confirm that the Kinesis Data Firehose records are being processed successfully. In the log events you should see messages including INIT_START, Raw Kinesis Data Firehouse Record, etc.
4. Check Amazon DynamoDB Data:
    * Navigate to Amazon DynamoDB in the AWS Console.
    * Select the table created by the CloudFormation template and choose 'Explore Table Items'.
    * Confirm the presence of the event data by checking if the message IDs appear in the table. 
    * The table should have one or more message_id entries from the test message(s) you sent above.
    * Click on a message_id to review the data, and copy the message_id to a text editor on your computer. It will look like “0201123456gs3nroo-clv5s8pf-8cq2-he0a-ji96-59nr4tgva0g0-343434”
5. API Gateway Testing:
    * In the API Gateway console, find the MessageIdAPI.
    * Navigate to Stages and copy the Invoke URL provided.
    * Open the text editor on your computer and paste the APIGateway invoke URL. 
    * Create a curl command with you API Gateway + ?message_id=message_id. It should look like this:
        * “https://txxxxxx0.execute-api.us-west-2.amazonaws.com/call?message_id=020100000xx3xxoo-clvxxxxf-8cq2-he0a-ji96-59nr4tgva0g0-000000”
    * Copy the full curl command in your browser and enter.
    * The results should look like this (MacOS, Chrome): 

By following these deployment and testing steps, you'll have a functioning solution for tracking Pinpoint message delivery status using Amazon Pinpoint, Kinesis Fire Hose, DynamoDB and CloudWatch. 

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
