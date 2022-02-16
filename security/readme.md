# Security
Hands on projects for AZ-500 and SC-300 


## Section 1: Implement Identity and Access Security for Azure

Exercise: Add a custom domain to Azure AD
- Users > custom domain names > add custom domain
- enter domain name > add domain > add DNS info to your provider (ex. namecheap.com)
- Type: TXT, Host: @, TXT value: MS=ms..., TTL: 3600 seconds (or 60 minutes) > save
- tap Verify (wait 5+ mins) > make primary > yes

Exercise: Sign up for AAD P2 trial, user creation and group mgmt
- AAD > Licenses > All Products > tap free trial dropdown, tap Activate (refresh browser)
- create users - users > new user > create user > add info
- create groups - manage > groups > new group > add info > add owners and members > create
- for dynamic user - membership type = dynamic user / under dynamic user members - add dynamic query > configure rules > property (ex. department), operator - equals, value (ex. HR) and save > create

Exercise: AAD role assignment
- aad console > manage > roles and admins > select global admin > assignments > select user and add
- subscriptions window > Access control (IAM) > add role assignments
- under role - assign access to user, group, or service principal > members - select members > select and save

Granted perms to users and groups in AAD and Azure subs.

Exercise: AAD Connect deployment
- deploy azure vm hosting and domain controller [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/application-workloads/active-directory/active-directory-new-domain) > depoly to azure
- select subscription > create new res group > choose region > admin name and pw > add domain name (ex. az500lab.com) and dns prefix (ex. az500lab-58463) > select VM size > leave default values > review and create > after validation passed, tap create to complete deployment (takes 15+ mins)
- after complete - go to res group > click your res group, then adVM VM resource > copy DNS name value
- open remote desktop connection (search icon, type rdp) > paste value and connect
![Screenshot (8)](https://user-images.githubusercontent.com/10605985/154188932-41e43d5e-a7db-4d28-a5d5-2d220f8a5aac.png)
- create test users in AD DS - from rdp session, open cmd admin and type powershell
- add commands to download and run script that will create test users and groups 
- Error - an error occured trying to download [idfix ](https://github.com/Microsoft/idfix). follow [steps here](https://github.com/microsoft/idfix/issues/20#issuecomment-676633032) to fix

Exercise: Deploy AAD Connect PHS
-

Exercise: Enable MFA by changing user state
-

Exercise: Implement conditional access
-

Exercise: Implement AAD Identity Protection
-

Exercise: AAD Privileged Identity Management
-

Exercise: Create access review and review PIM auditing features
-


## Section 2: Implement Azure Platform Protection

Exercise: Provision resources for Ch 6+7
-

Exercise: Implement Azure DDoS protection Standard
-

Exercise: Implement Azure Firewall
-

Exercise: Configure a WAF on Azure Applicaion Gateway
-

Exercise: Configure NSGs and ASGs
-

Exercise: Configure firewall and service endpoints on storage account
-

Exercise: Configure Azure Bastion
-

Exercise: Clean up resources
-

Exercise: Provision resources for Ch 8
-

Exercise: Deploy Antimalware extension for Azure
-

Exercise: Implement Azure Automation Update Management
-

Exercise: Implement Azure Disk Encryption
-

Exercise: Enable Just-in-time VM access
-

Exercise: Provision resources for Ch 8
-

Exercise: Secure ACR
-


## Section 3: Secure Storage, Applications, and Data


Exercise: Provision storage account with encryption in transit enforced
-

Exercise: Configure storage account access controls
-

Exercise: Provision resources for Ch 11
-

Exercise: Implement network access control
-

Exercise: Implement AAD authentication and authorization
-
 
Exercise: Implement Always Encrypted
- 

Exercise: Manage Access to Key Vault resources
- 

Exercise: Protect Key Vault resources
- 

Exercise: Implement management groups and Azure Policy
- 

Exercise: Implement Azure Sentinel
- 

CLEAN UP RESOURCES!
