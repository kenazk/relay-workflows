This workflow finds all unencrypted S3 buckets in a given account and encrypts them
with default encryption. 

For more information on default encryption, see [Amazon S3 Default Encryption for S3 Buckets
](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)

## Prerequisites

Before you run this workflow, you will need the following:  
- An AWS account.  
- An AWS IAM user with permissions to list and modify S3 buckets (if not
  run in dry run mode).  
- One or more S3 buckets that are unencrypted.  

## Run the workflow

Follow these steps to run the workflow:  
1. Add your AWS credentials as a Connection:
   - Click **Setup** 
   - Find the Connection named `my-aws-account` and click Edit(✎). Use the following values:  
      - **KEY**: `ACCESS KEY ID`  
      - **VALUE**: Enter your AWS access key id associated with the account  
      - **KEY**: `SECRET ACCESS KEY`  
      - **VALUE**: Enter your AWS secret access key associated with the account  
   - Click **Save**  
      
2. Click **Run workflow** and wait for the workflow run page to appear.  
3. Supply following parameters to the modal:  
   - **KEY**: `dryRun`  
   - **VALUE**: True if you don't want to perform actual WRITE operations  

4. **Warning:** If you run the workflow with the `dryRun` parameter set to
   `false`, buckets not in compliance with this workflow policy will
   immediately be modified to be 'private'.  

## Run the workflow on a schedule  

Follow these steps to run this workflow on a schedule:  
-  Un-comment out the Trigger block in the workflow file:  

> TIP: If you're using the Relay code editor, highlight the `triggers` section and type `⌘ + /` (Mac) or `Ctrl + /` (Windows) to uncomment.  

```yaml
# triggers:
# - name: schedule
#   source:
#     type: schedule
#     schedule: '0 * * * *'
#   binding:
#     parameters:
#       dryRun: true
```

-  Configure the `schedule` trigger:  
   - Supply the run interval in [cron format](https://crontab.guru/).  
-  Configure the following parameter bindings:  
   - Specify whether `dryRun` should be set to `true` or `false`.  
-  Click **Save changes**