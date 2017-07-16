# Provision Software

---

* There are 2 ways to **provision software** on your instances
* You can build your **own custom AMI** and bundle your software with the image
  * **Packer** is a great tool to do this
* Another way is to boot **standardized AMIs**, and then install the software on it you need
  * Using **file uploads**
  * Using **remote exec**
* Using** automation tools** like chef, puppet or ansible
* **Current state** for terraform with automation
  * **Chef is integrated** with terraform, you can add chef statments
  * You can run **puppet agent **using remote-exec
  * For Ansible, you can first run terraform, and **output **the IP addresses, then run **ansible-playbook **on those hosts
    * This can be automated in a workflow script
    * There are **3rd party initiatives** integrating Ansible with terraform

#### File Uploads

Here is the example "file uploads"resource part of an instance.tf.

```json
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"

  provisioner "file" {
    source = "app.conf"
    destination = "/etc/myapp.conf"
  }
}
```

If you want to upload a file into the instance, you have to add a **provisioner "file" {} **inside the "aws\_instance" resource. **Source = "app.conf"** \_that means we have a file "app.conf" next to our tf files and we want to upload this file to the aws\_instance. **destination = "/etc/myapp.conf"** is the destination where we want to put the file inside the instance.

**File Uploads** can be used in conjunction with **remote-exec** to execute a script. That means you can use "File uploads" to upload a script into the instances, then use the "remote-exec" to execute the script.

The provisioner may user **SSH **\(for Linux\) or **WinRM **\(for Windows\).

#### Connection

So to use SSH, you can use "**connection**":

Here is a example:

```json
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"

  provisioner "file" {
    source = "script.sh"
    destination = "/opt/script.sh"
    connection {
      user = "${var.instance_username}"
      password = "${var.instance_password}"
    }
  }
}
```

In this example, terraform will use ssh to connect to the instance by using "user" & "password" after spinning up the Ubuntu instance. 

> Tips: The default type of connection is "SSH". If you want to use the other types, you have to define it in the "connection {}".

When spinning up instance on AWS, **ec2-user** is the default user for Amazon Linux and **ubuntu **for Ubuntu Linux.

Typically on AWS, you'll use SSH keypairs:

Here is a example:





