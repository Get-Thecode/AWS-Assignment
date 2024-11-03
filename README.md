Project Overview
This project is a .NET Core API that integrates AWS S3 for file storage, demonstrating file handling and cloud storage management. The configuration emphasizes modular and clean architecture principles.

Setup and Configuration
Prerequisites
.NET Core SDK: Ensure you have the .NET Core SDK installed.
AWS Account: Set up an AWS account, create an S3 bucket named yadav-file-storage, and configure IAM user credentials.
AWS S3 Configuration
Bucket Name: yadav-file-storage

Region: eu-north-1

IAM Policy for S3 Access:
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
Update your appsettings.json with AWS credentials and region:

json
Copy code
"AWS": {
    "AccessKey": "your-access-key",
    "SecretKey": "your-secret-key",
    "Region": "eu-north-1"
}
var awsOptions = builder.Configuration.GetSection("AWS");
var credentials = new BasicAWSCredentials(awsOptions["AccessKey"], awsOptions["SecretKey"]);
RegionEndpoint region = RegionEndpoint.GetBySystemName(awsOptions["Region"]);
builder.Services.AddSingleton<IAmazonS3>(sp => new AmazonS3Client(credentials, region));

SOLID Principles Applied
Single Responsibility: Separate concerns for AWS configuration, error handling, and setup instructions.
Open-Closed: AWS services are configured for easy extension without modifying existing classes.
Dependency Injection: Inject IAmazonS3 into services, enhancing testability.

