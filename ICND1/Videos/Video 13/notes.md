# Video 13 Notes

## Configuring SSH, User Accounts, and Password Encryption

- **Configuring SSH on a Cisco Device**
  - Configure a Hostname
    - ```Switch(config)# hostname NEW_HOSTNAME```
  - Configure a Domain Name
    - ```Switch(config)# ip domain-name NEW_DOMAIN_NAME```
  - Generate Encryption Keys
    - ```Switch(config)# crypto key generate rsa```
    - Modulus size recommended >= 2048
  - Enable SSHv2
    - ```Switch(config)# ip ssh version 2```
  - Create Local User Accounts
    - ```Switch(config)# username NEW_USERNAME secret NEW_PASSWORD```
  - Choose to Allow Telnet and/or SSH
    - ```Switch(config)# line vty 0 15```
    - ```Switch(config-line)# transport input ssh``` - Allows SSH only
    - ```Switch(config-line)# transport input telnet``` - Allows telnet only
    - ```Switch(config-line)# transport input ssh telnet``` - Allows both
    - ```Switch(config-line)# login local``` - Uses local user database

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

