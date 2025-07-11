---
title: "Lab 2: Explore S3 Data Source"
weight: 32
---

# Objective 
In this lab, you will explore the S3 bucket structure set up for the Amazon Q Business application and look at the role-specific documents inside of S3. You will also examine the Access Control List (ACL), Amazon Q Business indexes access control list (ACL) information attached to documents. This information is used to filter chat responses based on a user's document access level, ensuring that users only receive information from documents they are authorized to access.
::alert[For this workshop, the **amazonq-workshop-s3-xxxxxx** bucket has been pre-created with all necessary files to complete the workshop.]{header="Note"}
## Scenario Overview
1. You're working with an S3 bucket that contains:
2. Separate folders for Support and Engineering documents
3. An ACL configuration file used by Amazon Q Business for access control
## What You'll Explore
1. S3 bucket structure
2. Look at content inside of support.pdf
3. Look at content inside of engineering.pdf
3. Look at acl.json file
:::code{language=mermaid}
graph TD
    A[amazonq-workshop-s3-xxxxxx];
    A --> C[acl];
    C --> D[acl.json];
    A --> E[data];
    E --> F[support];
    F --> X[support.pdf];
    E --> G[engineering];
    G ---> Z[engineering.pdf]; 
:::
## Expected Outcomes
1. Familiarity with the S3 bucket structure and role-based documents
2. Insight into how ACLs are used to control access by Amazon Q Business
# Begin
::alert[For this lab we will only be working in the AWS Managment Console]{header="Please Note"}

::::expand{header="Step 1: Open Support.pdf file"}
1. Open the :link[Amazon S3 console]{href="https://console.aws.amazon.com/s3"}
2. Choose the bucket that starts with **amazonq-workshop-s3-xxxxx**

![data](/static/labs/lab2/data.png)

3. Choose the **data/** directory
4. Choose the **support/** directory
5. Choose the **support.pdf** file
6. Choose the **open** button

![open](/static/labs/lab2/open.png)

The **support.pdf** contains AWS Support documentation. This document outlines basic support use cases and AWS services information. Access to this document is restricted to members of the **AmazonQSupportTeam** group in Okta, ensuring that only support personnel can query this content through Amazon Q Business.
::::

::::expand{header="Step 2: Open engineering.pdf file"}
1. Go back the **/data** directory in the **amazonq-workshop-s3-xxxxx** bucket
2. Choose the **engineering/** directory 

![eng](/static/labs/lab2/eng.png)

3. Choose the **engineering.pdf** file
6. Choose the **open** button

The **engineering.pdf** contains engineering project documentation, including details about "Project Pegasus". Access to this document is restricted to members of the **AmazonQEngineeringTeam** group in Okta, ensuring only engineering personnel can query this sensitive content through Amazon Q Business.
::::

::::expand{header="Step 3: Open acl.json file"}
1. Go back the **/acl** directory in the **amazonq-workshop-s3-xxxxx** bucket.

![acl](/static/labs/lab2/acl.png)

2. Choose the **acl.json** file
6. Choose the **open** button

The **acl.json** file contains access control configurations that define which Okta groups can access specific directories in the S3 bucket. It maps the **AmazonQEngineeringTeam** group to the engineering folder and the **AmazonQSupportTeam** group to the support folder, ensuring Amazon Q Business provides responses only from documents users are authorized to access.
::::

# Conclusion
In this lab, you explored the S3 bucket structure used by Amazon Q Business. You examined how documents are organized in role-specific folders, with engineering content in the engineering folder and support content in the support folder. You also learned how the ACL configuration in `acl.json` controls access to these documents, ensuring users can only query content relevant to their role when using Amazon Q Business.

::alert[Amazon Q Business supports over 40 different data source connectors, and ACLs can be applied in various ways depending on the source type. This lab demonstrated one approach using S3, but similar principles apply across different data sources to ensure secure and role-appropriate access to information.]{header="Keep in Mind"}



