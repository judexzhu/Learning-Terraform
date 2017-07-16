# Provisioning on Linux

---

In this Demo, we will

1. Using terraform to spin up an Ubuntu host 
2. Generate an SSH public & private key pair
3. Using File Uploads to upload a bash script into the Instance
4. Using remote exec to execute the script

Let's create a new folder with some tf files, here I will create a "demo-2" folder for the demo of the Linux host, and another "demo-2b" folder for Windows host later.

#### Check the files

Under the "demo-2" folder , you will have below files:

instance.tf

```json
resource "aws_key_pair" "mykey" {
  key_name = "mykey"
  public_key = "${file("${var.PATH_TO_PUBLIC_KEY}")}"
}

resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"
  key_name = "${aws_key_pair.mykey.key_name}"

  provisioner "file" {
    source = "script.sh"
    destination = "/tmp/script.sh"
  }
  provisioner "remote-exec" {
    inline = [
      "chmod +x /tmp/script.sh",
      "sudo /tmp/script.sh"
    ]
  }
  connection {
    user = "${var.INSTANCE_USERNAME}"
    private_key = "${file("${var.PATH_TO_PRIVATE_KEY}")}"
  }
}
```

You can see, here we using the file load to upload a file called "scrpt.sh" to the instance.

Then we will execute it by remote exec. "chmod +x /tmp/script.sh" make this "script.sh" executable and then "sudo /tmp/script.sh" to apply the script.

Also we use connection with SSH key pair "mykey"  ssh to the instance to execute the script.

Let's see what is inside the "script.sh":

script.sh

```json
#!/bin/bash
apt-get update
apt-get -y install nginx
```

It's just a simple bash shell script, which will run "apt-get update" first, then install the nginx with sudo.

provider.tf

```json
provider "aws" {
    access_key = "${var.AWS_ACCESS_KEY}"
    secret_key = "${var.AWS_SECRET_KEY}"
    region = "${var.AWS_REGION}"
}
```

This file is the exactly the same with the previous demos.

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

variable "PATH_TO_PRIVATE_KEY" {
  default = "mykey"
}
variable "PATH_TO_PUBLIC_KEY" {
  default = "mykey.pub"
}
variable "INSTANCE_USERNAME" {
  default = "ubuntu"
}
```

Here in the "vars.tf". We added 3 more variables.

1. "**PATH\_TO\_PRIVATE\_KEY**", and it's value is "mykey". That means under the same folder with these tf files. we need a ssh private key with the file name "mykey".
2. "**PATH\_TO\_PUBLIC\_KEY**", and it's value is "mykey.pub". That means under the same folder with these tf files. we need a ssh public key with the file name "mykey.pub".
3. "**INSTANCE\_USERNAME**", and it's value is "ubuntu". For we're going to spin up an Ubuntu host, as we talked before, the default user of the Ubuntu server is "ubuntu".

Don't forget to create the "terraform.tfvars" and put your "AWS\_ACCESS\_KEY" and "AWS\_SECRET\_KEY"  inside it.

![](/images/vardemo-tfvarsfile.png)

Next, let's generate the ssh key pair.

#### Generate SSH Key pair

If you are working on Linux system or Mac, generate the SSHkey pair is easy.

Just run 

```bash
ssh-keygen -f mykey
```



