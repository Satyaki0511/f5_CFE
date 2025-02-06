# f5_CFE
Cloud Failover Extension Cloud Failover Extension  
1>	 Open the link :-https://github.com/F5Networks/f5-cloud-failover-extension/releases

2>	Download the latest rpm packet “f5-cloud-failover-2.1.3-3.noarch.rpm”

3>	Upload the rpm packet in f5 device
>>iApps>>package Management LX 
>>choose File
>>Upload

4>	Login to f5 CLI >> type Bash 

5>	Run this command 
curl -su admin: -X GET http://localhost:8100/mgmt/shared/cloud-failover/declare |  jq .declaration > cfe.json

6>	vim cfe.json

>> add the Configuration 

7>	Run this command 
curl -su admin: -X POST -d @cfe.json http://localhost:8100/mgmt/shared/cloud-failover/declare | jq .


 8>	For troubleshooting :-
>> https://clouddocs.f5.com/products/extensions/f5-cloud-failover/latest/userguide/troubleshooting.html

>> https://github.com/F5Networks/f5-aws-cloudformation/tree/main/supported/failover/across-net/via-api/2nic/existing-stack/byol

>> https://community.f5.com/kb/technicalarticles/configuring-aws-ha-failover-across-azs-without-eips-using-f5-cloud-failover-exte/307019



