---
title: "Lab 4: Role Based Scenarios"
weight: 34
---

# Objective 
In this lab, you will test Amazon Q Business's access controls lists (ACLs) by signing in as different users and verifying that they can only access documents appropriate to their roles. You'll see how Amazon Q Business uses ACLs to ensure secure access to information based on user groups from Okta.
### Scenario Overview
1. Sign in as a Support User to verify access to support documentation
2. Sign in as an Engineering User to verify access to engineering documentation
3. Test access restrictions by attempting to query content outside each user's permissions
### What You'll Test
1. **Support User Access**
    - Access to support documentation
    - Restricted access to engineering content
2. **Engineering User Access**
    - Access to Project Pegasus documentation
    - Engineering-specific content queries
## Before You Begin
1.  Have your Okta organization URL ready
2.  Have the following credentials available:
    - Support User: **qsupport**
    - Engineering User: **qengineer**
# Begin
::alert[For this lab, you'll need to use private browser windows when switching between users to ensure clean authentication sessions.]{header="Important"}

::::expand{header="Step 1: Login as Support User"}
1. Please use a **new private browser window** for this step.
2. Navigate to **Okta.com** choose **login** and enter the **organization url**.
3. Sign an as the **Support User**
- Username: [qsupport]
- Password: [password]

![loginsup](/static/labs/lab4/loginsup.png)

4. Once logged in choose the **AWS IAM Identity Center** app.
5. Choose the **workshop-application** option

![link](/static/labs/lab4/link.png)

6. This will open up the Amazon Q Business chatbot
7. Ask the following question "what is an iam role"

![iam](/static/labs/lab4/iam.png)

You will see Amazon Q Business provide a detailed response about IAM roles, with a citation indicating the information was sourced from the support.pdf document. This confirms that as a Support User has access to query and receive information from the support documentation.

::alert[Notice how Amazon Q Business provides support information while maintaining proper access controls - only support team members can access.]{header="Note"}

8. Now ask about project pegasus "what is Project Pegasus"

![ask](/static/labs/lab4/ask.png)

You will see Amazon Q Business respond with "No answer is found." This demonstrates that the ACL is working as intended - since you're logged in as a Support User, you cannot access content from the engineering.pdf document which contains the Project Pegasus information. This is an example of how Amazon Q Business uses ACLs to maintain data security and ensure users can only query documents they're authorized to access.

9. Feel free to ask more questions or move on to the next step.
::::

::::expand{header="Step 2: Login as Engineering User"}
1. Please use a **new private browser window** for this step.
2. Navigate to **Okta.com** choose **login** and enter the **organization url**.
3. Sign an as the **Engineering User**
- Username: [qengineer]
- Password: [password]

![logine](/static/labs/lab4/logine.png)

3. Once logged in choose the **AWS IAM Identity Center** app.
4. Choose the **workshop-application** option

![link](/static/labs/lab4/link.png)

5. This will open up the Amazon Q Business chatbot
6. Ask about project pegasus "what is Project Pegasus"

![askpos](/static/labs/lab4/askpos.png)

You will see Amazon Q Business provide a detailed response about Project Pegasus, explaining that it's a confidential quantum computing initiative. The response includes citations from engineering.pdf, confirming that as an Engineering User, you have proper access to this project information.

::alert[Notice how Amazon Q Business provides detailed project information while maintaining proper access controls - only engineering team members can access this confidential content.]{header="Note"}

7. Now ask "what is an IAM role"

![askiam](/static/labs/lab4/askiam.png)

You will see Amazon Q Business respond with "No answer is found." This demonstrates that the ACL is working as intended - since you're logged in as an Engineering User, you cannot access content from the support.pdf document which contains AWS support documentation. 

::alert[Notice how Amazon Q Business provides detailed project information while maintaining proper access controls - only engineering team members can access this confidential content. If you need Engineering users to access support.pdf, you would need to modify the acl.json file to grant the AmazonQEngineeringTeam group access to the support folder path.]{header="Note"}


8. Feel free to ask more questions or move on to the next step.
::::
# Conclusion
In this lab, you tested Amazon Q Business's role-based access controls by signing in as both Support and Engineering users. You verified that:

- Support users could access support documentation but were restricted from engineering content

- Engineering users could access Project Pegasus information but not support content

This demonstrates how Amazon Q Business effectively uses ACLs to maintain data security, ensuring users receive responses only from documents they're authorized to access based on their Okta group membership.

::alert[While this lab demonstrated ACL implementation with S3, Amazon Q Business supports over 40 different data source connectors. Each connector type may implement access controls differently based on the source system's capabilities and security requirements. This flexibility allows organizations to maintain consistent security controls across diverse data sources.]{header="Important Note"}


