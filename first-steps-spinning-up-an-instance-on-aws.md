# First Steps in Terraform - Spinning up an instance

---

#### Create an terraform file:

 named "instance.tf"

```
provider "aws" {
  access_key = "ACCESS_KEY_HERE"
  secret_key = "SECRET_KEY_HERE"
  region     = "us-east-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0d729a60"
  instance_type = "t2.micro"
}
```

`provider` : This is the terraform provider, for we are going to create a ec2 instance , it would be `aws`.

`ACCESS_KEY_HERE`: Here your put in the "**Access key ID**" of the "terraform" IAM account from the previous steps.

`SECRET_KEY_HERE`: Here your put in the "**Secret access key**" of the "terraform" IAM account from the previous steps.

`region` : You can chose whatever region you like\( might the nearest to your local\). Here I chose "`us-east-2`" Ohio.

`example`: This is the instance name.

`ami`: The image id we are using to create our instance. Different OS with different region has different ami. I will show you to how to get the correct ami for your instance later.

`instance_type` : Choose "t2.micro", so you don't have to pay for them. If for production, You can chose whatever you need.  



Edit this file as you need, use whatever editor you feel comfortable , I like using **Microsoft Visual Studio Code**, it's super powerful, intergrate  a nice git function and a intergrated terminal.



Get the AMI 

Now we are going to launch a newest version of Ubuntu with a Free tier t2.micro type aws instance.

Let's go to Ubuntu Amazon EC2 AMI Locator, here is the link : [http://cloud-images.ubuntu.com/locator/ec2/](http://cloud-images.ubuntu.com/locator/ec2/)

In the search box , type "us-east-2" and "zesty"

> Tips: "us-east-2" is my aws region, you need change it to the same region in your `instance.tf` file.
>
> "zesty" is the ubuntu 17.04 code name.

![](/images/ec2amilocator.png)

