
# The S3 Bucket
1. Create a new S3 Bucket in the same region where your EC2 is located (disable "Block Public Access option and enable ACLs);

# ACL configuration
2. After crating the bucket, go to https://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html and copy the grants you will need to transport the EC2 image, creating a new ACL with the folowing permissions:

    READ_ACP (In the Amazon S3 console, Bucket ACL should have the Read permission)

    WRITE (In the Amazon S3 console, Objects should have the Write permission)

# Configuration file.json required
3. Create a JSON file containing the following informations:

    {
        "ContainerFormat": "ova",
        "DiskImageFormat": "VMDK",
        "S3Bucket": "YOURS3BUCKET"
    }

# Starting the export task
4. Log in the AWS CLI and put the command:

    aws ec2 create-instance-export-task --instance-id i-INSTANCEID --target-environment vmware --export-to-s3-task file://C:\file.json

5. The process will start and will take some time, depending on the size of your EC2 Instance;
