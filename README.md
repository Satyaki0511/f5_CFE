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
{
  "class": "Cloud_Failover",
  "environment": "aws",
  "controls": {
    "class": "Controls",
    "logLevel": "silly"
  },
  "externalStorage": {
    "scopingTags": {
      "f5_cloud_failover_label": "      ## S3 bucket tag 
    }
  },
  "failoverAddresses": {
    "enabled": true,
    "scopingTags": {
      "f5_cloud_failover_label": "f5"          ## 
    }
  },
  "failoverRoutes": {
    "enabled": true,
    "scopingTags": {
      "f5_cloud_failover_label": "f5"            ## add routing tag of aws 
    },
    "scopingAddressRanges": [
      {
        "range": "10.120.17.64/26",               ## Subnet of floating ip  
        "nextHopAddresses": {
                        "discoveryType": "static",
                        "items": [
                            "10.120.11.17",       ## Self ip
                            "10.120.15.5"         ## Self ip 
                        ]
                    }
      }
    ]
  }
}

7>	Run this command 
curl -su admin: -X POST -d @cfe.json http://localhost:8100/mgmt/shared/cloud-failover/declare | jq .


 8>	For troubleshooting :-
>> https://clouddocs.f5.com/products/extensions/f5-cloud-failover/latest/userguide/troubleshooting.html

>> https://github.com/F5Networks/f5-aws-cloudformation/tree/main/supported/failover/across-net/via-api/2nic/existing-stack/byol

>> https://community.f5.com/kb/technicalarticles/configuring-aws-ha-failover-across-azs-without-eips-using-f5-cloud-failover-exte/307019



