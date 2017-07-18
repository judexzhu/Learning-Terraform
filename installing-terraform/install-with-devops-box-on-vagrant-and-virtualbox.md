# Install with Devops-box on Vagrant and VirtualBox

---

Install Terraform on the windows is not the best choice.

If you can run your pc / laptop on Linux, like Ubuntu, or on MAC, it will be much better than the windows.

But somehow, we can use Vagrant and VirtualBox to spinning up a local vm named "devops-box" on Windows which the terraform, packer, awscli have been already pre-installed.

Okay, let's work on it.

#### Install VirtualBox

VirtualBox is a powerful x86 and AMD64/Intel64 virtualization product for enterprise as well as home use.

Go to [https://www.virtualbox.org/](https://www.virtualbox.org/), download and install the Windows hosts Version.![](/images/installdevboxvb.png)

> Note: All install steps apply the default option.

#### Install Vagrant

Vagrant is a tool for building and managing virtual machine environments in a single workflow.

Go to [https://www.vagrantup.com/](https://www.vagrantup.com/), download and install the Windows Version.

> Note: All install steps apply the default option.

![](/images/installdevboxvagrant.png)

#### Install Git



Go to [https://git-scm.com/downloads](https://git-scm.com/downloads), download and install the Windows Version.

> Note: All install steps apply the default option.

![](/images/installdevboxgit.png)

#### Git Clone Vagrant file

After installing the VirtualBox, Vagrant and git. 

Open a Command Prompt by pressing "WIN+R" and run "cmd". Let's say, I want to clone the folder and build the vm under the "C:\".

Change the directory to "C:" and run :

```bash
git clone https://github.com/judexzhu/devops-box.git
```

Here is what it looks like:![](/images/installdevboxgitclone)

#### Vagrant Up

Bring the devops-box vm up by simply running 

```bash
vagrant up
```

It will take some time. After finish, run below command to check the ssh login information 

```bash
vagrant ssh-config
```

You will get the information like below:![](/images/installdevboxvagrantsshconfig.png)How to login the devops-box:

1. Using ip address 127.0.0.1
2. SSH port is 2222
3. Here is the private-key which used to login the vm

Let's open a ssh termial, I like to use Xshell a lot.

> Tips: Xshell can be download from here. [https://www.netsarang.com/download/down\_xsh5.html](https://www.netsarang.com/download/down_xsh5.html)
>
> It also has a nice installation guild.

Let's create a new session

![](/images/installdevboxxshellnewsession.png)

![](/images/installdevboxsessionauth.png)

1. On connection, give this session a name like "devops-box".
2. In the "Host" box fill with "127.0.0.1".
3. Set the "Port Number" to "2222".
4. Go to Authentication. 
5. Set the "Method:" to "Public Key".
6. Set "User Name:" to "ubuntu".
7. on the "User Key:", use "Browse.." button on the right to input the private key and select it. Using "`vagrant ssh-config`" to get the path of private key.
8. Click "OK" to finish.

You can see from below image that we can success login the VM, also the "terraform" has already been installed.![](/imagess/installdevboxlogin.png)

---

### Vargrant Cheat Sheet

Here is some useful command when using vagrant, wish they will be helpful.

Typing \`vagrant\` from the command line will display a list of all available commands.

Be sure that you are in the same directory as the Vagrantfile when running these commands!



