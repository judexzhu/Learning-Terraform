# Variables Demo

---

Let's have a look into the demo that how you can use variables in the terraform.

Create a folder you like, here I'm going to use "demo-1"

and Inside the "demo-1" folder, we will have three terraform files inside it, as what we describe in previous chapter.

instance.tf

```json
resource "aws_instance" "example" {
  ami           = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"
}
```

provider.tf

```json
provider "aws" {
    access_key = "${var.AWS_ACCESS_KEY}"
    secret_key = "${var.AWS_SECRET_KEY}"
    region = "${var.AWS_REGION}"
}
```

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

Current now , it will look like below

![](/images/vardeminfra1.png)

We do not have the value of the variables yet, so let's create the "terraform.tfvars" file and put our values inside it.

In this demo, you only need put "AWS\_ACCESS\_KEY" and "AWS\_SECRET\_KEY" variable values inside it, for the variable "AWS\_REGION" has a default values, and the variable "AMIS" can look up the map with the value of "AWS\_REGION" and get its  value by itself.

![](/images/vardemo-tfvarsfile.png)

> Attention: This is the file which you don't want to put it on your git repository, for it contains the sensitive information, most important, the access\_\_key and secret\_\_key. Anyone have these key pair can use them to create, build or destroy your aws infrastructure. Please be more careful with it.
>
> Typically, you want to put a ".gitignore" file inside your repository, and put "terraform.tfvars" inside it, depends on my repository structure, here is how it looks like.\(We will put more files in the ".gitignore" later. \)

.gitignore

```json
*/terraform.tfvars
```


