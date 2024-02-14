# Terraform



## Getting Started w/ Terraform
  + `Two requirements` to get started:
    - `Download` it;
    - Have `AWS CLI` up and running
  + Everything in terraform is a `.tf` file
  + The parts of the `.tf` file are:
    >- `Provider` - the cloud provider
    >- `Resource` - the cloud resource
    >>* The resource you want to collect is the `local file`
    >- `Data` - the cloud data
    >- `Variable` - the cloud variable
    >- `Output` - the cloud output



  ### CLI Commands
  + `terraform init`:
    * `downloads` all the plugins `for the providers you are using`
      >- This is always the `first command you run`, just like any other project when you're setting up and initiating your project.

  + `terraform apply`:
    * `applies` the `.tf` file to the cloud provider, `creating` the resources.
    * You can run the `-auto-approve` flag to skip the `yes` prompt
      - As a single command, you can alternatively run `terraform apply -auto-approve`

  + `terraform plan`:
    * `shows` you what resources will be created

  + `terraform destroy`:
    * `destroys` the resources you have created


  + The `state` file is the file that keeps track of the resources that have been created. It is created when you run `terraform apply` as a `.tfstate` file written in `json`
  + 
  + Terraforms defaults on `state` are:
    - `local` - the state file is stored on your local machine
    - `remote` - the state file is stored on a remote server
  + You can set up any `S3` compatible storage to store your state file by setting up the `backend` in the `.tf` file and running `terraform init` again
  
  + You keep your `variable definitions` in a `.tf` file and then you can reference them in your `.tf` file by using the `var` keyword 
  + You keep your `variable values` in a separate `.tfvars` file and then you can reference them in your `.tf` file by using the `var` keyword
    > Example:
    >  ```hcl
    >  variable "name" {
    >    type = string
    >  }
    >  ```
    >  ```hcl
    >  name = "value"
    >  ```



### Functions
  + `uppercase` - converts a string to uppercase

    > Example:
    >  ```hcl
    >  upper = upper("hello")
    >  ```
      - `upper` will be `HELLO`

  + `lowercase` - converts a string to lowercase

    > Example:
    >  ```hcl
    >  lower = lower("HELLO")
    >  ```
      - `lower` will be `hello`