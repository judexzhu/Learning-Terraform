#### What is terraform

> From official website

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.

Configuration files describe to Terraform the components needed to run a single application or your entire datacenter. Terraform generates an execution plan describing what it will do to reach the desired state, and then executes it to build the described infrastructure. As the configuration changes, Terraform is able to determine what changed and create incremental execution plans which can be applied.

The infrastructure Terraform can manage includes low-level components such as compute instances, storage, and networking, as well as high-level components such as DNS entries, SaaS features, etc.

Examples work best to showcase Terraform.  
The key features of Terraform are:

### [»](https://www.terraform.io/intro/index.html#infrastructure-as-code)Infrastructure as Code {#infrastructure-as-code}

Infrastructure is described using a high-level configuration syntax. This allows a blueprint of your datacenter to be versioned and treated as you would any other code. Additionally, infrastructure can be shared and re-used.

### [»](https://www.terraform.io/intro/index.html#execution-plans)Execution Plans {#execution-plans}

Terraform has a "planning" step where it generates an_execution plan_. The execution plan shows what Terraform will do when you call apply. This lets you avoid any surprises when Terraform manipulates infrastructure.

### [»](https://www.terraform.io/intro/index.html#resource-graph)Resource Graph {#resource-graph}

Terraform builds a graph of all your resources, and parallelizes the creation and modification of any non-dependent resources. Because of this, Terraform builds infrastructure as efficiently as possible, and operators get insight into dependencies in their infrastructure.

### [»](https://www.terraform.io/intro/index.html#change-automation)Change Automation {#change-automation}

Complex changesets can be applied to your infrastructure with minimal human interaction. With the previously mentioned execution plan and resource graph, you know exactly what Terraform will change and in what order, avoiding many possible human errors.



#### Terraform vs Ansible, Chef, Puppet, SaltStack

* Ansible, Chef, Puppet, SaltStack have a focus on automating the **installation and configuration** of software
  * Keeping the **machiines** in compliance , in a certain state
* Terraform can automate provisioning of the **infrastructure** itself
  * eg. Using the AWS, DigitalOcean, Azure API
  * Works well with automation software like ansible to install software after the infrastructure is provisioned

 







