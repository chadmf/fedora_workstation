# Chad's Fedora Workstation playbook

## How to use

To run all playbooks:

```shell
ansible-playbook playbook.yml
```

To run individual playbooks use the yml files to run each for example to run the flatpak one:

```shell
ansible-playbook flatpak.yml
```

## Currently includes modules

| Modules            | Description                                                                                       |
|--------------------|---------------------------------------------------------------------------------------------------|
| fedora_workstation | Gimp, plank, gnome tweaks                                                                         |
| flatpak            | slack, zoom, bluejeans                                                                            |
| openshift          | gets latest oc client                                                                             |
| vscode             | configures vscode repo                                                                            |
| yubi_u2f           | configures everything you need for universal 2 factor EXCEPT creating the file /etc/yubi_mappings |

---

### How to populate /etc/yubikey_mappings

1. Ansible will create the empty file for this on initial run you just need to do the rest manually
2. Run the following command as the user you want to map the key to, or replace your name with the username to be assigned to the key
pamu2fcfg
3. When the key starts blinking - touch key to generate credentials
4. It will output something that looks like this:

```shell
<username1>:<KeyHandle1>,<UserKey1>,<CoseType1>,<Options1>:<KeyHandl e2>,<UserKey2>,<CoseType2>,<Options2>:... 
```

5. Copy above output and put it into /etc/yubikey_mappings
sudo nano /etc/yubikey_mappings
-Or
sudo echo ‘paste output from the pamu2fcfg command you ran in step 3 between quotes’ >> /etc/yubikey_mappings
