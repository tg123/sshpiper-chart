# [sshpiper](https://github.com/tg123/sshpiper)

The missing reverse proxy for ssh scp

## Usage

### Install chart with helm

```
helm repo add sshpiper https://tg123.github.io/sshpiper-chart/

helm install my-sshpiper sshpiper/sshpiper --version 0.1.1
```

### Helm Parameters

| Name                         | Description                                                                                                                             | Default Value |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------|
| sshpiper.ssh_host_key_base64 | The SSH server private key, base64 encoded. If not set a new one will be generated                                                      | ""            |
| sshpiper.existingSecret      | The secret containing SSH server private key in the `server_key` key. If set the `sshpiper.ssh_host_key_base64` is no more interpreted. | null          |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------|


### Create Password Pipe


```
apiVersion: sshpiper.com/v1beta1
kind: Pipe
metadata:
  name: pipe-password
spec:
  from:
  - username: "password_simple"
  to:
    host: host-password:2222
    username: "user"
    ignore_hostkey: true
```

`ssh password_simple@piper_ip` will pipe to `user@host-password`


### Create Public Key Pipe

`ssh piper_ip -i <key in authorized_keys_data> ` will pipe to `user@host-publickey` and login with secret `host-publickey-key`


```
apiVersion: v1
data:
  ssh-privatekey: |
    <base64 encoded private key>
kind: Secret
metadata:
  name: host-publickey-key
type: kubernetes.io/ssh-auth
---
apiVersion: sshpiper.com/v1beta1
kind: Pipe
metadata:
  name: pipe-publickey
spec:
  from:
  - username: ".*" # catch all
    username_regex_match: true
    authorized_keys_data: "base64_authorized_keys_data"
  to:
    host: host-publickey:2222
    username: "user"
    private_key_secret:
      name: host-publickey-key
    ignore_hostkey: true
```

more info: kubernetes plugin for sshpiper <https://github.com/tg123/sshpiper/tree/master/plugin/kubernetes>
