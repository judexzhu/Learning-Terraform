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
Variable "AWS_REFION" {
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



