# Serverless File Processor Application

This project implements a *serverless file processing application* using *AWS Lambda, **API Gateway, **S3, **DynamoDB, and **AWS CDK. Users can upload text files via an API, process them using a Lambda function, and store the processed data in DynamoDB. The application is fully automated using **CI/CD* pipelines with *AWS CodePipeline*.

## Project Overview

- *S3 Bucket*: Stores uploaded text files.
- *Lambda Function*: Processes the uploaded files (counts the number of lines).
- *DynamoDB*: Stores the results, including the filename, timestamp, and line count.
- *API Gateway*: Exposes an HTTP POST endpoint for file uploads.
- *AWS CDK*: Used for infrastructure as code (IaC).
- *CI/CD Pipeline*: Automates the deployment using AWS CodePipeline, with integration to GitHub for version control.

## Prerequisites

- *AWS Account*: To create and deploy AWS resources.
- *AWS CLI*: Install the AWS CLI to interact with AWS services.
- *AWS CDK*: Install AWS CDK globally on your machine.
  ```bash
  npm install -g aws-cdk
Node.js and npm: Ensure Node.js and npm are installed for managing dependencies.
GitHub: A GitHub account to clone the repository and configure CI/CD.
Setting Up the Project
1. Clone the GitHub Repository
Clone the repository to your local machine:

bash
Copy code
git clone https://github.com/your-github-username/serverless-file-processor.git
cd serverless-file-processor
2. Install Dependencies
Navigate to the cdk folder and install necessary Node.js dependencies:

bash
Copy code
cd cdk
npm install
3. Deploy the Infrastructure
Deploy the serverless application to AWS using AWS CDK:

bash
Copy code
cdk deploy
This command will deploy the following resources:

S3 Bucket for file storage
DynamoDB Table for storing processed file information
Lambda Function for processing the files
API Gateway for file upload endpoint
4. Upload Files via API
After deployment, the API Gateway URL will be provided. You can upload text files by sending a POST request to the /upload endpoint with the file as the body.

Example using curl:

bash
Copy code
curl -X POST -F "file=@yourfile.txt" https://your-api-gateway-url/upload
5. View Processed Data in DynamoDB
The processed data (filename, timestamp, and line count) will be stored in the ProcessedFiles DynamoDB table. You can view the records directly through the AWS Console or use AWS CLI to query the data.

Example AWS CLI query:

bash
Copy code
aws dynamodb scan --table-name ProcessedFiles
CI/CD Pipeline
1. GitHub Integration
The project is integrated with GitHub as the source repository. When changes are pushed to the main branch, the CodePipeline is automatically triggered to build and deploy the changes.

2. CodePipeline Stages
Source Stage: Pulls the code from GitHub.
Build Stage: Uses AWS CodeBuild to install dependencies and synthesize the CDK stack.
Deploy Stage: Deploys the stack to AWS using CloudFormation.
3. Setting Up CodePipeline
To set up the CI/CD pipeline with GitHub, ensure that your GitHub token is stored in AWS Secrets Manager as github-token. This token will be used to authenticate CodePipeline with your GitHub repository.

4. CodeBuild Configuration
The project uses AWS CodeBuild to install dependencies and build the CDK stack. The configuration file buildspec.yml defines the build steps.

5. Push Changes to GitHub
Once you push changes to the main branch, CodePipeline will automatically:

Pull the updated code from GitHub
Build the application using CodeBuild
Deploy the updated stack to AWS
Lambda Function
The Lambda function is triggered when a file is uploaded to the S3 bucket. It performs the following tasks:

Reads the file from the S3 bucket.
Counts the number of lines in the file.
Creates a JSON object with the filename, timestamp, and line count.
Stores the result in DynamoDB.
Directory Structure
python
Copy code
├── cdk/                   # AWS CDK infrastructure code
│   ├── lib/                # Define infrastructure resources here
│   ├── bin/                # Entry point to the CDK app
├── lambda/                # Lambda function code
│   ├── handler.py          # Lambda function logic
├── buildspec.yml           # CodeBuild configuration
├── README.md               # Setup and usage instructions
├── .gitignore              # Ignore unnecessary files
└── cdk.json                # CDK configuration
Cleanup
To delete the resources created by this project and avoid ongoing charges, you can run the following command to tear down the infrastructure:

bash
Copy code
cdk destroy
Contributing
Feel free to open issues and submit pull requests. All contributions are welcome!

License
This project is licensed under the MIT License - see the LICENSE file for details.

markdown
Copy code

### Explanation:

- *Project Overview*: Describes the application's components.
- *Prerequisites*: Lists the tools and services needed for setup.
- *Setting Up the Project*: Provides detailed instructions to clone, install dependencies, and deploy the infrastructure.
- *CI/CD Pipeline*: Explains the CI/CD flow, including GitHub integration, CodePipeline, and CodeBuild setup.
- *Lambda Function*: Describes the functionality of the Lambda function.
- *Directory Structure*: Provides an overview of the project folder organization.
- *Cleanup*: Explains how to remove resources when the project is no longer needed.
- *Contributing*: Encourages collaboration and contributions to the project.
- *License*: Specifies the licensing for the project.

This README.md ensures that all the requirements are clearly documented and easy for others
