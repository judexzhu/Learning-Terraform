# Variables in terraform

---

* Everything in one file is not great
* Use variables to hide secrets
  * You don't want the AWS credentials in your git repository
* Use variables for elements that might change
  * AMIs are different per region
* Use variables to make it yourself easier to reuse terraform files

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



