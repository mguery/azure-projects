# Security
Hands on projects for AZ-500 and SC-300 


## Section 1: Implement Identity and Access Security for Azure

### Exercise: Add a custom domain to Azure AD
- Users > custom domain names > add custom domain
- enter domain name > add domain > add DNS info to your provider (ex. namecheap.com)
- Type: TXT, Host: @, TXT value: MS=ms..., TTL: 3600 seconds (or 60 minutes) > save
- tap Verify (wait 5+ mins) > make primary > yes

### Exercise: Sign up for AAD P2 trial, user creation and group mgmt
- AAD > Licenses > All Products > tap free trial dropdown, tap Activate (refresh browser)
- create users - users > new user > create user > add info
- create groups - manage > groups > new group > add info > add owners and members > create
- for dynamic user - membership type = dynamic user / under dynamic user members - add dynamic query > configure rules > property (ex. department), operator - equals, value (ex. HR) and save > create

### Exercise: AAD role assignment
- aad console > manage > roles and admins > select global admin > assignments > select user and add
- subscriptions window > Access control (IAM) > add role assignments
- under role - assign access to user, group, or service principal > members - select members > select and save

Granted perms to users and groups in AAD and Azure subs.

### Exercise: AAD Connect deployment
- deploy azure vm hosting and domain controller [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/application-workloads/active-directory/active-directory-new-domain) > depoly to azure
- select subscription > create new res group > choose region > admin name and pw > add domain name (ex. az500lab.com) and dns prefix (ex. az500lab-58463) > select VM size > leave default values > review and create > after validation passed, tap create to complete deployment (takes 15+ mins)
- after complete - go to res group > click your res group, then adVM VM resource > copy DNS name value
- open remote desktop connection (search icon, type rdp) > paste value and connect

![Screenshot (8)](https://user-images.githubusercontent.com/10605985/154188932-41e43d5e-a7db-4d28-a5d5-2d220f8a5aac.png)

- create test users in AD DS - from rdp session, open cmd admin and type powershell
- add commands to download and run script that will create test users and groups 
- Error - an error occured trying to download [idfix ](https://github.com/Microsoft/idfix). follow [steps here](https://github.com/microsoft/idfix/issues/20#issuecomment-676633032) to fix
- IdFix toolbar - query > edit object > action - edit > apply and yes. object goes from edit to complete. tap query to verify is corrected (no longer displayed)

Prepared on-prem AD env for integration with AAD. 

### Exercise: Deploy AAD Connect PHS
- from rdp session - server manager, local server, click On for IE Enhanaced Sec Config, set both options to Off
- download aad connect > express settings, phs, next, connect to aad with syncadmin account, connect dirs, add new AD acct, check continue w/o matching upn suffixes, next > select only orgusers, optional features - password writeback > check start sync process when config is complete, install
- portal.azure.com > aad > users > review synchronized users in directory synced column

Implemented a hybrid identity setup with onprem AD and AAD. 

![image](https://user-images.githubusercontent.com/10605985/154198235-2605fa84-6c8c-4c45-a9b3-86ce763edc62.png)

### Exercise: Enable MFA by changing user state
- aad > security > mfa > additional cloud-based mfa settings > select only text msg and notif through mobile app and save >on same settings page, users tab to select user, check box and enable on side
- user will be able to setup mfa with authenticator app and text to complete registration

### Exercise: Implement conditional access
- aad > security > conditional access > policies > new policy > name pol
- assignments - users and groups, select user/group
- review/edit other options - cloud apps, conditions (sign-in risks and levels, locations, device platforms) access controls (grant, block access)
- enable policy - report only, on, off

### Exercise: Implement AAD Identity Protection
- aad > security > identity protection > user risk policy 
- user risk remediation policy > assignments - include tab all users / exclude tab - select users to exclude
- user risk - low and above
- controls - access > allow access > require pw change > enforce policy - on 
- under Report section view Risky users, risky sign-ins, and dectections

Enabled AAD IP and configured policies (user risk and sign-in risk) to respond to events.

### Exercise: AAD Privileged Identity Management
- search PIM > AAD roles > Roles > Add assignments
- select role - billing admin > select member, select > next
- assignment type - eligible > assign / view assignments 
- edit billing admin > role settings > edit 
- activation tab - 3 hours, select justification and approval to activate> next assignment
- assignemtn tab - uncheck allow perm active assignment > next notification
- notification tab - review, update
- aad roles > eligible assignments > billing admin > activate > reason - add reason in textbox
- PIM under tasks - approve requests / click approve for users > add reason for activation and confirm

Implemented AAD PIM and verified role activation workflow with approval 

### Exercise: Create access review and review PIM auditing features
- PIM > aad roles > access reviews
- review access > click role > select user > type reason, approve
- access reviews and select global admin review, progress bar to view # approved change
- view alerts to see preconfigured alerts ans risk levels

![screenshot-portal azure com-2022 02 16-02_01_35](https://user-images.githubusercontent.com/10605985/154213106-69dd9b1f-6d43-4856-8804-f4b3a5d750f2.png)

Configured and validated a PIM access review. This will help you mitigate the risk of sale acess in your env.

---

## Section 2: Implement Azure Platform Protection

### Exercise: Provision resources for Ch 6+7
- start RDP session

### Exercise: Implement Azure DDoS protection Standard
- DDoS protection > create plan > fill info > create
- virtual networks blade > click vn > DDoS protection blade 
- Enable > choose ddos plan and save
(remember to disable, and delete ddos plan in ddos protection plans)


### Exercise: Configure a WAF on Azure Applicaion Gateway
- Virtual networks > click vn > subnets 
- add subnet > name and subnet range > save
- search app gw > create app gw > fill in info 
- next: frontends > public and add new public ip (Traffic enters the application gateway via its frontend IP address(es). An application gateway can use a public IP address, private IP address, or one of each type.)
- next: backends: add backend pool > linux-web-server, add backend w/o targets - No, target type -vm, target - 10.0.1.4 > add (A backend pool is a collection of resources to which your application gateway can send traffic. A backend pool can contain virtual machines, virtual machine scale sets, app services, IP addresses, or fully qualified domain names (FQDN).)
- next: configuration > add routing rule
- listener tab - rule name webapp-http-rule, listener name - webapp-http-rule-listener, frontend ip - public, protocol - http, port - 80 , listener type - basic, error page url - no
- backend targets tab - rule name - webapp-http-rule, backend pool, backend target - linux-web-server, http settings - add new / webapp-http-setting, default values, add and add 
- next: tags > next: review and create > create
- go to resource grp > click app-gw created > copy frontend public ip add
- paste ip in new broswer tab, reach apache server page (This means that traffic is passing
through the application gateway to the backend web server hosted on the Linux VM)

![screenshot-20 185 238 155-2022 03 08-20_04_47](https://user-images.githubusercontent.com/10605985/157352399-9dfaae3a-985a-4f65-8ece-418b663961d1.png)

### Exercise: Configure NSGs and ASGs
- search application sec groups > create sg 
- choose subs and resource group > create and create
- search azseclinvm > under settings - networking > app sec group > config app sg
- select sg and save
- search network sg > create nsg > create and create 
- go to resource > pick the nsg created > inbound sec rules > add rule to allow web traffic (dest asg, pick sg, port ranges 80, 443, protocol tcp, priority 1000) and another rule to deny ssh traffic (same values, but port 22, action deny, priority 900)
- inbound sec rules blade > network interfaces > associate tab > pick azseclinvm to associate the nsg with the ntwk interface of the linux vm 
- in rdp session - putty 10.0.1.4 - should be error for no ssh allowed, in browser - 10.0.1.4 should be default ubuntu page
- nsg > private-vm-sg > netwk int > diassociate 

### Exercise: Configure firewall and service endpoints on storage account
- search storage accounts > click on storage acct > file shares and click on file
- connect > linux tab to gt the mount command info and paste in clipboard
- from strg acct > networking > allow access from selected ntwks, add exiting vn > enable > add then save (this will enable a svc endpt for private-subnet)
- in rdp putty 10.0.1.4 to connect to linux vm over ssh > name and pw > sudo df -Th command to verify no file share
- copy and right click to paste mount command > azsecvmstrg... means file share mounted 
- from storage account > file shares > click file (error means no public access to file share) 

![screenshot-portal azure com-2022 03 08-20_58_46](https://user-images.githubusercontent.com/10605985/157357599-ccd67fee-f3b1-46eb-a1f8-c5a4833df398.png)

### Exercise: Configure Azure Bastion
- go to vn > create subnet > save
- go to vms > azsecwinvm > connect - bastion > deploy
- login with username and pw > connects to vm from rdp session to browser (allow popup to continue)

### Exercise: Implement Azure Automation Update Management
- search log analytics > create workspace > review & create > create
- search automation accounts > create automattion account > review & create > create
- go to vms > select vms > 3 dots - services > update management
- select custom > change workspace > for log an workspace - select subs, location, workspace > for automation account - select subs, location, account > ok > enable
- from automation accounts, select automation acct > update management - view non-compliant machines, machines that need attn, and missing updates. can sched deployments 

### Exercise: Implement Azure Disk Encryption
- key vault > create > next: access policy > enable access to Azure Disk Encryption for volume encryption (grants ADE perms needed to get secres from akv and unwrap keys) > review & create and create (this kv resrouce will be used to store vm enc secrets)
- generate a rsa 2048 key - from key vault, keys + generate/import > create a key - generate, name - Disk-Encryption-KEK, key type - RSA, RSA key size - 2048 > create
- vm > click vm resource > disks > addtl settings > disks to encrypt - os and data disks, select key vault created, select key created - Disk-Encryption-KEK, version - current version > save
- back to vm res, extensions and apps, 2 new ext created - azurediskencryption and installscript1
- from key vaults, select kv > secrets to view secrets repo (wrapped BitLocker encryption key - BEK)

protected sensitive data stored in vm disk using ade. configured kv res to store secrets, generated enc key to encrypt secrets

### Exercise: Enable Just-in-time VM access
- to enable JIT VM access - go to vm > settings > config > upgrade security center subs to enable jit > upgrade 

(JIT access enables you to lock down inbound traffic to your VM by allowing access for only a limited time)

(no change after upgrade clicked. [how to enable jit vm access](https://docs.microsoft.com/en-us/azure/defender-for-cloud/just-in-time-access-usage?tabs=jit-config-asc%2Cjit-request-asc#enable-jit-vm-access-))

<!--
### Exercise: Secure ACR
- container registry > container > access keys > disable admin user
- open access control iam in new page > add role assignment > serch acrpush > members - select members > select mbr > select app - azseclinvm > review and assign (assigned acrpush role to linux vms system-managed identity which gives perm to push images into the registry)
- acr > security > ms defender for cloud
-->

---

## Section 3: Secure Storage, Applications, and Data


### Exercise: Provision storage account with encryption in transit enforced
- create new resource - storage account
- under data storage, containers > new ctr > name - public, blob (read access for blob only) > create
- click into public upload json file > click into file > copy url
- paste url in new tab, then change url to http:// - error http not supported (created storage acct with enforced encryption in transit)

### Exercise: Configure storage account access controls
- go to storage account > settings - config > disable blob public access and save
- back to containers, click public > change access level > ok
- click json file and copy url > error "PublicAccessNotPermitted - Public access is not permitted on this storage account." (to gain access need to be authorized using key-based autho or id-based autho)
- from blob page/json file > generate sas - account key, key 1, rea perms, start before current time, expiry, https only, generate sas token and url (this is ad hoc method)
- copy and paste blob sas url in new tab - can now access file 
- back to container - switch to aad user account (error - no perms to list data user account with aad. dont have access to data plane of azure storage by default)
- access control > add role assignments - storage blob data contrib > assign access to u/g/sp, member - select current logged in account > review and assign
- container > switch to aad user account - can now access ctr res with aad user acct (error same?)
- back to storage acct > config > disable storage account key access > blob sas url - error - "KeyBasedAuthenticationNotPermitted - Key based authentication is not permitted on this storage account." 


### Exercise: Provision resources for Ch 11
-

### Exercise: Implement network access control
-

### Exercise: Implement AAD authentication and authorization
-
 
### Exercise: Implement Always Encrypted
- 

### Exercise: Manage Access to Key Vault resources
- 

### Exercise: Protect Key Vault resources
- 

### Exercise: Implement management groups and Azure Policy
- 

### Exercise: Implement Azure Sentinel
- 
