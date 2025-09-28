Accessing S3 Objects through CloudFront Distribution

prerequisite:
  S3 Object
  CloudFront Distribution

Implementation:
1. Create a S3 bucket and add object.
   * Block public access
   * Enable Bucket versioning
   * Enable static website hosting
  Try accessing the URL provided by S3 - 403 FORBIDDEN
   * Bucket policy:
         {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowCloudFrontOAC",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudfront.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<s3-bucket-name>/*",
            "Condition": {
                "StringEquals": {
                    "AWS:SourceArn": "arn:aws:cloudfront::<account-id>:distribution/<distribution-id>"
                }
            }
        }
    ]
}
2. Create a CloudFront Distribution
   * origin:
       origin domain - choose created s3 bucket
       Origin access - Origin access control settings (recommended)
     <img width="1527" height="102" alt="cloudfront-distrubution" src="https://github.com/user-attachments/assets/cdcbde2d-3b09-4397-b5bd-91d6f43ff327" />

   * Access the URL in the browser - SUCCESSFULLY ACCESSED s3 object from CloudFront
  
   <img width="1918" height="1017" alt="cloudfront" src="https://github.com/user-attachments/assets/9bf97a73-876d-4c9b-ac0b-57410fa73f88" />
