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
variable "AWS_REGION" {
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

Let's run `terraform plan`and you will see the result like this:

```
+ aws_instance.example
    ami:                          "ami-ae90b6cb"
    associate_public_ip_address:  "<computed>"
    availability_zone:            "<computed>"
    ebs_block_device.#:           "<computed>"
    ephemeral_block_device.#:     "<computed>"
    instance_state:               "<computed>"
    instance_type:                "t2.micro"
    ipv6_address_count:           "<computed>"
    ipv6_addresses.#:             "<computed>"
    key_name:                     "<computed>"
    network_interface.#:          "<computed>"
    network_interface_id:         "<computed>"
    placement_group:              "<computed>"
    primary_network_interface_id: "<computed>"
    private_dns:                  "<computed>"
    private_ip:                   "<computed>"
    public_dns:                   "<computed>"
    public_ip:                    "<computed>"
    root_block_device.#:          "<computed>"
    security_groups.#:            "<computed>"
    source_dest_check:            "true"
    subnet_id:                    "<computed>"
    tenancy:                      "<computed>"
    volume_tags.%:                "<computed>"
    vpc_security_group_ids.#:     "<computed>"


Plan: 1 to add, 0 to change, 0 to destroy
```

That means we have successfully use our variable with separate tf files and "terraform.tfvars" which containers the variable values to create the same infrastructure as our "First Steps".

Let's run terraform apply :

```
aws_instance.example: Creating...
  ami:                          "" => "ami-ae90b6cb"
  associate_public_ip_address:  "" => "<computed>"
  availability_zone:            "" => "<computed>"
  ebs_block_device.#:           "" => "<computed>"
  ephemeral_block_device.#:     "" => "<computed>"
  instance_state:               "" => "<computed>"
  instance_type:                "" => "t2.micro"
  ipv6_address_count:           "" => "<computed>"
  ipv6_addresses.#:             "" => "<computed>"
  key_name:                     "" => "<computed>"
  network_interface.#:          "" => "<computed>"
  network_interface_id:         "" => "<computed>"
  placement_group:              "" => "<computed>"
  primary_network_interface_id: "" => "<computed>"
  private_dns:                  "" => "<computed>"
  private_ip:                   "" => "<computed>"
  public_dns:                   "" => "<computed>"
  public_ip:                    "" => "<computed>"
  root_block_device.#:          "" => "<computed>"
  security_groups.#:            "" => "<computed>"
  source_dest_check:            "" => "true"
  subnet_id:                    "" => "<computed>"
  tenancy:                      "" => "<computed>"
  volume_tags.%:                "" => "<computed>"
  vpc_security_group_ids.#:     "" => "<computed>"
aws_instance.example: Still creating... (10s elapsed)
aws_instance.example: Still creating... (20s elapsed)
aws_instance.example: Still creating... (30s elapsed)
aws_instance.example: Creation complete (ID: i-00154990593b96c58)

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

Let's go to the AWS EC2 service to check.![](/images/vardemo-instancerunning.png)

An instance is running now ,and every information matches what we describe in the multiple tf files.

Then as usually , let's run "terraform destroy" to avoid fees.

```
Do you really want to destroy?
  Terraform will delete all your managed infrastructure.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

aws_instance.example: Refreshing state... (ID: i-00154990593b96c58)
aws_instance.example: Destroying... (ID: i-00154990593b96c58)
aws_instance.example: Still destroying... (ID: i-00154990593b96c58, 10s elapsed)
aws_instance.example: Still destroying... (ID: i-00154990593b96c58, 20s elapsed)
aws_instance.example: Still destroying... (ID: i-00154990593b96c58, 30s elapsed)
aws_instance.example: Still destroying... (ID: i-00154990593b96c58, 40s elapsed)
aws_instance.example: Still destroying... (ID: i-00154990593b96c58, 50s elapsed)
aws_instance.example: Destruction complete

Destroy complete! Resources: 1 destroyed.
```

Let's try it again, but this time let's see  what if we remove the "terraform.tfvars"  file. That mean we will define the variables without give them the values.

![](/images/vardemo-wovalues.png)

It will prompt those variable without values and you can put the values behind it. You see, I've put some wrong values, so it will got an error and stop without doing anything.

