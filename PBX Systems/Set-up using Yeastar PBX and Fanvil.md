#### **PBX Server or Control Panel:**
##### Yeastar PBX: 
	Model: S20
The **Yeastar Model S20** is a **VoIP PBX system** designed for small businesses, supporting up to 20 users and 10 concurrent calls.  It functions as a compact, modular IP-PBX appliance that integrates SIP, PSTN, ISDN BRI, and GSM/3G connectivity. Based on Asterisk 13, it offers features like voicemail, IVR, call routing, conferencing, and unified communications via the Linkus app—all without additional licensing fees.

###### Credentials:
IP Address: 172.16.0.254
UserName: admin
Password: Flashnet@2025




#### **IP Endpoints (Phones)**:
##### Fanvil:
	Model: V62W
The **Fanvil Model V62W** is an **IP phone** (or SIP desk phone), categorized as an **endpoint device** in a PBX system.  It supports 12 SIP lines, features a 2.8-inch color screen, HD audio, dual Gigabit Ethernet ports, Power over Ethernet (PoE), built-in Wi-Fi 6 (2.4GHz/5GHz), and Bluetooth 5.4 for wireless headsets or mobile integration.

###### Credentials:
IP Address: 172.16.0.193
UserName: admin
Password: admin



#### Different ways which can be used to configure the devices
The **Yeastar S20** and **Fanvil V62W** can be connected using several methods:

1. **Plug and Play (PnP)**
    - Both devices must be on the **same subnet**. 
    - The Fanvil V62W sends a discovery message; the S20 detects it automatically.
    - In the S20 web interface, assign an extension and save — the phone auto-configures.

2. **DHCP Option 66 (for different subnets)**
    - Use when the phone and PBX are on **separate subnets**. 
    - Configure the DHCP server with **Option 66** to point to the S20’s provisioning URL.
    - The phone retrieves its configuration from the S20 via HTTP/HTTPS. 

3. **Manual Configuration**
    - Access the Fanvil V62W’s web interface.
    - Manually enter SIP account details: extension number, password, and S20 IP address.
    - Set the SIP server to the S20’s IP and port (usually 5060). 

4. **Remote Provisioning (RPS)**
    - For phones **off-site or over the internet**. 
    - Requires public IP or domain (Yeastar FQDN or external host).
    - Forward required ports on the firewall (SIP and RTP).
    - Enable remote registration on the S20 extension. 

5. **Linkus CTI Integration (Optional Control)**
    - After registration, use the **Linkus desktop/web client** to control the Fanvil phone visually (call handling, transfer, hold, etc.) if uaCSTA is enabled.





#### **Steps to set-up and configure using Plug and Play (PnP)**
To connect a **Fanvil V62W** IP phone to a **Yeastar S20** PBX system using **Plug and Play (PnP)**, follow these steps:

***Note: Using Wi-Fi to connect the `Fanvil V62W` to the `Yeastar S20` is still classified as `Plug and Play (PnP)` if both devices are on the same network. The wireless connection method itself (Wi-Fi 6) is the **network transport**, but the provisioning method remains **PnP**, as the phone automatically discovers and registers with the S20 over the local network—regardless of whether it's connected via Ethernet or Wi-Fi.***

1. **Reset the Fanvil V62W** to factory defaults if previously used. 

2. **Connect the phone** to the same network as the Yeastar S20 via Ethernet (PoE or adapter).

3. **Log in** to the Yeastar S20 web interface.

4. Go to **Auto Provisioning > Phones** and click **Scan**. 

5. Locate the Fanvil V62W in the detected phones list (by MAC address or IP).

6. Click **Edit**, select **Fanvil** as Vendor and **V62W** as Model.

7. Assign an available **Extension** to the phone.

8. Configure optional settings (keys, codecs, etc.), then click **Save**.

9. Confirm the reboot prompt. The phone will reboot and auto-configure. 


After two reboots, the phone will be registered and ready for use.