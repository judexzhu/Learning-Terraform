# Variables in terraform

---

* Everything in one file is not great
* Use variables to hide secrets
  * You don't want the AWS credentials in your git repository
* Use variables for elements that might change
  * AMIs are different per region
* Use variables to make it yourself easier to reuse terraform files

#### All in one tf file

Here is the "instance.tf" we used in the previous chapter:

instance.tf

```json
provider "aws" {
  access_key = "ACCESS_KEY_HERE"
  secret_key = "SECRET_KEY_HERE"
  region     = "us-east-2"
}

resource "aws_instance" "example" {
  ami           = "ami-ae90b6cb"
  instance_type = "t2.micro"
}
```

#### Multiple \*.tf files

I'm going to split this one into multiple \*.tf files

First, let's create a provider.tf

provider.tf

```json
provider "aws" {
  access_key = "${var.AWS_ACCESS_KEY}"
  secret_key = "${var.AWS_SECRET_KEY}"
  region     = "${var.AWS_REGION}"
}
```

It contain the provider which obviously the "aws", the "access\_\_key", ""secret\_\_key" and the "region".

We are not going to fill them out the actual values, instead we replaced them with variables.

${var.Variable\_name} is the format of the terraform variables.

Then let's create another file named "vars.tf"

vars.tf

```json
variable "AWS_ACCESS_KEY" {}
variable "AWS_SECRET_KEY" {}
Variable "AWS_REFION" {
  default = "us-east-2"
}
```

This "vars.tf" is to declare the variables. It defines all the variables we used in the "provider.tf" file. If it's empty inside the "{}", that's mean we are not going to define the values, if there is a "default = " inside the "{}" , that mean we will give the variable a default value if no other value has been defined.

Then a "terraform.tfvars" need to be created, and inside of it, we will define all the values of the variables.

terraform.tfvars

```json
AWS_ACCESS_KEY = ""
AWS_SECRET_KEY = ""
AWS_REGION = ""
```

It's empty here, but you need put your values inside the "terraform.tfvars" file to make your terraform works.

> Tips: If you are using a git repository to save the terraform configuration files, remember to put this file name into the `.gitignore`, so you wont push this file which containers your "AWS\_ACCESS\_KEY" and "AWS\_SECRET\_KEY" into the git repositories.
>
> If your variables has a default value, you can leave it empty here, to make the variables using the default value. Otherwise, input a value here to override the defaults.

Last, we need make the "instance.tf" file

instance.tf

```json
resource "aws_instance" "example" {
  ami           = "ami-ae90b6cb"
  instance_type = "t2.micro"
}
```

Now , we have fours files in the same folder, and it look much clearly. But wait, we're not finished yet.

Let's do more. Let me show you how to change the "ami" into a lookup variable too.

#### Change "ami" into variable

First, we need to change the "instance.tf" file as below:

instance.tf

```json
resource "aws_instance" "example" {
  ami           = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"
}
```

The "provider.tf" would be exactly the same.

provider.tf

```json
provider "aws" {
  access_key = "${var.AWS_ACCESS_KEY}"
  secret_key = "${var.AWS_SECRET_KEY}"
  region     = "${var.AWS_REGION}"
}
```

The Change the vars.tf, add a new  "AMIS" variables as below:

vars.tf

```json
variable "AWS_ACCESS_KEY" {}
variable "AWS_SECRET_KEY" {}
Variable "AWS_REGION" {
  default = "us-east-2"
}
variable "AMIS" {
  type = "map"
  default = {
    us-east-1 = "ami-a60c23b0"
    us-east-2 = "ami-ae90b6cb"
    us-west-1 = "ami-96f1dcf6"
    us-west-2 = "ami-7646530f"
  }
}
```

The variables type is "map"  and it has "key:value" pairs.

```json
variable "AMIS" {
  type = "map"
  default = {
    us-east-1 = "ami-a60c23b0"
    us-east-2 = "ami-ae90b6cb"
    us-west-1 = "ami-96f1dcf6"
    us-west-2 = "ami-7646530f"
  }
```

Let's look back to the "ami" inside the "instance.tf" file.

```json
ami ="${lookup(var.AMIS, var.AWS_REGION)}"
```

It has two parameters, one is "var.AMIS" and the second is "var.AWS\_REGION".

so it will first get the value of "var.AWS\_REGION", for example, let's say it would be "us-east-2", then it take the value "us-east-2" as the key into the variable "AMIS" and lookup for the value, which is "ami-ae90b6cb". Finally, it give the value it looked up to the "ami"

```json
ami           = "${lookup(var.AMIS, var.AWS_REGION)}"
```

to

```json
ami           = "ami-ae90b6cb"
```

And don't forget the file where we put all the variables value inside,"terraform.tfvars"

terraform.tfvars

```json
AWS_ACCESS_KEY = ""
AWS_SECRET_KEY = ""
AWS_REGION = ""
```

Let's make some demo in the next chapter.

