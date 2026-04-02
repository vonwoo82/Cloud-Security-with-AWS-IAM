# Cloud-Security-with-AWS-IAM

Demonstrating how to use AWS IAM to control access and permissions settings in our AWS Account.

Services used were Amazon EC2 and AWS IAM. Key concepts demonstrated include IAM users, policies, user groups and account aliases.

<img width="1463" height="949" alt="aws-security-iam_1c864649" src="https://github.com/user-attachments/assets/9aa6f1fb-ec30-45cf-8970-80152b168789" />

-------------------------------------------------------------------------------------------------------------------------------------------------------
**Tags**

What I did in this step

In this step, I launched two EC2 instances because we need to boost computing power.

Understanding tags

Tags are organizational tools that lets lable our resources. They are helpful for grouping resources, cost allocations and applying policies for all resources with the same tag. 

My tag configuration

The tag i've used on my EC2 instances is called Env, which stands for Environment. The value I've assigned for our instances are produciton and develpment.

<img width="965" height="493" alt="aws-security-iam_2e0e5a5d" src="https://github.com/user-attachments/assets/b9818bdf-3f7e-4f67-9b18-9400dd50fcd3" />


**IAM Policies**

What I did in this step

In this step, I will use IAM policies to control the access level of a new NextWork intern because they should have access to the development enviroment (i.e. the development instance) but not the production environment.

Understanding IAM policies

IAM Policies are like rules that determine who can do what in our AWS Account. We're using policies today to control who has access to our production/environment instance

**The policy I set up**

For this project, I’ve set up a policy using JSON

Policy effect

I’ve created a policy that allows the policy holder (i.e. the inter) to have persmission to do anything they want to any instance tagges with "Development", They can also see information for any instance, but they're denied access to deleting/creating tags for instance as well. 

Understanding Effect, Action, and Resource

The Effect, Action, and Resource attributes of a JSON policy means whether or not the policy is allowing/denying action (i. e Effect); what the policy holder can or cannot do (i.e. Action); and the specific AWS resources that the policy relate to (i.e. Resource)

------------------------------------------------------------------------------------------------------------------------------------------------------------

**My JSON Policy**

<img width="1463" height="949" alt="aws-security-iam_1c864649" src="https://github.com/user-attachments/assets/39690eec-a3cf-4e46-9b82-b8bd1dad31ca" />

------------------------------------------------------------------------------------------------------------------------------------------------------------

**Account Alias**

What I did in this step

In this step, I set up an Account Alias which is like a nickname for our AWS console's login. This is because an account alias make it simpler for our users to login.

Understanding account aliases

An account alias is simply a nickname for our AWS Account! Instead of a long account ID, we can now reference our account alias instead!

Setting up my account alias
Creating an account alias took me 30 seconds - its a imple configuration in the IAM dashboard. ... Now, my new AWS console sign-in URL uses the alias instead of my account ID

<img width="622" height="327" alt="aws-security-iam_0eb4439b" src="https://github.com/user-attachments/assets/7e3bc54a-8f6f-4b37-a5f5-cdc4454d1531" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------

**IAM Users and User Groups**

What I did in this step


In this step, I will  set up two IAM resources - IAM users, and IAM users groups. This is because IAM users are the logins for people that want access to our AWS account, while user groups are like folders to manage users that have the same level of access.

Understanding user groups

IAM user groups are like folders that collect IAM users so that you can apply permission settings at the group levels

Attaching policies to user groups

I attached the policy I created to this user group, which means any user created inside this group will automatically get the permissions attached to our NextWorkDevEnvironmentPolicy IAM Policy

Understanding IAM users

IAM users are people or entities that have access/can login to our AWS account

------------------------------------------------------------------------------------------------------------------------------------------------------------

**Logging in as an IAM User**

Sharing sign-in details

The first way is to email sign-in instructions to the user, while the second way is to download the .csv file with the sing-in details inside

Observations from the IAM user dashboard

Once I logged in as my IAM user, I noticed that our user is already denied access to panels on the main AWS console dashboard. This is because we only set up permissions to our development EC2 instance, so our interns wouldn't have access to anything else and even see anything else.

<img width="1416" height="632" alt="aws-security-iam_6f2ab446" src="https://github.com/user-attachments/assets/4dcdd401-76c8-4e98-bf11-40957a95f078" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------

**Testing IAM Policies**

What I did in this step

In this step, I will login to our own AWS account as the intern and test access to the production and development instances because we want to make sure our intern doesnt have the ability to do anything that affect our production environment. 

Testing policy actions

I tested my JSON IAM policy by attempting to stop both development and production instances.

Stopping the production instance

When I tried to stop the production instance, we were met with an error. This was because our production instance is tagged with the production label, whis is outside of the scope of our permission policy - interns are only allowed to do things to the development instance.

<img width="804" height="332" alt="aws-security-iam_0e7a9d6a" src="https://github.com/user-attachments/assets/299acd9b-cffb-4aba-8fc5-f03351df3f46" />


**Stopping the development instance**

Next, when I tried to stop the development instance, we successfully saw the instance change to stopping and then stopped.  This was because our permission pollicy allows the intern (i.e. users in the nextwork-dev-group) to stop instances. 

<img width="1170" height="225" alt="aws-security-iam_1811801c" src="https://github.com/user-attachments/assets/1ead3e9e-b62b-44d9-8264-c18123b9eb4e" />

---------------------------------------------------------------------------------------------------------------------------------------------------------------

**IAM Policy Simulator**

To extend my project, I'm going to test our permission policies in a safer and more controlled way - a tool called the IAM. Policiy Simulator! I'm doing this because having to stop instances and log into AWS Accounts as other users are a bit disruptive. Lets find a more efficient way.

Understanding the IAM Policy Simulator

The IAM Policy Simulator is a tool that lets us simulate actions and test permissions settings by defining a specific user/group/role and the action we want to test for. It's useful for saving time when testing permission settingss. No more logging into another user or actually stopping resources. 

How I used the simulator

I set up a simulation for whether our dev user group has permission to Stop instances or Deletetags. The results were denied for both - we had to adjust the scope of the EC2 instances to ones that are tagged with "Developmenet". Once we applied that tag, permission was allowed. 

<img width="1028" height="188" alt="aws-security-iam_069d8a621" src="https://github.com/user-attachments/assets/432a50fe-0e6c-4ca3-83a9-ae412564ab66" />

