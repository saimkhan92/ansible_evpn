
# 'common' role

Generate the base configuration, non specific to the EVPN/VXLAN part :
 - Management Interface
 - Loopback Interface
 - Root password
 - Timezone
 - Syslog
 - User
 - SNMP
 - Static Route

Template can be found in [roles/common/templates/main.conf.j2 ](templates/main.conf.j2)

## Variables needed by the template

```yaml
loopback_ip:
global:
    root_hash:                  # Root password in Hash
    login_message:              
    time_zone:                  # Timezone
    name_servers:               # List of name servers
    ntp_servers:                # List of NTP servers
    snmp:                       # Information for SNMP
        location:
        contact:
        polling:
        - community: <community>
    routes:                     # Dict of static route to configure (optional)
        <route>: <next-hop>
vqfx:                           # true / false*
```

## Example

```yaml
# File group_vars/all/common.yaml
global:
    root_hash: $1$T1pkl3nw$Ph4CZ3ZlZ/u8ZCqV9NsAd.
    login_message: This is the property of Juniper Corp. Do not login without express permission.
    time_zone: America/Los_Angeles
    name_servers:
    - 172.29.131.60
    - 8.8.8.8
    ntp_servers:
    - 172.25.113.150
    snmp:
        location: "NYC-POC"
        contact: Anurag Menon Saim Khan
        polling:
        - community: public
    routes:
        0.0.0.0/0: 172.25.114.1



```
