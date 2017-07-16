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

Here is the "file uploads"resource part of an instance.tf.

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





