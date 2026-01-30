#Today I focused on understanding the IAM authentication and IAM resources that are provides by AWS.
#I learnt that we must follow the IAM Security Best Practices:

        Follow the principle of least privilege by granting only the permissions required.

        Avoid using the root account for daily operations; lock it down.

        Enable Multi-Factor Authentication (MFA), especially for the root user and privileged accounts.

        Use temporary credentials via IAM Roles and AWS STS instead of long-term credentials. 
#Moreover in IAM there is IAM resources: IAM users,IAM roles,IAM groups and IAM policies

#In IAM policies it has the following elements, which are(Version, statement,effect,principal,action,resources,conditions) this elements constitutes and make up what the permissions are allowed and Denied

#IAM policies have an implicit deny(default deny) that is override by the explicit allow which in turn is overriden with the explicit deny  
