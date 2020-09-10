# azure-devops-nginxplus
NGINX Plus Deployment Pipeline for Azure DevOps

This pipeline will deploy NGINX Plus into an ADO `Environment` and optionally register the
instance with NGINX Controller. It can also install NGINX AppProtect if you have a license
for that.

## Creating the pipeline
You will first need to fork this repository on Github, then in you Azure DevOps Project
goto pipelines and click the add `New Pipeline` button. 

Select GitHub as the location of the code. You will need to link your ADO account with GitHub
if you haven't already and then select your fork of this project.

Azure will detect the pipeline and display it for you. The next step is to setup the required
variables.

## Adding Variables
You will need to add some variables to the pipeline before you can use it. In the review/edit
page for the pipeline you will have a `Variables` button. This button opens a new pane in which
you can create or edit the variables. The required variable are:

### Azure DevOps variables
1. azureDevOpsEnvironment - The name of the environment where you want to deploy NGINX
2. azureDevOpsTag - The tag to use for targeting the NGINX instances

### NGINX Plus Variables
1. nginxRepoKey - Your private key for the NGINX Plus repository
2. nginxRepoCrt - Your certificate for the NGINX Plus repository
3. nginxAP - Set to `true` if you want to include NGINX App Protect.

### NGINX Controller Registration
1. controllerRegister - Set this to `true` if you want to register NGINX Plus with NGINX Controller
2. controllerApiKey - This is the API secret needed to register with your controller
3. controllerUri - The URL for registering with your controller (eg https://controller.foo.com)
4. controllerVerify - Whether the controller certificate can be verified by the NGINX instance (true or false)
5. agentLocation - The location in which to register the agent (default should be "unspecified").
6. agentBeta - Whether to enable beta features in the NGINX Controller Agent (true or false)

## Running the pipeline
The pipeline will check for NGINX Plus and NAP, installing if they don't exist. 
If the `controllerRegister` variable is set to `true` then the pipeline will also attempt to register the
instance with NGINX Controller.

