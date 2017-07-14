# Fish Steps in Terraform - Create IAM User

---

* Spinning up instance on AWS
* Sign up/ Open an AWS account
  * Using t2.micro instance free tier  
* Create IAM admin user
* Create terraform file to spin up t2.micro instance 
* Run terraform apply
  * Alway use terraform destroy to destroy your infrastructure after using to avoid charging 

#### Create an AWS accunt

Go to [https://aws.amazon.com](https://aws.amazon.com/) to create your own account

then with a few steps about detail information input, you create your aws account

next step is to sign in to the console

If everything runs well, you should see a web console like this:![](/images/awswebconsole.png)

Make sure you're using the "t2.micro" tier every time with the lab and shutdown everything after the lab, so you don't have to pay for them.

#### Create an IAM account for terraform to provision the infrastructure

scroll down the web console until you find the  **IAM **service under the **Security, Identity & Compliance** filed.

Here:

![](/images/awsiamservice.png)

The Dashboard would look like

![](/images/iamdashboard.png)Click **Users **from the left panel, click **Add user**

![](/images/iamadduser.png)

1. Give the new user a name , for we are using this account for learning terraform, "terraform" would be a good choice.
2. for we would only use account to run with the terraform, An **access key ID** and a **secret access key** are must have, we don't need the  the user account to login from the AWS Management Web console.
3. Click "**Next Permissions**"

![](/images/iamcreateuser.png)

On the next page

1. Select **Attach existing policies directly**
2. then choose the "**Administrator Access**" policy
3. Click "**Next: Review**"

![](/images/iamuserpermission.png)

There is nothing to set in the "Review" Page, if you find something wrong, use the "Previous" button to go back to change the settings.![](/images/iamuserreview.png)

Click "**Create User**"

On the "**Complete**" page, be sure you record the Access key ID and Secret access key. You can take a snapshot , click the "Download.csv" or take a photo with your cellphone.

> Important: This would be the last time you see these credentials and be available to download them. Make sure you saved them well and keep them private.
>
> But if you lost the "Secret access key", don't worry, you can always go to the IAM dashboard, delete the old one, then create the a new one, don't forget to replace the values in your terraform files.

![](/images/iamusercomplete.png)After the user has been created , let's go the "EC2" services and use terrfrom to spinning up an ec2 instance.

