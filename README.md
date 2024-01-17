# Amazon Pinpoint API

## Introduction

This sample include code that helps users leverage AWS services for data streaming, storage, and retrieval of event information using a simple API call. Specifically, a user can use a API call to check the status of a message sent via Amazon Pinpoint. 

When a customer recieves a time sensitive email or SMS, the customer experience can be impacted. For instance, consider an e-commerce platform sending out shipping notifications. By quickly verifying that the message was delivered, businesses can preemptively address any potential issues, ensuring customer satisfaction. Amazon Pinpoint tracks email and SMS delivery and engagement events, which can be streamed using Amazon Kinesis Firehose for storage or further processing. However, third party applications don’t have a direct API to query and obtain the latest status of a message. This solution allows you to verify the message via API Gateway. 


## Architecture

[TODO]

## Getting started

To get started and deploy the code in your AWS account please follow the current guides:

### Deployment


1. Download the AWS CF and navigate to the AWS CloudFormation console under the AWS region you want to deploy the solution.
2. Select Create stack and With new resources. Choose Template is ready as Prerequisite – Prepare template and Upload a template file as Specify template. Upload the template downloaded in step 1.
3. Fill the AWS CloudFormation parameters:
    1. PinpointProjectId: Paste your Amazon Pinpoint’s project Id.

### Testing

1. Follow these instructions to test an email message: https://docs.aws.amazon.com/pinpoint/latest/userguide/messages-email.html
2. Follow these instructions to test an SMS message: https://docs.aws.amazon.com/pinpoint/latest/userguide/messages-sms.html
3. Navigate to Cloudwatch and look at ‘aws/lambda/ProcessingLambdaFunction’ logs. This will allow you to check if the Kinesis Firehose records have been successfully recorded.
4. Navigate to DynamoDB. Choose **Tables**. Next, choose **PinpointLiveEvents**. Then, choose **Explore Table Items**. Copy the message_id for the data you would like to query for later.
5. Navigate to API Gateway and choose **MessageIDApi**. Then navigate to **Stages**. Copy the url under **Invoke URL**.
6. Lastly, open your terminal. Type the following command: curl “http://www.apigateway.com/call?message_id=1234”. Replace URL with the url you copied from API Gateway and replace the message_id with the id you copied from DynamoDB. 

## Requirements

- AWS Account Access ([setup](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)) with enough permission to deploy the application
- [AWS CLI version 2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) with [named profile setup](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
