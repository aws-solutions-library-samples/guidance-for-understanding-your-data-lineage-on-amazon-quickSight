# Guidance for Data Lineage with Amazon QuickSight

## Table of Content

List the top-level sections of the README template, along with a hyperlink to the specific section.

### Required

1. [Overview](#overview-required)
    - [Cost](#cost)
2. [Prerequisites](#prerequisites-required)
    - [Operating System](#operating-system-required)
3. [Deployment Steps](#deployment-steps-required)
4. [Deployment Validation](#deployment-validation-required)
5. [Running the Guidance](#running-the-guidance-required)
6. [Next Steps](#next-steps-required)
7. [Cleanup](#cleanup-required)

## Overview

Business Intelligence (BI) Engineers and Data Architects can accelerate their understanding of Data Lineage in QuickSight by deploying Lambda, Glue, Athena, S3 and QuickSight using CloudFormation to visualize data usage as well as relationship between Data sources, Analyses, Dashboards and fields within Dashboards.

### Cost

_You are responsible for the cost of the AWS services used while running this Guidance. As of 01/2024, the cost for running this Guidance with the default settings in the <Default AWS Region (Most likely will be US East (N. Virginia)) > is approximately $10.50 per month._

Replace this amount with the approximate cost for running your Guidance in the default Region. This estimate should be per month and for processing/serving resonable number of requests/entities.


## Prerequisites

### AWS account requirements

* This deployment requires you have an AWS CloudTrail trail enabled in the region you are deployment. The trail should have Management Events enabled
* Ensure QuickSight has access to the S3 bucket created by this stack post deployment - https://docs.aws.amazon.com/quicksight/latest/user/troubleshoot-connect-S3.html

### Supported Regions

The Guidance is recommended to be deployed in the same AWS region having QuickSight resources.

## Deployment Steps

**Required Input Parameters**
- Stack name - Stack name can include letters (A-Z and a-z), numbers (0-9), and dashes (-)
- QuickSightUser - User name of an active QuickSight user who needs access to the Data Lineage Dashboard and relevant QuickSight resources.
- QuickSightUserNamespace - Namespace of the QuickSight user (Provide 'default' unless the above QuickSight user was created in a different Namespace)

**Optional Input Parameters**
- Suffix - Add a short NUMERIC suffix here if you need to create multiple instances of this deployment

1. Download the YAML file from this repository
2. Navigate to AWS Console
3. Search for CloudFormation in the "Services" search bar
4. Once in the CloudFormation console, click on the "Create Stack" button (use the "With new resources option")
5. In the "Create Stack" wizard, chose "Template is ready", then select "Upload a template file"
6. Upload the YAML file, click Next
7. In the Specify stack details screen, provide the required inputs
8. In the Configure Stack options screen, leave the configurations as-is. Click Next
9. In the Review screen, scroll down to the bottom of the page to the Capabilities section and acknowledge the notice that the stack is going to create required IAM Roles by checking the check box. 
10. Click Create stack


## Deployment Validation

Navigate to QuickSight and login as the QuickSight user provided when creating the AWS CloudFormation stack. IF the deployment is successful, you should see a 'Data Lineage' Dashboard with relevant DataSets created.


## Running the Guidance

The Guidance automatically updates the QuickSight resource metadata stored in the S3 bucket based on resource creation, deletion or modification in QuickSight.

## Next Steps

The Data Lineage Dashboard created in QuickSight can be saved as a new Analysis, and customized to add/modify visuals, interactivity or filters. The Dashboard can be shared to other QuickSight users in the same AWS Account.

## Cleanup

Deleting the AWS CloudFormation stack deletes the two deployed Lambda functions. However, the following resources need to be manually deleted to accruing cost.

- S3 Bucket: *createquicksight-dlcodebucket-<AWS_Account_ID>-<Suffix>*
- S3 Bucket: *quicksight-datalineage-<AWS_Account_ID>-<Suffix>*
- EventBridge Rule: *quicksight-datalineage-rule-<Suffix>*
- Athena Database and Tables: *quicksightdatalineage* database and all tables in this database

## Notices

*Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers.*
