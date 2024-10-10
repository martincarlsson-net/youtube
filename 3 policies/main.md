## How to...
### 1. txt
```bash
config system external-resource
edit "blocklist__emerging_threats" 
    set type address
    set resource "https://rules.emergingthreats.net/fwrules/emerging-Block-IPs.txt"
    set refresh-rate 30
next
edit "blocklist__firehol_level1"
    set type address
    set resource "https://iplists.firehol.org/files/firehol_level1.netset"
    set refresh-rate 30
next

config firewall service group
edit "blocked_ports_wan"
    set member "dhcp" "radius" "samba" "smb" "snmp" "syslog" "netbios" "dce-rpc" "kerberos" "ldap" "ldaps" "rdp" "ah" "esp" "gre" "ike" "l2tp" "pptp"
    set color 6
next

config firewall policy
edit 1337 
    set name "blocklist__outbound"
    set srcintf "any"
    set dstintf INTERFACE
    set srcaddr "all"
    set dstaddr "blocklist__emerging_threats" "blocklist__firehol_level1"
    set schedule "always"
    set service "all"
    set logtraffic all
next
edit 1338 
    set name "blocklist__inbound"
    set srcintf INTERFACE
    set dstintf "any"
    set srcaddr "blocklist__emerging_threats"
    set dstaddr "all"
    set schedule "always"
    set service "all"
    set logtraffic all
next
edit 1339 
    set name "block__ports_wan"
    set srcintf "any"
    set dstintf INTERFACE
    set srcaddr "rfc_1918"
    set dstaddr "rfc_1918"
    set schedule "always"
    set service "blocked_ports_wan"
    set logtraffic all
    set dstaddr-negate enable
next


```

![alt text](fw_policies.png)