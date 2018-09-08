# heimdal kerberos apache 2

## Set up machines
```
user@host:~/heimdal_kerberos_apache2/test$ vagrant up
Bringing machine 'kdc' up with 'virtualbox' provider...
Bringing machine 'service' up with 'virtualbox' provider...
Bringing machine 'client' up with 'virtualbox' provider...
==> kdc: Importing base box 'ubuntu/xenial64'...
...
```

## Run Ansible playbook
```
user@host:~/heimdal_kerberos_apache2$ ansible-playbook site.yml -v
```
## Client test

### Login to client machine
```
user@host:~/heimdal_kerberos_apache2/test$ vagrant ssh client

```

### Check DNS
```
ubuntu@client:~$ dig +noall +answer -tA  service.example.xa 
service.example.xa.     604800  IN      A       10.0.0.3
```
### Kinit
```
ubuntu@client:~$ kinit
ubuntu@EXAMPLE.XA's Password: 
```

### Run Firefox
```
firefox
```

Enter http://service.example.xa/server-status and access should be granted


