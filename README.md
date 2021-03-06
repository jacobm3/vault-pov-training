# Running a Vault Proof of Value Session

## Steps

### Prerequisites

- Create an ssh key
  [Linux/Mac terminal instructions](https://www.digitalocean.com/community/tutorials/how-to-create-ssh-keys-with-putty-to-connect-to-a-vps)

  [Putty instructions](https://www.digitalocean.com/community/tutorials/how-to-create-ssh-keys-with-putty-to-connect-to-a-vps)

  Make sure to save the private and public key somewhere you can find them.


- Create a Terraform Enterprise account by navigating to this link and following the instructions: https://app.terraform.io/account/new

- Notify the instructor of your Terraform Enterprise user name.

- Log into the appropriate Terraform Enterprise organization.
  - The appropriate Terraform Enterprise organization will have an OAuth link that allows it to create a workspace using this repository.
  - Steps
    - Click 'Create Workspace'
    - Name your workspace
    - Choose `TheHob/vault-pov-training` as the repository to which you'd like to link.
    - Choose `master` as the branch to which you'd like to attach your workspace.
    - Populate the below variables on the 'Variables' tab
    ```
    # Terraform variables
    public_key = # Value: Contents of your personal SSH public key
    my_name    = # Your name or the name you'd like to apply to your environment
    region     = 'us-east-1' # Change it if you'd like, but if you do, you'll need to choose a value for 'training_ami' that exists in the region.
    vpc_id     = # Already set as the default VPC for you for this training, but change it to your preferred VPC if you are running this in your own account.

    # Environment variables
    AWS_ACCESS_KEY_ID     = # Value: Your AWS access key ID
    AWS_SECRET_ACCESS_KEY = # Value: Your AWS secret access key
    ```
    - Once populated, queue a plan.
    - Once plan completes, confirm it.
    - Use the outputs to connect to your VM. You should see something like the below.
    ```
    ssh -i ec2-user@<Public DNS of your VM>
    ```

### Installing Consul and Vault

- Open a shell terminal on each of your linux instances.
- From a terminal on each of your Linux AWS instances, run the following to get the Vault and Consul Enterprise binaries and install them:
  ```
  $ sudo su -
  # mkdir binaries && cd binaries
  # yum -y install wget unzip
  # wget https://s3-us-west-2.amazonaws.com/hc-enterprise-binaries/vault/ent/0.10.4/vault-enterprise_0.10.4%2Bent_linux_amd64.zip
  # wget  https://s3-us-west-2.amazonaws.com/hc-enterprise-binaries/consul/ent/1.2.2/consul-enterprise_1.2.2%2Bent_linux_amd64.zip
  # unzip consul-enterprise_1.2.2+ent_linux_amd64.zip
  # unzip vault-enterprise_0.10.4+ent_linux_amd64.zip
  # cp -rp consul /usr/local/bin/consul
  # cp -rp vault /usr/local/bin/vault
  ```

- From here, we'll use the [Proof of Value document](https://docs.google.com/document/d/1-5WJWPPr6gVRgc4Nn3INnqWo_20DVkIre9Otw3NgswU/edit#) to get our cluster running. If you can't access the link, the instructor will provide you with a PDF or Word document.
