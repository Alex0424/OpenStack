# Hello

### Create Key Pair

Key Pair Name: `name-private-key`

Key Type: `SSH key`

Click `Create Keypair`

It should look like this: `-----BEGIN RSA PRIVATE KEY----- pFfDhV37ixi7FawW4iMr74j/ePN37R... -----END RSA PRIVATE KEY-----`

Click `Copy Private Key to Clipboard`

Open text-editor on your computer and paste the full private key and save. 

Open your terminal and store the key in hidden .ssh file:

```
cd path/to/.ssh
vi name_ssh.pem
```
paste ssh key here

```
chmod 600 name_key.pem (Read and write only for owner for security and the key to work)
```

### Create Network

- Network
  - Network Name `name_private_network`
- Subnet
  - Subnet Name `name_subnet`
  - Network Address `x.x.x.0/24` (instead of x use a number between 0 and 255`)
  - IP Version `IPv4`
- Subnet Details
  - Allocation Pools `x.x.x.2,x.x.x.254` (this means 255 devices can be connectet to the subnet)
  - DNS Name Servers `8.8.8.8,8.8.4.4`

### Router

- CreateRouter
  - Router Name `name_router`
  - External Network `external-1`

### Interface

- Network --> Routers --> Your Router --> Interfaces --> Add Interface
  - Subnet `name_subnet`

### Security Groups

- Create Securety Group
- 
  - Name `name_security_group`
  - Add Rule
    - Rule `SSH`

### Launch Instance

- Details
  - Instance Name `name_instance`
- Source
  - Select Boot Source `Image`
  - Create New Volume `No`
  - Add `CentOS 9 Stream`
- Flavor
  - Chose the flavor you want
- Networks
  - add `name_private_network`
- Security Groups
  - add `name_security_group`
- Key Pair
  - add `your ssh key`
- Configuration
  - Customization Script (Modified)
    ```
    #cloud-config
    final_message: "The system is finally up, after $UPTIME seconds"
    ```
- Metadata
  - Custom `Image used`
  - Image used : `"CentOS 9 Stream"`

### Floating IP Compute/Instance/your_instance

- Associate Floating IP (click on `↓`)
- ![image](https://github.com/Alex0424/OpenStack/assets/33380655/5e7f999a-1ad9-4716-b5da-6edd0d6ff9a4)
  - IP Address `+` (create new)
  - Port to be associated `name_instance:ip`
 
### SSH into the Instance

- in linux terminal: `ssh -i path/to/.ssh/name_key.pem root@your_ip`

![image](https://github.com/Alex0424/OpenStack/assets/33380655/6415db54-b7d6-4293-9625-d1efdbbcd607)

