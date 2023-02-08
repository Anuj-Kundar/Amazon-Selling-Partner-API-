# To do:

## Overview:
1. Create a [Seller Central](https://sellercentral.amazon.com/) account (or log into an existing one if you have it)
2. Complete your developer application from within Seller Central
3. Register your Selling Partner application, using [AWS IAM](https://aws.amazon.com/iam/) and Seller Central
  ![image](https://user-images.githubusercontent.com/89484481/217536099-827fc3a6-c511-4835-b360-10447c2ea565.png)


# In detail:
Requirements: Professional-level Amazon Seller account to develop Amazon Marketplace apps.
>note :Apply for a developer account from within the Seller Central account.

Create and configure IAM policies and entities
================================================
[refer docs](https://developer-docs.amazon.com/sp-api/docs/creating-and-configuring-iam-policies-and-entities)

Complete Developer Application in Seller Central
================================================
1. apply for a Amazon Marketplace developer account! Go to [Seller Central](https://sellercentral.amazon.com/) and then click       Partner Network > Develop Apps
2. Clicking "Proceed to Developer Profile" will land you on another hefty form with a few different sections. 
then "Contact Information".
3. Fill out the form and click "Submit" at the bottom of the page.
4. Go to "Developer central" and  Create new app.
 ![image](https://user-images.githubusercontent.com/89484481/217552820-109fa024-4819-42a7-8eb6-eeffdc8b91ec.png)

Registering your Selling Partner API application
================================================

The SP API documentation has a [guide](https://developer-docs.amazon.com/sp-api/docs/registering-your-application) on how to do this, but alternate process looks like this:

Overview:
1.  Login to AWS account.
2.  Create an IAM user that will eventually be connected to your Selling Partner API developer credentials.
3.  Create an inline policy on the IAM user that grants the user access to the SP API (this is where I'm telling you to do something different from what Amazon's instructions say—I'll explain why below).
4.  Register your new SP API application! (Your developer application has to be approved first.)

For steps 1 and 2, follow [Amazon's guide](https://github.com/amzn/selling-partner-api-docs/blob/main/guides/en-US/developer-guide/SellingPartnerApiDeveloperGuide.md#registering-your-application), but stop before their [Step 3](https://github.com/amzn/selling-partner-api-docs/blob/main/guides/en-US/developer-guide/SellingPartnerApiDeveloperGuide.md#step-3-create-an-iam-policy). Amazon says to create an IAM policy and IAM role, attach the policy to the role, and then add an STS policy to your IAM user. But as discussed in [this GitHub issue](https://github.com/amzn/selling-partner-api-docs/issues/128), that adds an extra (seemingly unnecessary) step to the SP API authentication process. We're going to set things up in a way that allows you to skip that STS step.

Once you've completed Step 2, navigate to the IAM user you just created by clicking on its username in the list of IAM users. Then to grant the user access to the SP API:

1.  Click **Add inline policy** in the upper right
2.  Select the **JSON** tab
3.  Paste the following JSON into the editor:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "execute-api:Invoke",
            "Resource": "arn:aws:execute-api:*:*:*"
        }
    ]
}
```
    
4.  Click **Review Policy**, and name your policy .
5.  Click **Create policy**

 Here we are Done configuring IAM and can ignore steps 3-5 of Amazon's guide on registering your SP API application.



