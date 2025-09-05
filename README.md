# AWS Deadline Cloud Setup Script

This bash script automates the end-to-end setup of a basic AWS Deadline Cloud environment. It handles the creation of all necessary resources, including an S3 bucket for storage, a Deadline Cloud farm, IAM roles with correct trust policies, a queue, a service-managed fleet, and the association between the queue and the fleet.

This script is ideal for developers and administrators who want to quickly spin up a functional Deadline Cloud environment for testing or development purposes without manual console configuration.

---

## Prerequisites

Before running the script, ensure you have the following:

- **AWS CLI:** The AWS Command Line Interface must be installed and configured with a profile that has administrative permissions to create IAM roles, S3 buckets, and Deadline Cloud resources.
- **`jq`:** The `jq` command-line JSON processor is required to parse output from AWS CLI commands. You can install it using your system's package manager (e.g., `sudo apt-get install jq` on Ubuntu, `brew install jq` on macOS).

---

## Configuration

You must modify the **`USER CONFIGURATION`** section of the script to match your specific AWS account and resource names.

```bash
# =============================================================================
# USER CONFIGURATION
# =============================================================================
# The AWS region where resources will be created. Must be a region that supports AWS Deadline Cloud.
export AWS_REGION="us-east-1"
# The AWS CLI profile to use for authentication.
export AWS_PROFILE="kj-aws"
# The name for the S3 bucket. Must be globally unique.
export S3_BUCKET="kj-aws-test-deadline-cloud-storage-bucket"
# Set to "true" to create a new S3 bucket, or "false" to use an existing one.
export CREATE_S3_BUCKET="true"
# A display name for your Deadline Cloud farm.
export DEADLINE_CLOUD_FARM_NAME="kj-aws-test-my-deadline-farm"
# Names for the IAM roles to be created. These should be unique within your account.
export QUEUE_SERVICE_ROLE_NAME="kj-aws-test-DeadlineCloud-Queue-Service-Role-3"
export FLEET_SERVICE_ROLE_NAME="kj-aws-test-DeadlineCloud-Fleet-Service-Role-3"
export MONITOR_USER_ROLE_NAME="kj-aws-test-AWSDeadlineCloudMonitorUserRole-3"
# A display name for the render fleet.
export DEADLINE_FLEET_DISPLAY_NAME="my-deadline-fleet"
# The maximum number of workers for your fleet.
export MAX_WORKER_COUNT=5
# The name of the local JSON file that defines the fleet's EC2 configuration.
export FLEET_CONFIG_FILE="service-managed-fleet-config.json"
# The ARN of the IAM entity (user or role) that will be associated with the monitor.
export PRINCIPAL_ID_ARN="arn:aws:iam::833740154547:user/envoi-services"
