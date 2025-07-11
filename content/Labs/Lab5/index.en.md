---
title: "Lab 5: Explore More Capabilities (Optional Lab)"
weight: 35
---

# Objective 
In this lab, you will configure and test various guardrails in Amazon Q Business, including LLM fallback settings, blocked words, and topic controls. These guardrails help ensure appropriate and secure interactions while maintaining control over the types of responses Amazon Q Business provides to users.
## Scenario Overview
You're a system administrator configuring Amazon Q Business for your organization. You need to:
   - Allow fallback to built-in knowledge when enterprise data isn't available
   - Prevent use of unprofessional terminology
   - Block discussions about specific topics
   - Test the guardrails to ensure they work as intended
::alert[These guardrails are essential for maintaining professional communication standards and controlling access to sensitive topics in enterprise environments.]{header="Important"}
## What You'll Do
1. Configure Amazon Q Business guardrails:
   - Enable LLM fallback for comprehensive responses
   - Set up blocked words for professional communication
   - Create topic controls for sensitive subjects
2. Test the guardrails:
   - Verify blocked word replacement
   - Test LLM fallback functionality
   - Confirm topic control restrictions
# Begin
::alert[For this lab, you'll need to use private browser windows when switching between users to ensure clean authentication sessions.]{header="Important"}

::::expand{header="Step 1: Adjust Amazon Q Business Guardrails"}
1. Using the left side navigation in the :link[Amazon Q Business console]{href="https://console.aws.amazon.com/amazonq/business"}, return to **workshop-application**
2. In the left menu, under **Enhancements**, choose **Admin controls and guardrails**
3. In the **Global controls** card, choose **Edit**

![guardrails](/static/labs/lab5/guardrails.png)

4. Check the **Allow Amazon Q to fall back to LLM knowledge** box
::alert[**Allow Amazon Q to fall back to LLM knowledge** enables Amazon Q Business to provide responses using its built-in knowledge when it cannot find relevant information in your connected data sources. This helps ensure users get helpful responses even when the exact information isn't in your documents.]{header="Understanding LLM Fallback"}
5. In the **Blocked words** section, enter the following words:
   - Gross
   - sinful
   - joint
   - foodie
6. Click **Add** after entering each word

![blocked](/static/labs/lab5/blocked.png)

7. At the bottom of the page, click **Save**
::alert[**Blocked words** prevent Amazon Q Business from using specific terms in its responses. This helps maintain professional communication and comply with your organization's content policies. When these words appear in questions, Amazon Q Business will find alternative ways to express the same concepts.]{header="Understanding Blocked Words"}
8. Under **Topic specific controls**, click **Create topic control**

![topic](/static/labs/lab5/topic.png)

9. Configure the topic control:
   - **Name**: slack-support
   - **Description**: Slack app control topic to be excluded from the responses based on the chat messages
   - **Example chat message**: How do I configure AWS Support App in Slack?
10. Click **Add New Rule**

![rule](/static/labs/lab5/rule.png)

11. Configure Rule 1:
    - For **Behavior**, select **Block Completely**
    - For **Messaging Shown**, enter "Your admin has blocked this with a topic control"
    - Note: You can optionally define specific users and groups for this control
12. Click **Save**

![save](/static/labs/lab5/save.png)

::alert[**Topic Controls** allow you to identify and manage how Amazon Q Business handles specific topics in conversations. You can block certain topics completely, show custom messages, or restrict topics to specific users or groups.]{header="Understanding Topic Controls"}
::::

::::expand{header="Step 2: Test Amazon Q Business Guardrails"}
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
7. In the chat window type **recommend a foodie joint in my neighborhood** to see the result below.

![foodie](/static/labs/lab5/foodie.png)

::alert[Notice how Amazon Q Business avoids using the blocked word "foodie" in its response and finds alternative ways to express restaurant recommendations.]{header="Blocked Words in Action"}
8. Prompt more question to further test Amazon Q chatbot for blocked words
9. Let's enter the following prompts and observe what happens, this will query the Amazon Q Business LLM for answers.
- How many people live in Sydney, Australia?

![aus](/static/labs/lab5/aus.png)

::alert[With LLM fallback enabled, Amazon Q Business can now provide answers using its built-in knowledge when information isn't found in your enterprise data. This is why you now get detailed responses about Sydney's population.]{header="LLM Fallback in Action"}

9. Next, lets test the Topic Controls. In the chat window type: "Tell me about AWS Support App in Slack."

![safety](/static/labs/lab5/safety.png)

::alert[The topic control blocks this query entirely and displays our custom message. This demonstrates how topic controls can prevent discussions about specific subjects, helping maintain appropriate boundaries in business communications.]{header="Topic Control in Action"}

10. Feel free to test more queries to explore how these guardrails work together
::::
# Conclusion
In this lab, you learned how to implement multiple layers of control in Amazon Q Business:
- Enabled LLM fallback to provide comprehensive responses when needed
- Configured blocked words to maintain professional communication
- Set up topic controls to manage access to specific subjects

These guardrails work together to create a secure and appropriate chat experience while ensuring users receive helpful, relevant information within your organization's guidelines.

::alert[Amazon Q Business's guardrails are flexible and can be customized to match your organization's specific requirements and compliance needs.]{header="Key Takeaway"}