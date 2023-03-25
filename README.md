# openstack

## 1-Operating System Installation

##### During the installation of the CentOS OS. Move to Install CentOS Stream 8-stream and click tab on your keybord
<img src="https://user-images.githubusercontent.com/37241883/227654861-09b14faf-e3ea-4bbe-94cd-9df2bb09a800.png" width="800" height="300">

##### Type a space to separate than the last kernel option, type
```    
net.ifnames=0 biosdevname=0   
```

<img src="https://user-images.githubusercontent.com/37241883/227655969-62fc200c-4989-4360-a991-56dcd9f9557b.png"  width="600" height="300">

###### Click on Network & Host

<img src="https://user-images.githubusercontent.com/37241883/227656624-8b4b647c-e25c-4041-9407-47f318e78519.png"  width="600" height="300">

###### First step we need to set the Host Name,
###### Now, the network card got an IP from the DHCP. configure the IP manually by clicking configure. Give the card the same fetched configuration from DHCP

<img src="https://user-images.githubusercontent.com/37241883/227658133-8c31d7ce-1f2f-4216-9d4b-ae488c8463cc.png"  width="600" height="300">

###### IPv4 Configuration, 

<img src="https://user-images.githubusercontent.com/37241883/227663906-1c574b31-978a-4d16-b6e5-e368c5c3587d.png"  width="600" height="300">

##### Then create user and make him Admin

<img src="https://user-images.githubusercontent.com/37241883/227664517-95b640f7-a4a0-42a3-8365-9453e0ce429d.png"  width="600" height="300">

## 2- Prerequisites Deployment:

##### Environment Setup:

###### 1- Add the hostname to /etc/hosts and make an alias for it, 

<img src="https://user-images.githubusercontent.com/37241883/227667034-133d7b31-bda7-4985-8c7f-55d64e495f9a.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227667144-bfd4bc99-ba82-4a24-b774-39305559efd6.png"  width="600" height="300">

###### 2- Disable and stop firewalld
``` 
systemctl disable firewalld
systemctl stop firewalld
systemctl status firewalld

```

<img src="https://user-images.githubusercontent.com/37241883/227667673-b251fd56-6b39-43f3-941c-29132ee37347.png"  width="600" height="300">

###### 3- Disable SeLinux

``` 
setenforce 0
```

<img src="https://user-images.githubusercontent.com/37241883/227667939-aa202fc4-37f5-432b-8e05-0a4db74915c6.png"  width="600" height="300">



###### 4- Disable and stop Networkmanager

```
systemctl disable NetworkManager
systemctl stop NetworkManager
systemctl status NetworkManager

```
<img src="https://user-images.githubusercontent.com/37241883/227668763-370ba648-3e81-4314-acec-68e111e5eba7.png"  width="600" height="300">

###### 5- Download network-scripts

```
dnf install network-scripts -y
```

<img src="https://user-images.githubusercontent.com/37241883/227669539-ad7d2dc5-2d11-494a-936a-36ebcbf68d41.png"  width="600" height="300">

###### 6- Enable and Start network-scripts

```
systemctl enable network
systemctl start network
systemctl status network

```
<img src="https://user-images.githubusercontent.com/37241883/227669633-a64c69ea-083a-4036-9edf-530f574b3ba4.png"  width="600" height="300">

###### 7- Enable power tools and install yoga,

```
dnf config-manager --enable powertools 
dnf install -y centos-release-openstack-yoga
```
<img src="https://user-images.githubusercontent.com/37241883/227674739-72e12fbf-9c3c-4593-8c3b-f54c3849fae2.png"  width="600" height="300">


###### 8- Update the system,
```
dnf -y update

```
<img src="https://user-images.githubusercontent.com/37241883/227674840-2f5ece62-3620-4235-9227-3f36634eedfa.png"  width="600" height="300">


###### 9- Install Packstack,

``` 
dnf install -y openstack-packstack
```
<img src="https://user-images.githubusercontent.com/37241883/227674948-caf06453-48f7-4480-a16c-cc0724727b77.png"  width="600" height="300">

###### 10- Generate answer file,

```
packstack --gen-answer-file=/root/answers.txt --os-neutron-l2-agent=openvswitch --os-neutron-ml2-mechanism-drivers=openvswitch --os-neutron-ml2-tenant-network-
types=vxlan --os-neutron-ml2-type-drivers=vxlan,flat --provision-demo=n --os-neutron-ovs-bridge-mappings=extnet:br-ex --os-neutron-ovs-bridge-interfaces=br-ex:eth0 --
keystone-admin-passwd=redhat --os-heat-install=n

```
<img src="https://user-images.githubusercontent.com/37241883/227675303-9af49a64-5bc6-4b43-8578-b1a1687681f5.png"  width="600" height="300">

###### 11- Start the installation,

```
packstack --answer-file=/root/answers.txt -t 3600
```
<img src="https://user-images.githubusercontent.com/37241883/227675386-274b8eb0-ffbe-4bef-bed3-101406a9b7c0.png"  width="600" height="300">


## 3- Validation:

open the dashboard in your browser, and enter the User Name and the password to Sign In.

<img src="https://user-images.githubusercontent.com/37241883/227676234-f38f74da-2ccd-4d0f-a191-0589d23779ce.png"  width="600" height="300">

## 4- Build Our Platform:
 
 #### 4.1- Create a Private Network:
 
 Firstly, we need you to be root and source the keystonerc_admin file to run the openstack commands, 

 <img src="https://user-images.githubusercontent.com/37241883/227678966-00bcf8e3-08bb-4f17-8e0a-84cc3d3b33b9.png"  width="600" height="300">
 
 ```
 neutron net-create Internal
 ```

 <img src="https://user-images.githubusercontent.com/37241883/227680521-807f49f7-51dd-4d44-b30c-dd60d4430c7a.png"  width="600" height="300">
 
 You can check the result form the GUI from Project Network  Network Topology, 
 
 <img src="https://user-images.githubusercontent.com/37241883/227680703-9f072a47-9971-4d6d-ace3-1b40056476d9.png"  width="600" height="300">
 
 
 #### 4.2- Create a Private Subnet:
 
 ```
 openstack subnet create --network Internal --subnet-range 192.168.10.0/24 --dhcp Internal_subnet

 ```
 <img src="https://user-images.githubusercontent.com/37241883/227679864-d565f8de-ad77-4d58-8b24-eb5ae8dd5a89.png"  width="600" height="300">
 
  <img src="https://user-images.githubusercontent.com/37241883/227679867-eb290a7c-df1a-472f-a4b3-26912c72ae28.png"  width="600" height="300">
 
 #### 4.3- Create an External Network:
 
 ```
 openstack network create External --provider-network-type flat --provider-physical-network extnet --external

```

 <img src="https://user-images.githubusercontent.com/37241883/227680045-779d6664-7592-4073-b796-45868b72dc83.png"  width="600" height="300">
 
  <img src="https://user-images.githubusercontent.com/37241883/227680047-cde04b14-0838-49de-99b9-dc973c2a5a3d.png"  width="600" height="300">
  
  
 
#### 4.4- Create an External Subnet:

```
openstack subnet create External_subnet --no-dhcp --allocation-pool start=192.168.120.160,end=192.168.120.170 --
gateway 192.168.120.2 --network External --subnet-range 192.168.120.0/24

```
<img src="https://user-images.githubusercontent.com/37241883/227681586-2cfe22f1-46eb-4efe-b58b-cb137f8af990.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227681588-239e4252-eb8e-44a3-b357-29de5d76a1de.png"  width="600" height="300">
 
#### 4.5- Create a Router:

```
neutron router-create router
```

<img src="https://user-images.githubusercontent.com/37241883/227688504-8ce10a2f-71e7-4011-b7c7-4184eaf2669f.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227688506-4424f5e7-4375-49f5-bd70-6b4ca9f05e1f.png"  width="600" height="300">

####  4.6- Set Router Gateway, Using External Network:

```
neutron router-gateway-set router External
```


<img src="https://user-images.githubusercontent.com/37241883/227681657-93830a78-c7b6-4566-8dab-7893774941ab.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227681659-bc2e30fd-1707-4ee9-9dcc-fa09f5b65ed0.png"  width="600" height="300">

####  4.7- Set Router Gateway, Using Internal Network:

```
neutron router-interface-add router Internal_subnet
```


<img src="https://user-images.githubusercontent.com/37241883/227681697-a8ef9153-e8a3-4e36-b54f-9aa6b7b8f894.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227681700-8a889b6b-614a-4d01-bcf8-0fdfecc2ba02.png"  width="600" height="300">
####  4.8- Install image file and Create image using glance component:

```
curl -L http://download.cirros-cloud.net/0.3.4/cirros-0.3.4-x86_64-disk.img | glance image-create --name='cirros 
image' --visibility=public --container-format=bare --disk-format=qcow2
```
<img src="https://user-images.githubusercontent.com/37241883/227689040-de470b51-4eca-43a7-80db-28f7b5786715.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227689043-460e9057-7d3e-42ab-9a3f-7752ecdc3226.png"  width="600" height="300">

## Now We Ready to Start our Instance

#### 1- Create Instance: 

```
openstack server create --image 'cirros image' --flavor m1.tiny --network Internal server1

```
<img src="https://user-images.githubusercontent.com/37241883/227682110-b8879db5-1f59-4a79-906f-d6e592ef374d.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227682113-7da38cd7-e53a-4a07-b52a-f1219320eaf0.png"  width="600" height="300">

#### 2- Create FloatingIP, to reach our instance from the Internet.

```
openstack floating ip create External

```

<img src="https://user-images.githubusercontent.com/37241883/227682174-6d1f2ff8-c907-4444-b0d5-30de428d9e7f.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227682177-d1978fab-7a4c-44b1-9df6-31c4fe4310f4.png"  width="600" height="300">

#### 3- Assign the FloatingIP to the Instance_Port

```
openstack floating ip set --port 967bac43-0eca-4ba2-be64-dfe0a86893d5 192.168.120.162

```
<img src="https://user-images.githubusercontent.com/37241883/227682266-d29fff81-62fc-4d32-b0b6-8bc629ed040d.png"  width="1000" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227682267-889d4941-31a7-490a-b70e-016a76fab6cd.png"  width="600" height="300">
#### 4- Add two rules in the default security group to enable ssh port and ICMP Project→ Network→ Security Groups → Manage Rule
<img src="https://user-images.githubusercontent.com/37241883/227682427-d7b201e8-d732-47a6-88a7-bb275b4b574d.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227682428-cbf3b267-546f-4d50-acea-8d0390575036.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227682655-b8d23552-8b2d-4cbb-877e-ec7ce3afe739.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227682658-be5f7b32-b186-456c-8aa4-c36cff475228.png"  width="600" height="300">
#### 5- Connect to your instance by SSH, 

User Name: cirros
Password: cubswin:)

```
ssh cirros@192.168.120.162
```

<img src="https://user-images.githubusercontent.com/37241883/227682750-cfcba5b9-21a9-46cb-94f8-865d25cbf7f7.png"  width="600" height="300">

<img src="https://user-images.githubusercontent.com/37241883/227687099-14eb1905-fffc-4ad2-b793-43f978561758.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687106-021ad7c8-797e-4120-9fe8-519d7174c9a1.png"  width="600" height="300">

Lets Launch and Instance from GUI, 
##### 1
<img src="https://user-images.githubusercontent.com/37241883/227685262-c4185527-c602-4a82-a0a0-8507ae9a8bd4.png"  width="600" height="300">
##### 2
<img src="https://user-images.githubusercontent.com/37241883/227685273-c3c6c2e8-18aa-4ced-bfe3-2bd5891c11ec.png"  width="600" height="300">
##### 3
<img src="https://user-images.githubusercontent.com/37241883/227685280-870fab5c-a8a3-4387-b987-fb69f3ae7de8.png"  width="600" height="300">
##### 4
<img src="https://user-images.githubusercontent.com/37241883/227685293-bb0c7567-d36b-4245-9f6d-bdf9050d66d4.png"  width="600" height="300">
##### 5
<img src="https://user-images.githubusercontent.com/37241883/227685295-b28ed352-d28a-4bd5-9de4-a18bddbedc47.png"  width="600" height="300">
##### 6
<img src="https://user-images.githubusercontent.com/37241883/227685311-8ba2779b-25e8-4ec9-8c12-12eb52688ae2.png"  width="600" height="300">
##### 7
<img src="https://user-images.githubusercontent.com/37241883/227685378-f90cbe65-1ac5-480e-b596-4e877b82678f.png"  width="600" height="300">


Validate from GUI and please waiting to be running, 
<img src="https://user-images.githubusercontent.com/37241883/227687610-01ac4d83-c1c7-489f-b631-435a2e2141b4.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687616-bdce8020-9900-4e20-8ac8-8938a18cbc05.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687618-79908702-3062-4719-a65c-41ee1fbc01b4.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687623-56741c51-028a-43c9-a210-87f2aa023c52.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687626-60b65b27-9aba-4c83-8566-7a72b0537efa.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687627-19ea5c52-5d1a-47a7-9f02-4dea40f94305.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687628-0a254db2-5b62-4bb2-9dfa-6df715b50208.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687598-8416bf7e-8579-41dc-a699-14fce3962e03.png"  width="600" height="300">
<img src="https://user-images.githubusercontent.com/37241883/227687603-982e2baa-3bd4-48b1-9083-3d0bcb1831d3.png"  width="600" height="300">

