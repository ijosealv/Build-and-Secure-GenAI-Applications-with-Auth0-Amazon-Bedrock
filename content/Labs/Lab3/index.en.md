---
title: "Lab 3: Configure Amazon Q Business Application"
weight: 33
---

# Objective 
In this lab, you will walk through the process of setting up an Amazon Q Business application with an S3 data source.
## Scenario Overview
1. AWS IAM Identity Center is integrated with Okta as the Identity Provider
2. Two distinct user groups exist in Okta:
    - **AmazonQEngineeringTeam**: Engineering personnel
    - **AmazonQSupportTeam**: Support personnel
## What You'll Build
1. Configure Amazon Q Business application named "workshop-application"
2. Assign group-based access to application
3. Add S3 data source to application with ACL
## Expected Outcomes
1. Role-appropriate document access
2. Secure information compartmentalization
3. Context-aware Amazon Q responses based on user roles
# Begin
::alert[For this lab we will only be working in the AWS Managment Console]{header="Please Note"}

::::expand{header="Step 1: Verify Users and Groups in AWS IAM Identity Center"}
1. Open the :link[IAM Identity Center console]{href="https://console.aws.amazon.com/singlesignon"}.
2. Choose **Groups** in the left navigation pane.
- Here you will see (2) groups provisioned from Okta **AmazonQSupportTeam** and **AmazonQEngineeringTeam**, each group has (1) User.

![groups](/static/labs/lab3/groups.png)

3. Choose **Applications** from the left navigation pane.
- Here you will see the **workshop-application** which is the Amazon Q Business application created for this workshop. AWS IAM Identity Center is used to manage User/Group access to the Amazon Q Business application.

![applications](/static/labs/lab3/applications.png)

No further action needed, continue to Step 2.

::::

::::expand{header="Step 2: Assign Group Access to Amazon Q Business Application"}

::alert[To know more about the different features of user subscription tiers, consult the :link[Amazon Q Business Guide]{href="https://docs.aws.amazon.com/amazonq/latest/qbusiness-ug/tiers.html#user-sub-features"}]{header="Note"}
1. Open the :link[Amazon Q Business Console]{href="https://console.aws.amazon.com/amazonq/business"}.
2. Under **Applications** choose **workshop-application**

![app](/static/labs/lab3/app.png)

3. Choose **Manage user access** button

![manage](/static/labs/lab3/manage.png)

4. Under the **Groups** tab click on **Add groups and users** button.
5. In the search bar enter **AmazonQSupportTeam** and click to add
6. Now search for **AmazonQEngineeringTeam** and click to add
7. Click **Assign**

![assign](/static/labs/lab3/assign.png)

8. Under the **Current Subscription** leave as is, **Q Business Pro** for both groups
9. Click **Confirm**

![confirm](/static/labs/lab3/confirm.png)

10. You should now see under **User access** (2) assigned groups.

![update](/static/labs/lab3/update.png)

No further action needed, continue to Step 3.
::::

::::expand{header="Step 3: Add Data S3 Source"}
::alert[For this workshop an index has been pre-created named **QBusiness-Index**]{header="Note"}
1. In the Amazon Q Business console, choose **Data sources** from the left navigation pane.
2. Choose **Add data source** button.

![add](/static/labs/lab3/add.png)

3. In the **Data Sources** section select **Amazon S3**
4. In the **Add Amazon S3** page enter out the following details
    - **Data source name**: `s3-data-source`
    - **IAM role**: Select `Create a new service role (Recommended)`
    - Leave the **Role name** at its default (a new role name was generated).

![s3name](/static/labs/lab3/s3name.png)

5. Under **Sync Scope** enter the following details
    - **Enter the data source location**: use the **Browse S3** button to choose the S3 bucket that was created for the workshop **(s3://amazonq-workshop-s3-XXXXXXXXXXX)**
    - **Access control list (ACL) configuration file location**: use the **Browse S3** button to choose the **acl.json** file, located in the **/acl** directory.
    - **Include patterns**: Type: **Prefix**; Prefix: **data**

![s3prefix](/static/labs/lab3/s3prefix.png)

6. Under **Sync mode** select **Full sync**
7. Under **Sync run schedule** select **Run on demand**

![s3sync](/static/labs/lab3/s3sync.png)

8. Leave the Configure VPC and security group, Tags, and Field mappings cards as default.
9. Choose **Add data source**

![adddata](/static/labs/lab3/adddata.png)

10. You'll be automatically redirected to the data source page. You will see that the **Status** shows as **Creating** - this takes less than a minute.
11. Click the **Sync now** button to start a synchronization of the S3 data source.

![sync](/static/labs/lab3/sync.png)

The sync for (2) files will take approximately 8-10 minutes. You may continue with Lab 4 while this runs. 

::::
# Conclusion
In this lab, you set up an Amazon Q Business application with an S3 data source. You configured group-based access to the application and added an S3 bucket as a data source with role-specific ACLs. This setup enables Amazon Q to provide context-aware responses based on user roles while maintaining secure information compartmentalization.

