# AWS permissions

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::971333952697:role/service-role/AmazonEMR-ServiceRole-20230525T120500"
            },
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::spark-testing-cluster",
                "arn:aws:s3:::spark-testing-cluster/*"
            ]
        },
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": ""
            },
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::spark-testing-cluster",
                "arn:aws:s3:::spark-testing-cluster/*"
            ]
        }
    ]
}
```