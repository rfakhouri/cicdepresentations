# Infrastructure as Code
## Using Terraform to Automate the Cloud

---

# What is Terraform?

------

It is an open source tool that codifies APIs into declarative configuration files that can be shared amongst team members, treated as code, edited, reviewed, and versioned.

---

# HashiCorp Configuration Language (HCL)

---

# What is that?

------

It's a declarative configuration language created by HashiCorp*  
_The company that created Terraform_

---

# What does that mean?

------

You define the *state* of your infrastructure and Terrafrom figures out what commands you need to run and in what order to create that state	
This is different from how you are used to writing code where you tell the computer how to give you the state you want.

------

# It looks like this:

```
resource "azurerm_resource_group" "rg" {
name     = "resource-group-name"
location = "CanadaEast"
tags {
  environment = "TF sandbox"
}
}
```

---

# Terraform vs...
- Cloud Formation
- Azure Templates
- Shell Scripting

---

# First Steps

------

In a directory run 

```
terraform init
```

- Download and install Providers
- Download Modules

---

```
# Apply vs Plan

---

# Common Pitfalls

---

# Input Variables
- CLI 
- File
- Environment

---

# Data Sources

---

# Outputs

---

# Dependencies

---

# Modules
