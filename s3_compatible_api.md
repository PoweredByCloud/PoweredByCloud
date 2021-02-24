# Amazon S3 compatible API

Poweredby.Cloud provides support for Amazon S3 compatible API.
This means that you can continue to use your existing Amazon S3 tools (for example, SDK clients and CLI tools)
and also you can make minimal changes to their applications to work with PowerdbBy.Cloud.

## API support

Poweredby.Cloud support these following APIs:

* DeleteObject
* GetObject
* HeadBucket
* HeadObject
* ListBuckets
* ListObjects
* PutObject

## Configuration

`Access Key ID` and `Secret Access Key` can be created from [Developer Page](https://poweredby.cloud/dashboard/developer).

S3 API endpoint is `https://stdcdn.com`.

Poweredby.Cloud support latest S3 v4 signature version.

## Examples

### AWS SDK for Python (Boto3)

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

### S3cmd

[S3cmd](https://s3tools.org/s3cmd) is a popular command line S3 client for Linux and Mac.
First follow [this link](https://github.com/s3tools/s3cmd/blob/master/INSTALL.md) to install.

To configure PoweredBy.Cloud as your default provider, use the *--configure* option.

```bash
$ s3cmd --configure
```

s3cmd requests your access and secret keys.

```bash
Access Key: 82686f2af0e34d4b9da1ab4a593dff46
Secret Key: 86bf1f02e5e4427ca14901788ee24393d8d6898a907648c49b8fc5fd529895b0
```

Enter `us-east-1` for default region.

```bash
Default Region [US]: us-east-1
```

Enter `stdcdn.com` for S3 endpoint.

```bash
S3 Endpoint [s3.amazonaws.com]: stdcdn.com
```

Enter `%(bucket)s.stdcdn.com` for DNS-style template.

```bash
DNS-style bucket+hostname:port template for accessing a bucket [%(bucket)s.s3.amazonaws.com]: %(bucket)s.stdcdn.com
```

Press <kbd>ENTER</kbd> to skip encryption password.
Read more from [s3tools.org](https://s3tools.org) if you like to use password to protect your s3cmd configuration file.

```bash
Encryption password:
Path to GPG program:
```

Press <kbd>ENTER</kbd> to use HTTPS protocol.

```bash
Use HTTPS protocol [Yes]:
```

Press <kbd>ENTER</kbd> to skip proxy.

```bash
HTTP Proxy server name:
```

Press <kbd>Y</kbd> + <kbd>ENTER</kbd> to test the s3cmd configuration.

```bash
Please wait, attempting to list all buckets...
Success. Your access key and secret key worked fine :-)
```

Press <kbd>Y</kbd> + <kbd>ENTER</kbd> to save `.s3cfg` file.

```bash
Configuration saved to '~/.s3cfg'
```

You can use s3cmd to manage files like this

```bash
# List buckets
$ s3cmd ls

# List files
$ s3cmd ls s3://mybucket/

# List files in bucket recursivly
$ s3cmd --recursive ls s3://mybucket/

# Upload file
# Remember adding --disable-multipart option so that s3cmd use PutObject api to upload files
# PoweredBy.Cloud does not support multipart upload right now
$ s3cmd --disable-multipart put /path/to/demo.png s3://mybucket/path/to/demo.png

# Download file
$ s3cmd get s3://mybucket/path/to/demo.png

# Delete file
$ s3cmd rm s3://mybucket/path/to/demo.png
```

### AWS cli
