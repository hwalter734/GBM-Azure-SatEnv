# GBM-Azure-SatEnv
This project prepares and deploys an environment in Microsoft Azure for use with Red Hat Satellite.
# Requirements
- **Ansible**: Debe tener instalado Ansible en su nodo de control. Independientemente del sistema operativo que utilice, haga uso del manejador de paquetes predeterminado de su máquina (apt|yum|etc). Más información sobre la instalación y requirimientos de Ansible haga click [aquí](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
- **Ansible Tower (Optional)**: More info [here](https://docs.ansible.com/ansible-tower/2.2.2/html/quickinstall/index.html).
- **Ansible Tower License (Optional)**: More info [here](https://www.redhat.com/en/technologies/management/ansible/try-it) 
- **Microsoft Azure Account**: You can obtain a month membership with $200 in credit when creating a new account in Microsoft Azure. More info [here](https://azure.microsoft.com/en-us/free/) para crear su cuenta.
## Packages Installation 
`pip install 'ansible[azure]'`
## Microsoft Azure Account Authentication
You can authenticate your account by using the following command `az login`.  
## Ansible Tower Environment
Ansible Tower needs your credentials to launch the job template containing the playbook. Go to *Credentials*, choose type *Microsoft Azure Resource Manager*. Enter your username and password. To obtain your *Subscription ID* and *Tenant ID* you can run the following command `az account list`. The ID is your *Subscription ID* and your tenat is your *Tenant ID*. You can leave the other fields blank. 
![azureinfocredentials](screenshots/azurecredentials.png?raw=true)

**NOTE** You may encounter a bug that relates with an error with authentication. As an alternative, you can create a new user in Azure Active Directory and use the credentials of the new user. Take note that you need to provide the user with the necessary permissions to access and modify your Azure resources. More info [here](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/add-users-azure-active-directory).  
