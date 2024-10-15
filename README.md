# CloudSnap-Watchdog

# Objective:
The project aims to automate an AWS environment's cleanup process for Amazon Elastic Block Store (EBS) snapshots. EBS snapshots are utilized for recovery and backup, however as time passes, an accumulation of orphaned or underutilized snapshots may result in higher storage expenses. To ensure the overall dependability of the automation process, this project's aim was strengthened with strong error-handling methods to gracefully handle circumstances where related volumes or snapshots were not identified. The project demonstrated technical expertise in serverless architecture, AWS Lambda, CloudWatch, EBS, and SNS. By eliminating unnecessary, redundant EBS snapshots, the project significantly reduced costs and improved resource management in AWS cloud settings.

# Components:
AWS Lambda Function (lambda_handler):

Trigger: Scheduled execution, using AWS CloudWatch Events.

Rutime: Python.

Execution Role: The Lambda function assumes a role with the necessary permissions to interact with EC2 and delete EBS snapshots.

# Boto3 Library:
The official AWS SDK for Python interacts with AWS services programmatically.

# Functionality:
Snapshot Retrieval: Information about EBS snapshots held by the AWS account (OwnerIds=['self']) may be retrieved by using the describe_snapshots API.

Active Instance Retrieval: identifies and retrieves instance IDs from running EC2 instances using the describe_instances API.

Iteratively going through each received snapshot is the snapshot cleanup logic. determines if the snapshot is connected to a volume. In the event that it is not associated to a disk, deletes the snapshot. Verify whether the volume, if connected to it, is still present. Deletes the snapshot if the volume is empty (not connected to any active instances). Deletes the snapshot if the volume cannot be located (may have been erased).

Error Handling: To handle errors, such as when trying to describe volumes that might not exist anymore (InvalidVolume.NotFound), try and except blocks are used.

Logging: Prints messages to record the steps done and give insight into the cleaning procedure.

# Deployment:
The Lambda function is deployed in the AWS environment. It is scheduled to run at defined intervals (e.g., daily or weekly) using AWS CloudWatch Events.


# Considerations:
Permissions: Verify that the IAM policies required for EC2 and EBS activities are associated to the Lambda execution role.

Testing: Prior to deploying the Lambda function in a production environment, thoroughly test it in a controlled environment.

Monitoring: To gain further insight into the Lambda function's operation, put monitoring and logging systems (like AWS CloudWatch Logs) into place.


# Benefits:
Cost Optimization: Regularly cleaning up unused EBS snapshots helps reduce storage costs.

Resource Efficiency: Ensures storage resources are used efficiently by removing unnecessary snapshots.

Automation: Automates a manual and potentially error-prone task, improving operational efficiency.
