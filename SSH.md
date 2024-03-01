# OpenStack Horizon
## Project/Compute/Key Pairs
## Create Key Pair:

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
ssh -i path/to/.ssh/name_key.pem root@your_ip
``` 

find your ip at `project/compute/instances/your_instance/interfaces` under `Fixed IPs`

## Import Public Key

Key Pair Name: `name-import-key`

Key Type: `SSH Key`

Open terminal, create a key pair & copy it:

```
ssh-keygen -t rsa -b 2048 -f name-import.key
```

```
cat name-import.key
```

paste the key pair in `Public Key` 

```
ssh root@your_ip
``` 

find your ip at `project/compute/instances/your_instance/interfaces` under `Fixed IPs`
