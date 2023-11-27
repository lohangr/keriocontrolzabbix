# keriocontrolzabbix
Template Firewall Kerio Control para Zabbix v4.4

## Discovery rules

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
|Discovery LLD Information Processor Firewall|<p>-</p>|`SNMPv2 agent`|fgHaStatsCpuUsages.discovery<p>Update: 84600</p>|
|LLD Discovery Firewall Description|<p>-</p>|`SNMPv2 agent`|sysDescr.discovery<p>Update: 84600</p>|
|Firewall Network Interface LLD Discovery|<p>-</p>|`SNMPv2 agent`|FwIfName.discovery<p>Update: 84600</p>|
|Discovery LLD Information Memory Firewall|<p>-</p>|`SNMPv2 agent`|fgHaStatsMemUsage2.discovery<p>Update: 84600</p>|


## Items collected

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
|SNMPv2 agent availability|<p>-</p>|`Zabbix internal`|zabbix[host,snmp,available]<p>Update: 60s</p>|
|System contact details|<p>-</p>|`SNMPv2 agent`|system.contact[sysContact.0]<p>Update: 1h</p>|
|System description|<p>-</p>|`SNMPv2 agent`|system.descr[sysDescr.0]<p>Update: 1h</p>|
|System location|<p>-</p>|`SNMPv2 agent`|system.location[sysLocation.0]<p>Update: 1h</p>|
|System name|<p>-</p>|`SNMPv2 agent`|system.name<p>Update: 1h</p>
|System object ID|<p>-</p>|`SNMPv2 agent`|system.objectid[sysObjectID.0]<p>Update: 15m</p>|
|Uptime|<p>-</p>|`SNMPv2 agent`|system.uptime[sysUpTime.0]<p>Update: 30s</p>|
|Network Interface Administrative Status {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifAdminStatus.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|Network Interface Alias {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifAlias.[{#SNMPINDEX}]<p>Update: 84600</p><p>LLD</p>|
|Network Interface Information {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifInOctets.[{#SNMPVALUE}]<p>Update: 600</p><p>LLD</p>|
|Network Interface Description {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifName.[{#SNMPINDEX}]<p>Update: 84600</p><p>LLD</p>|
|Outbound traffic on the interface {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifOutOctets.[{#SNMPVALUE}]<p>Update: 600;60s/1-5,07:00-19:00</p><p>LLD</p>|
|Network Interface Mac Address {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifPhysAddress.[{#SNMPINDEX}]<p>Update: 84600</p><p>LLD</p>|
|Network Interface Type {#SNMPVALUE}|<p>-</p>|`SNMPv2 agent`|ifType.[{#SNMPINDEX}]<p>Update: 84600</p><p>LLD</p>|
|Memory in use|<p>-</p>|`SNMPv2 agent`|fgHaStatsMemUsage.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|Memory Cache Usage|<p>-</p>|`SNMPv2 agent`|highMemUsage.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|Full Firewall Memory|<p>-</p>|`SNMPv2 agent`|hrMemorySize.[{#SNMPVALUE}]<p>Update: 84600</p><p>LLD</p>|
|Buffering Memory Usage|<p>-</p>|`SNMPv2 agent`|memBuffer.[{#SNMPVALUE}]<p>Update: 30s</p><p>LLD</p>|
|Share Memory Usage|<p>-</p>|`SNMPv2 agent`|memShared.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|Free Total Memory|<p>-</p>|`SNMPv2 agent`|memTotalFree.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|Used Memory (percent)|<p>-</p>|`Calculated`|memory.usage.percent.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|CPU Utilization|<p>-</p>|`SNMPv2 agent`|fgHaStatsCpuUsage.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|
|Number of Services|<p>-</p>|`SNMPv2 agent`|ifNumber.[{#SNMPVALUE}]<p>Update: 60</p><p>LLD</p>|


## Triggers

|Name|Description|Expression|Priority|
|----|-----------|----------|--------|
|Processor usage {HOST.NAME} it's too high!|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:fgHaStatsCpuUsage.[{#SNMPVALUE}].last(5m)}>50</p><p>**Recovery expression**: </p>|High|
|Memory usage {HOST.NAME} it's too high!|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:fgHaStatsMemUsage.[{#SNMPVALUE}].min(5m)}>999.99K</p><p>**Recovery expression**: </p>|High|
|The Network Interface {#SNMPVALUE} It is out!|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:ifAdminStatus.[{#SNMPVALUE}].last()}<>1</p><p>**Recovery expression**: </p>|Disaster|
|Firewall processor usage {HOST.NAME} it's too high! (LLD)|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:fgHaStatsCpuUsage.[{#SNMPVALUE}].last()}>50</p><p>**Recovery expression**: </p>|High|
|The Network Interface {#SNMPVALUE} offline|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:ifAdminStatus.[{#SNMPVALUE}].last()}<>1</p><p>**Recovery expression**: </p>|disaster|
|No SNMP data collection|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:zabbix[host,snmp,available].max({$SNMP.TIMEOUT})}=0</p><p>**Recovery expression**: </p>|Warning|
|System name has changed (new name: {ITEM.VALUE})|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:system.name.diff()}=1 and {Kerio Control Firewall:system.name.strlen()}>0</p><p>**Recovery expression**: </p>|Information|
|{HOST.NAME} has been restarted (uptime < 10m)|<p>-</p>|<p>**Expression**: {Kerio Control Firewall:system.uptime[sysUpTime.0].last()}<10m</p><p>**Recovery expression**: </p>|Disaster|

## Graphs
|Name|Type|
|----|----|
|Uptime|<p>-</p>|<p> Graph item</p>|
|Memory in use on %|<p>-</p>|<p> Graph item prototype</p>|
|Memory usage {#SNMPVALUE}|<p>-</p>|<p> Graph item prototype</p>|
|Processor usage {#SNMPVALUE}|<p>-</p>|<p> Graph item prototype</p>|


Baseado no template:
https://github.com/zabbix/community-templates/tree/main/Network_Appliances/template_snmp_firewall_kerio/5.0
