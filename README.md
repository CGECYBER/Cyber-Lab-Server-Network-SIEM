# **Cyber Lab Server**

**Cyber Lab Server** is a comprehensive, live network infrastructure project designed to demonstrate the foundational setup for building and expanding a custom server environment. It incorporates **Cisco 1941 routers** for secure traffic management and **Catalyst 2960-X switches** to ensure stable, scalable network connectivity. The setup is powered by a **Dell R720 server** running **Proxmox**, enabling virtualization and resource allocation.

## **Foundational Topology**

![Foundational Topology](Topologies/Foundationl%20Topology.png)

<table>
  <thead>
    <tr>
      <th>Router Configurations</th>
      <th>Switch Configurations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <pre><code>
enable
configure terminal
hostname RouterName

enable secret YourPassword

interface GigabitEthernet0/0
ip address [WAN IP] 255.255.255.0
no shutdown
exit

interface GigabitEthernet0/1
ip address [LAN IP] 255.255.255.0
no shutdown
exit

access-list 1 permit 192.168.1.0 0.0.0.255
interface GigabitEthernet0/0
ip nat outside
exit

interface GigabitEthernet0/1
ip nat inside
exit

ip nat inside source list 1 interface GigabitEthernet0/0 overload

interface Loopback0
ip address [WAN IP] 255.255.255.0
exit

interface Loopback1
ip address [LAN IP] 255.255.255.0
exit

end
write memory
copy running-config startup-config
        </code></pre>
      </td>
      <td>
        <pre><code>
enable
configure terminal
hostname SwitchName                                                                                                                                                                                                                              

service password-encryption
enable secret YourPassword

line con 0
password YourPassword
login
exit

line vty 0 4
password YourPassword
login
exit

no ip domain-lookup

interface vlan 1
ip address [LAN IP] 255.255.255.0
no shutdown
exit

ip route 0.0.0.0 0.0.0.0 [Router LAN IP]

end
write memory
        </code></pre>
      </td>
    </tr>
  </tbody>
</table>

# **Network SIEM**

Beyond the foundational infrastructure, this project aims to show the potential of integration with additional systems such as **Windows Server 2019** and **Ubuntu Linux** environments. Splunk Enterprise is deployed on the Ubuntu server to enable centralized log collection and analysis, offering robust capabilities for **real-time monitoring**, **threat detection**, and **incident response**. This flexible setup also supports network management, security monitoring, and **SIEM testing**, with ample room for future expansion and customization to meet evolving operational needs.

## SIEM Expanded Topology|

![Extended Topology](Topologies/Extended%20Topology.png)

## **SIEM Benefits**
- **Proactive threat detection** through centralized log collection and analysis  
- **Faster incident response** with automated alerts and reporting  
- **Scalable infrastructure** to grow as security needs expand  
- **Improved security posture** with continuous monitoring and anomaly detection  
- **Enhanced compliance** by maintaining detailed logs and reports  
- **Increased operational efficiency** by automating routine security tasks

---

**Setup Document** 
📄 [Server Setup (PDF)](./Server%20Setup.pdf)

