.NET Core API with AWS S3 Integration
Project Overview
This project is a .NET Core API that integrates with AWS S3 for file storage. It demonstrates file handling and cloud storage management, following modular, clean architecture principles and adhering to the SOLID design principles.

Setup and Configuration
Prerequisites
.NET Core SDK: Make sure the .NET Core SDK is installed on your machine.
AWS Account: Set up an AWS account. Create an S3 bucket named yadav-file-storage, and configure IAM user credentials with permissions to access the bucket.
AWS S3 Configuration
Bucket Details
Bucket Name: yadav-file-storage
Region: eu-north-1
IAM Policy for S3 Access
Configure your IAM user with a policy that grants the required permissions for file handling in S3. Here’s an example policy:

json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPutObject",
            "Effect": "Allow",
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::yadav-file-storage/*"
        },
        {
            "Sid": "AllowGetObject",
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::yadav-file-storage/*"
        },
        {
            "Sid": "AllowListBucket",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::yadav-file-storage"
        }
    ]
}
appsettings.json Configuration
Update your appsettings.json with your AWS credentials and region as follows:

json
Copy code
"AWS": {
    "AccessKey": "your-access-key",
    "SecretKey": "your-secret-key",
    "Region": "eu-north-1"
}
Configure AWS S3 Client in .NET Core
In your code, retrieve AWS credentials from configuration and set up the S3 client:

csharp
Copy code
var awsOptions = builder.Configuration.GetSection("AWS");
var credentials = new BasicAWSCredentials(awsOptions["AccessKey"], awsOptions["SecretKey"]);
RegionEndpoint region = RegionEndpoint.GetBySystemName(awsOptions["Region"]);
builder.Services.AddSingleton<IAmazonS3>(sp => new AmazonS3Client(credentials, region));
SOLID Principles Applied
Single Responsibility: AWS configuration, error handling, and setup instructions are clearly separated into distinct components.
Open-Closed: AWS services are configured for easy extension without modifying existing classes, enhancing flexibility.
Dependency Injection: The IAmazonS3 service is injected into necessary components, improving testability and code modularity.





