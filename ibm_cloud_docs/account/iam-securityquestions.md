---

copyright:

  years: 2018, 2023

lastupdated: "2023-02-09"

keywords: security questions, MFA, multifactor authentication, login security

subcollection: account

---

{{site.data.keyword.attribute-definition-list}}

# Enabling MFA security questions for a user
{: #questions}

As an Administrator on the IAM Identity Service or All IAM Account Management services, you can enable the multifactor authentication (MFA) option that prompts a user for security questions and answers at login. This type of legacy account-based MFA is required only for the account where the setting is enabled and is available only for accounts with classic infrastructure.
{: shortdesc}

For more information about your MFA options, see [Types of multifactor authentication](/docs/account?topic=account-types).

## Before you begin
{: #security-question-access}

If you have any of the following types of access, you can update this setting for other users in your account:

* Administrator role on the IAM Identity Service or All IAM Account Management services
* You are an ancestor in the classic infrastructure hierarchy for the user and you have the Manage users classic infrastructure permission assigned

You can manage this setting for yourself if you have the **User-managed login** setting turned on in your User detials.

To turn on security questions for a user, they must first set up [security questions](#security-questions-setup) and answers.
{: important}

## Setting up security questions
{: #security-questions-setup}

Users can set up answers to three security questions for extra authentication at login. You must set up your security questions and answers before you or administrator can enable this MFA requirement for you.

To set up your security questions, complete the following steps:
1. From the console, go to Go to **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Profile and settings**, and select **Login settings**.
2. In the Security questions seciton, click **Set up**.
3. Select the questions that you want to have and answer them. You must answer all three security questions.
4. Click **Save** when you're finished.

To update your security questions, click **Edit**.
{: tip}


## Enabling security questions
{: #enable-security-question}

Complete the following steps to turn on MFA security questions for a user:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Users**.
2. Select a user from the list.
3. From the **User details** page in the **Manage user's login** section, set the **Require MFA security questions at login** option to **On**.

If the toggle **Require MFA security questions at login** is disabled and you can't turn it on or off, you don't have access to manage the MFA factor. You must be the account owner or have the **User-managed login** setting turned on. Contact your account owner or administrator to get access to turn on the User-managed login setting. To check if User-managed login is turned on, go to **Manage > Access (IAM) > Users** and click on yourself. View the User-managed login section.
{: tip}
{: note}
