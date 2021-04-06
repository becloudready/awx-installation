# Run ansible playbooks using AWX 
* In this repo will see how to run ansible playbooks on remote machine using AWX Web UI.

# Prerequisites
* A running AWX Web UI machine.
* A remote AWS amazon ec2 instance.
* A Key pair (pem format) 

# Step 1: Create new organization.
* First, we will create a new organization by clicking on Organizations option by the name **devops** & description **my devops** as shown in figure below and click save.
![](https://github.com/becloudready/awx-installation/blob/main/organization.PNG)

# Step 2: Create new user
* Now, we will create new user by clicking on user option and enter the following details as shown in figure below & click save.
![](https://github.com/becloudready/awx-installation/blob/main/user.PNG)

# Step 3: Create new inventory
* Next, we will create new inventory by entering following details as shown in figure below & click save.
![](https://github.com/becloudready/awx-installation/blob/main/inventory.PNG)

# Step 4: Create new host
* Now, to create host click on the recently created inventory and select the hosts at the top and enter the following details as shown in figure and click save. 
* Host name can be IP address of remote machine or dns name.
![](https://github.com/becloudready/awx-installation/blob/main/host.PNG)

# Step 5: Create new credentials
* Now, we will create new credentials by entering the following details as shown in figure below & click save.
* Enter the username as **ec2-user** & password as **ec2-user**.
* For SSH Private key click browser option and select the pem file.Finally click on save. 
![](https://github.com/becloudready/awx-installation/blob/main/credentials.PNG)

# Step 6: Create new project
* Next, we will create project by entering the following details and click save.
![](https://github.com/becloudready/awx-installation/blob/main/project.PNG)

# Step 7: Create new Template
* Now, we will create new template by entering the following details and click save.
* In job template, select the following 
  ```
  Job type as 'Run'
  Inventory as 'test demo'
  Project as 'create_dir'
  Playbook as 'create_directory.yml'
  SSH as 'amazon'
  ```
![](https://github.com/becloudready/awx-installation/blob/main/template.PNG)

# Step 8: Run Job Template
* Finally, to run job template click on templates option and select the job template **create-dir-demo** and click on **Launch Template** icon.
![](https://github.com/becloudready/awx-installation/blob/main/run-job-template.PNG)

# Output
* Below screenshot shows ansible playbook executed successfully.
![](https://github.com/becloudready/awx-installation/blob/main/output_awx.PNG)
* Congratulations!!!!, we have successfully executed ansible playbook on remote aws amazon machine using AWX.


