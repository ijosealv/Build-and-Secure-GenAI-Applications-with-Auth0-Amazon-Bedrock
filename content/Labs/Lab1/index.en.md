---
title: "Lab 1: Configure Okta as Idp in AWS IAM Identity Center"
weight: 31
---

# Objective 
In this lab, you will set up a SAML connection between Okta and AWS IAM Identity Center, and configure user synchronization using the System for Cross-domain Identity Management (SCIM) standard.
### Scenario Overview
1. User and group management is centralized in Okta
2. Users need to access AWS resources through the Okta portal
3. AWS IAM Identity Center needs to be integrated with Okta for seamless identity management
### What You'll Build
1. **SAML Connection**
   - Configure Okta as an external identity provider for AWS IAM Identity Center
   - Set up SAML metadata exchange between Okta and AWS
2. **SCIM Provisioning**
   - Enable automatic user provisioning from Okta to AWS IAM Identity Center
   - Configure SCIM endpoint and access token
3. **User and Group Synchronization**
   - Push groups from Okta to AWS IAM Identity Center
   - Verify user population in AWS IAM Identity Center
### Expected Outcomes
1.  Seamless Single Sign-On (SSO) from Okta to AWS
2.  Automated user and group synchronization
3.  Centralized identity management through Okta

This setup ensures that your AWS environment stays in sync with your Okta user directory, providing a streamlined access management experience for your organization.
# Begin
::alert[This workshop uses a single-account instance of AWS IAM Identity Center. In production environments, an organization-level instance is recommended.]{header="Note"}

::::expand{header="Step 1: Obtain the SAML metadata from your Okta account"}
1. Sign in to the **Okta admin dashboard** by signing in as Admin User. Once inside Admin Console expand **Applications**, then select **Applications**.
2. On the **Applications** page, choose **AWS IAM Identity Center** app.

![application](/static/labs/lab1/application.png)

3. Select the **Authentication** tab.

![auth](/static/labs/lab1/authentication.png)

4. Under **SAML Signing Certificates**, select **Actions**, and then select **View IdP Metadata**. 
    - A new browser tab opens showing the document tree of an XML file. Select all of the XML from `<md:EntityDescriptor>` to `</md:EntityDescriptor>` and copy it to a text file.

![saml](/static/labs/lab1/saml.png)

5. Save the text file as **metadata.xml**

![savefile](/static/labs/lab1/savefile.png)

**Leave the Okta admin dashboard open, you will continue using that console in the later steps**
::::

::::expand{header="Step 2: Configure Okta as the identity source for IAM Identity Center"}
1. Open the :link[IAM Identity Center console]{href="https://console.aws.amazon.com/singlesignon"}.
2. Choose **Settings** in the left navigation pane.
3. On the **Settings** page, choose **Actions**, and then choose **Change identity source**.

![source](/static/labs/lab1/source.png)

4. Under **Choose identity source**, select **External identity provider**, and then choose **Next**.

![external](/static/labs/lab1/external.png)

5. Under **Configure external identity provider** in section **Service provider metadata**, do the following:
    - Copy link of **IAM Identity Center Assertion Consumer Service (ACS) URL** paste inside a text file
    - Copy link of **IAM Identity Center issuer URL** paste inside a text file

![copyurl](/static/labs/lab1/copyurl.png)

6. Under **Identity provider metadata**, under **IdP SAML metadata** select **Choose file** and then select the **metadata.xml** file you created in the previous step from Okta console "**Step 1: Obtain the SAML metadata from your Okta account**"

![choosefile](/static/labs/lab1/choosefile.png)

7. Choose **Next**
8. After you read the disclaimer and are ready to proceed, enter **ACCEPT**
9. Choose **Change identity source**

![accept](/static/labs/lab1/accept.png)

**Leave the AWS console open, you will continue using that console in the next step**

10. Return to the **Okta admin dashboard** and select the **Authentication** tab of the AWS IAM Identity Center app, then click **Edit** on the **Sign-on settings**

![signon](/static/labs/lab1/signon.png)

11. Under **Advanced Sign-on Settings** enter the following:
    - For **AWS SSO ACS URL** enter the value you copied for **IAM Identity Center Assertion Consumer Service (ACS) URL**
    - For **AWS SSO Issuer URL** enter the value you copied for **IAM Identity Center issuer URL**
12. Choose **Save**

![links](/static/labs/lab1/links.png)

You are now ready to provision users from Okta in IAM Identity Center. 

**Leave the Okta admin dashboard open, and return to the IAM Identity Center console for the next step**
::::

::::expand{header="Step 3: Configure SCIM Provisioning"}
1. Open the :link[IAM Identity Center console]{href="https://console.aws.amazon.com/singlesignon"}.
2. Choose **Settings** in the left navigation pane.
3. Locate the **Automatic provisioning** information box, and then choose **Enable**

![enable](/static/labs/lab1/enable.png)

4. In the **Inbound automatic provisioning** dialog box, copy each of the values and paste inside a text file.
    - **SCIM endpoint**
    - **Access token** 
    - Later in this tutorial you will paste these values to configure provisioning in Okta
5. Choose **Close**

![scim](/static/labs/lab1/scim.png)

6. Return to the **Okta admin dashboard**
7. On the **IAM Identity Center app** page, choose the **Provisioning** tab and click **Configure API Integration**
8. Select the check box next to **Enable API integration** to enable provisioning.
9. Configure Okta with the SCIM provisioning values from AWS IAM Identity Center that you **copied earlier in this tutorial**
    - In the **Base URL** field, enter the **SCIM endpoint** value.
    ::alert[Make sure that you remove the trailing forward slash at the end of the URL]
    - In the **API Token** field, enter the **Access token** value

![scimpaste](/static/labs/lab1/scimpaste.png)

10. Choose **Test API Credentials** to verify the credentials entered are valid. You will see the following message displayed

![scimverify](/static/labs/lab1/scimverify.png)

11. Choose **Save**
12. Under **Provisioning**, choose **To App**, Click **Edit**, and then select the **Enable check box** for each of the Provisioning features. For this tutorial, select all the options.
13. Choose **Save**

![toapp](/static/labs/lab1/toapp.png)


You are now ready to synchronize your users from Okta with IAM Identity Center.
::::

::::expand{header="Step 4: Push Users and Groups Assignmnet in Okta"}
1. In the **Okta IAM Identity Center app** page, choose the **Push Groups** tab. You can push both people and groups to AWS IAM Identity Center. For this lab we will **Push Groups**
2. Choose the **Push Groups** tab.
3. Click on **Push Groups** drop down and select **Find groups by name**

![push](/static/labs/lab1/push.png)

4. Search for group name by typing **AmazonQ** in the text box. Once the group appears, **select group** and click **Save**
5. The group status changes to **Active** after the group and its members have been pushed to IAM Identity Center.
::::

::::expand{header="Step 5: Provision Users From Okta"}
As part of this pre-configured workshop environment, users were created but not yet provisioned. Let's provision these users now that we've set up the group assignments in AWS IAM Identity Center.
1. In the **Okta IAM Identity Center app** page, choose **Assigments**.
2. Choose the **Provision Users** button.

![prov](/static/labs/lab1/prov.png)

3. Choose **OK** to the Provision User Notification.

![provusers](/static/labs/lab1/provusers.png)

You should see the user list populated by your Okta users inside AWS IAM Identity Center
::::
# Conclusion
In this lab, you successfully integrated Okta with AWS IAM Identity Center, establishing SAML-based Single Sign-On and automated user provisioning through SCIM. By configuring Okta as the external identity provider and pushing group assignments, you've created a streamlined, centralized way to manage user and groups via Okta.