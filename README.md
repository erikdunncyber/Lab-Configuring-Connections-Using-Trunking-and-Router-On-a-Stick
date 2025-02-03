<h1>Packet Tracer - Configuring Connections Using Trunking and 'Router On a Stick'</h1>

<p align="center">
This is a network I created with 3 different VLANs where I'll be configuring the connection between SW1 and SW2 as a trunk and the connection between SW2 and R1 using 'router on a stick': <br/>
<img src="https://i.imgur.com/Igvfs9L.png" height="80%" width="80%"/>
<br />
<br />
I'll first start on Switch 1 to configure trunking by going into Global Configuration mode on the switch's CLI and then declare the interface range I want to configure using the command "int g0/1". Now I'll use the command "switchport mode trunk" to enable trunking on this interface and declare which VLANs are included in this trunked connection using the "switchport trunk allowed vlan 10,30" command, the 2 VLANs directly connected to Switch 1. I'll then set the native VLAN to an unused VLAN using the command "switchport trunk native vlan 1001": <br/>
<img src="https://i.imgur.com/mlp8tAb.png" height="80%" width="80%"/>
<br />
<br />
Now that I have configured trunking for VLAN 10 and 30 on Switch 1's g0/1 interface, check and verify to see if all necessary VLANs exist on Switch 1. I'll use the "do show vlan brief" and appears that VLAN 10 and 30 are properly appearing as I would expect: <br/>
<img src="https://i.imgur.com/wjame9P.png" height="80%" width="80%"/>
<br />
<br />
I'll be moving on to Switch 2 and will be essentially going through the same steps I went through to configure Switch 1 but as it applies to Switch 2. So first, from Switch 2's CLI I'll declare the interface range I want to configure through Global Configuration mode being "int g0/1". Now I'll allow trunking for VLAN 10 and 30 on this interface using the "switchport mode trunk" and "switchport trunk allowed vlan 10,30". Lastly, I'll use the "switchport trunk native vlan 1001" command to set the native VLAN and once again, check the VLAN brief to verify all necessary VLANs exist on Switch 2 to properly configure this trunked connection: <br/>
<img src="https://i.imgur.com/EXplafX.png" height="80%" width="80%"/>
<br />
<br />
I can also verify which interfaces are allowed on the trunked connection using the "do show interface trunk" command. By checking this brief it appears that I've forgotten to add VLAN 30 to Switch 2. I added VLAN 30 and ran the bried once more. It appears everything is in order now. : <br/>
<img src="https://i.imgur.com/2wDW9ff.png" height="80%" width="80%"/>
<br />
<br />
Now I'll be configuring the connection between SW2 and R1 using 'router on a stick'. To do this I'll stay on Switch 2's CLI and select and configure its g0/2 interface. I'll enable trunking using the "switchport mode trunk" command and allow VLANs 10, 20, and 30 on this connection. Then I'll set the native VLAN to VLAN 1001. : <br/>
<img src="https://i.imgur.com/5dXcHr9.png" height="80%" width="80%"/>
<br />
<br />
Now I'll go on to R1's CLI enable the g0/0 interface with the "no shutdown" command since Cisco router interfaces are disabled by default. Now i'll configure VLAN 10's sub-interface by using the command "int g0/0.10" and set the VLAN number with the command "encapsulation dot1q 10". I'll set the IP address with the last usable address of the subnet with the command "ip address 10.0.0.62 255.255.255.192": <br/>
<img src="https://i.imgur.com/9Y3NHD9.png" height="80%" width="80%"/>
<br />
<br />
I'll go through the same steps as before to configure the sub-interfaces for VLAN 20 and 30 as neccessary. Now that I'vs made all the needed configurations all the connections within the network should be working as intended: <br/>
<img src="https://i.imgur.com/RHoGq5p.png" height="80%" width="80%"/>
<br />
<br />
I'll use PC 7 to ping other PCs within the network to verify that all network connections are working properly. I'll first try pinging PC 1 (10.0.0.1). The packets are sent and recived successfully. Now I'll ping PC 5 in VLAN 20 (10.0.0.65). The packets are sent and recived successfully. Finally, I'll ping PC 3 in VLAN 30 (10.0.0.129). The packets are sent and recived successfully. This shows that I've successfully configured trunking between the switches for all VLANs within the network and properly configured 'router on a stick' between the router and switch 2 to perform IP routing between VLANs: <br/>
<img src="https://i.imgur.com/FdHqSUB.png" height="80%" width="80%"/>
<br />
<br />
</p>

