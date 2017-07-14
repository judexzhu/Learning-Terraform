# Installing Terraform

---

Go to [www.terraform.io](https://www.terraform.io/)

![](/images/terrformwebsite.png)

Click Download, then chose your Operation System

![](/images/selectdownloados.png)

For I'm using windows 10 64bit, I will download the Windows 64bit version. But disregard what your OS is, the dowload is always a zip file, all you need to do is to download this zip file &gt; extract &gt; move the terraform binary to the $path or add the terrform binary file location into the $path.

The Current terraform version is 0.9.11



## On Windows

Here is what the Zip file looks like, and inside of it , you will only see one file "terraform.exe"\(Windows Version\)

![](/images/terraformzip.png)

![](/images/terraformexe.png)

Go to **Control Panel\System and Security\System\Advanced system settings\Environment Variables...**

![](/images/env.png)

Click Edit the **Path** under the **System variables **box

Add the Path to your "terraform.exe". For example, I put the terraform.exe under "C:\Users\Jude\Downloads\", so it would be looks like:

![](/images/addterraformpath.png)

Click "OK" to apply the settings, then open a windows "Command Prompt", type "terraform" and press enter, if you saw below messages, then your terraform has been successfully installed.

![](/images/terraforminstalledwin.png)



