# aws-configservice-setup
Creates AWS ConfigService resources - as needed - to enable configuration change logging in every region.

### HowTo

1. Install needed dependencies:
  * Ruby
  * `gem install aws-sdk`
2. Edit `config.yml` to reflect the account to be configured:
  * **profile** - The pre-configured AWS CLI profile name with the AK / SK combo for the account to be configured.
  * **account_number** - The 12-digit AWS account number for the account to be configured.
  * **region** - The region to use for any single-region resources to be created.
  * **configservice_iam_role_name** -  The prefix of the IAM role for ConfigService that will be created for each region.
  * **configservice_s3_bucket_name** - The global S3 bucket prefix that will store ConfigService logs for all regions.
  * **configservice_sns_topic_name** - The SNS topic name that will be created in each region and used to broadcast ConfigService changes.
3. Run `config.rb`

### Caveats

It is possible that an `InsufficientDeliveryPolicyException` will be thrown when the script tries to create the DeliveryChannel. This is due to the IAM Role not being readily available after being created. A wait time has been added in, but it's still possible that it could happen. If this it does, simply run the script again as it is idempotent.
