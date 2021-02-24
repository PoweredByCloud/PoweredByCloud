## Amazon S3 compatible API

Poweredby.Cloud provides support for Amazon S3 compatible API.
This means that you can continue to use your existing Amazon S3 tools (for example, SDK clients and CLI tools)
and also you can make minimal changes to their applications to work with PowerdbBy.Cloud.

### API support

Poweredby.Cloud support these following APIs:

* DeleteObject
* GetObject
* HeadBucket
* HeadObject
* ListBuckets
* ListObjects
* PutObject

### Configuration

`Access Key ID` and `Secret Access Key` can be created from [Developer Page](https://poweredby.cloud/dashboard/developer).

S3 API endpoint is `https://stdcdn.com`.

Poweredby.Cloud support latest S3 v4 signature version.

### Examples

#### AWS SDK for Python (Boto3)

The following is an example of calling ListBuckets API.

```python
import boto3


s3 = boto3.resource(
    's3',
    aws_access_key_id='82686f2af0e34d4b9da1ab4a593dff46',
    aws_secret_access_key='86bf1f02e5e4427ca14901788ee24393d8d6898a907648c49b8fc5fd529895b0',
    region_name='us-east-1',
    endpoint_url='https://stdcdn.com'
)

# Print out the bucket names
for bucket in s3.buckets.all():
    print(bucket.name)
```
