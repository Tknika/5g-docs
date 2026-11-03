**Stellar227** 

Indoor 2x250mW gNB **Installation Guide**

All rights reserved © Baicells Technologies Co., Ltd. Document version: 01 

**About This Document**   
**![][image1]**

This document is intended for personnel who will be installing the Baicells Stellar227 Indoor  2x250mW gNB product. The product overview is followed by the procedures for properly  installing. Please be advised that only personnel with the appropriate electrical skills and  experience should install this device. 

**Copyright Notice** 

Baicells Technologies, Inc., copyrights the information in this document. No part of this  document may be reproduced in any form or means without the prior written consent of  Baicells Technologies, Inc. 

**Disclaimer** 

The information in this document is subject to change at any time without notice. For more  information, please consult with a Baicells technical engineer or the support team. 

**Disposal of Electronic and Electrical Waste** 

Pursuant to the WEEE EU Directive, electronic and electrical waste must not be  disposed of with unsorted waste. Please contact your local recycling authority  for disposal of this product. 

**Revision Record** 

| Date  | Version  | Description |
| ----- | ----- | ----- |
| 30 Dec., 2023  | 01  | Initial Released. |
|  |  |  |
|  |  |  |

**Contact Us**

|  | Baicells Technologies Co., Ltd.  | Baicells Technologies North America, Inc. |
| ----- | ----- | ----- |
|  | China  | North America |
| Address  | 9-10F, 1st Bldg., No.81BeiqingRoad,  Haidian District, Beijing, China | 555 Republic Dr., \#200, Plano, TX 75074,  USA |
| Phone  | 400-108-0167  | \+1-888-502-5585 |
| Email  | contact@Baicells.com or   support@Baicells.com | sales\_na@Baicells.com or   support\_na@Baicells.com |
| Website  | www.Baicells.com  | https://na.Baicells.com |

![][image2]

**Safety Information** 

For the safety of installation personnel and for the protection of the equipment from  damage, please read all safety warnings. If you have any questions concerning the warnings,  before installing or powering on the base station contact the Baicells support team. 

![][image3]**Warning ![][image4]**IMPORTANT SAFETY INSTRUCTIONS 

This warning symbol means danger. You are in a situation that could cause bodily injury. Before you work on any equipment, be aware of the hazards involved with electrical circuitry and be familiar with standard practices for preventing accidents. 

![][image5]**Warning ![][image6]**Read the installation instructions before you connect the system to its power source. 

![][image7]**Warning ![][image8]**Installation of the equipment must comply with local and national electrical codes. 

![][image9]**Warning ![][image10]**This product relies on the existing building or structure for short-circuit (overcurrent) protection. Ensure that the protective device is rated no greater than 20A. ![][image11]**Warning ![][image12]**Do not operate this wireless network device near unshielded blasting caps or in an explosive environment unless the device has been modified and qualified for such use.

Table of Contents   
![][image13]

1\. Overview..................................................................................................................1 ![][image14]Introduction ................................................................................................................ 1 Highlights..................................................................................................................... 1 Appearance ................................................................................................................. 2 Technical Specification................................................................................................ 3 

1.4.1 Technology .......................................................................................................... 3 1.4.2 Interface .............................................................................................................. 3 1.4.3 Performance........................................................................................................ 4 1.4.4 Features............................................................................................................... 5 1.4.5 Link Budget.......................................................................................................... 5 1.4.6 Physical................................................................................................................ 5   
2\. Installation Preparation ..........................................................................................7 Packing List.................................................................................................................. 7 Support Materials...................................................................................................... 7 Installation Tools....................................................................................................... 7 Construction Safety..................................................................................................... 7 Installation Environment............................................................................................. 8   
3\. Installation................................................................................................................9 Ceiling or Wall Mounting ............................................................................................ 9 Connect Cables..........................................................................................................10 Power on to Check LED Status..................................................................................11

List of Figures 

Figure 1-1 Stellar227 Appearance ............................................................................2 

List of Tables 

Table 1-1 Stellar227 Interface Description ................................................................2 Table 1-2 Stellar227 Interface Indicators...................................................................2 Table 2-1 Supporting Materials .................................................................................7

**1.Overview** 

Introduction  

The Baicells Stellar227 is an advanced indoor 5G Sub-6G integrated base station  (gNB), which is designed and developed based on Qualcomm 5G SoC solution. This  2x250mW gNB is low power, subminiature and easy to maintenance. 

This product helps operators to enhance the coverage performance of 5G networks  effectively, improve the capacity of 5G networks and eliminate the blind district,  meanwhile it also can help to reduce the system power consumption. 

Highlights  

• Standard NR Band n78/n41/n48 

• Comply with 3GPP Release 15 and Release 16 

• GUI-based local and remote Web management 

• Supports 100MHz bandwidth per cell 

• Peak rate: Up to DL 850Mbps\* and UL 600Mbps  

• Supports 128 RRC connected users per cell 

• Supports Stand Alone (SA) mode 

• Supports F1 setting\* 

• Supports SCTP control (IKE SCTP) 

• Supports embedded 5G core network (HaloB) 

• Integrated small cell form factor for quick and easy installation • Supports flexible xHaul 

• Highly secured with equipment certification against potential intrusion risk • Supports TR-069 network management interface 

• Lower power consumption, which reduces OPEX 

\* Planned for future release

1 

Appearance  

The appearance of Stellar227 is shown in Figure 1-1. 

Figure 1-1 Stellar227 Appearance 

  

The Stellar227 interfaces are described in Table 1-1. 

Table 1-1 Stellar227 Interface Description 

| Interface  | Description |
| ----- | ----- |
| PWR  | 12VDC power supply interface |
| LAN  | RJ-45 interface (GE), used for initial configuration or  maintenance during device operation |
| WAN/POE++  | RJ-45 interface (GE), used for data backhaul and PoE++  power supply, complied with IEEE 802.3bt standard. |
| SFP  | Optical interface (SFP) 0, used for data backhaul |
| GPS  | External GPS antenna interface 1, SMA (F) connector |
| RST  | Power reset button |
| ANT0  | (optional) External antenna interface 0, SMA (F) connector |
| ANT1  | (optional) External antenna interface 1, SMA (F) connector |

The Stellar227 interface indicators are described in Table 1-2. 

Table 1-2 Stellar227 Interface Indicators

| Identity  | Color  | Status  | Description |
| ----: | ----: | ----: | :---: |

2 

| PWR  | Green  | Steady ON  | (Reserved) |
| :---- | :---- | ----- | :---- |
| RUN  | Green | Steady ON  | The power supply is normal. |
|  |  | Fast flash: 0.125s   on,0.125s off | The device is starting up. |
|  |  |  | Slow flash: 1s on, 1s off The device is operating normally. |
|  |  | OFF  | No power supply or device fault. |
| ACT  | Green | Steady ON  | The cell is active. |
|  |  | Slow flash: 1s on, 1s off The cell is deactivated. |  |
| ALM  | Red | Steady ON  | The device is fault. |
|  |  | OFF  | No alarm. |

Technical Specification  

**1.4.1 Technology** 

| Item  | Description |
| ----- | ----- |
| Standard  | 5G NR TDD (3GPP R15 & R16 compliant) |
| TDD UL/DL   Configuration | 5ms periodicity (μ=1): DDDDD+DDSUU  5ms periodicity (μ=1): DDDDD+SUUUU\*  2.5ms dual periodicity (μ=1): DDDSU+DDSUU  2.5ms single periodicity (μ=1): DDDSU\*, DSUUU  |
| Frequency Band  | n41 (2496 MHz – 2690 MHz)  n48 (3550 MHz – 3700 MHz)  n78 (3300 MHz – 3800 MHz) |
| Channel Bandwidth  | n41: 100MHz   n48: 10/20/30/40MHz  n78: 10/20/30/40/50/60/80/90/100MHz |
| Multiplexing  | 2x2 MIMO (DL) |
| Security  | Radio: SNOW 3G/AES-128  Backhaul: IPsec (X.509 AES-128, AES-256, SHA-128, SHA-256) |

**1.4.2 Interface**

| Item  | Description |
| ----- | ----- |
| Ethernet Interface  | 2 x RJ-45 Ethernet interface (1 GE)   1 x 1GE optical interface (SFP)  1 x 10GE optical interface (SFP+) |

3 

| Item  | Description |
| ----- | ----- |
| Power Supply  | 12VDC/POE++ |
| Protocols Used  | IPv4, UDP, TCP, ICMP, NTP, SSH, IPsec, TR-069,  HTTP/HTTPs, DHCP |
| Network   Management | IPv4, HTTP/HTTPs, TR-069, SSH, Embedded EPC |
| VLAN/VxLAN\*  | 802.IQ/VxLAN |
| LED Indicators  | 4 x status LED   PWR/ACT/RUN/ALM  |
| RF Antenna  | Embedded omni antenna or 2T2R external high gain  antenna with SMA connectors |
| GPS Antenna  | External GPS antenna, SMA connector |

**1.4.3 Performance** 

| Item  | Description |  |  |
| ----- | ----- | :---: | :---: |
| Peak Data Rate  | 100 MHz  | DL (Mbps)  | UL (Mbps) |
|  | 5ms periodicity  (DDDDD+DDSUU ,6:4:4)  | 810  | 210 |
|  | 5ms periodicity  (DDDDD+SUUUU ,6:4:4)\* | 525  | 400 |
|  | 2.5ms dual periodicity   (DDDSU+DDSUU, 10:2:2) | 720  | 330 |
|  | 2.5ms single periodicity  (DDDSU, 10:2:2)\* | 850  | 210 |
|  | 2.5ms single periodicity  (DSUUU, 10:2:2) | 380  | 600 |
| User Capacity  | Up to 128 RRC connected users |  |  |
| MAX Deployment  Range | 2000 m2 |  |  |
| Latency  | Round-trip delay (RTD) less than 10 milliseconds |  |  |
| Receive   Sensitivity | \-92 dBm (per channel) |  |  |
| Modulation  | UL: MCS0 (QPSK) to MCS27 (256QAM)  DL: MCS0 (QPSK) to MCS27 (256QAM) |  |  |
| Transmit Power  Range | 0 to 24 dBm per channel (combined 27dBm, configurable) (1 dB  interval) |  |  |
| Quality of Service  | Nine-level priority indicated by QoS Class Identifiers (QCI) |  |  |
| ARQ/HARQ  | Supported |  |  |
| Synchronization  | GPS/NL/1588v2 |  |  |

**NOTE**: The test method of receiving sensitivity is proposed by the 3GPP TS 36.104, which is based on 

4 

5MHz bandwidth, FRC A1-3 in Annex A.1 (QPSK, R=1/3, 25RB) standard. 

\* Planned for future release 

**1.4.4 Features** 

| Item  | Description |
| ----- | ----- |
| Voice  | VoNR/EPS-FB |
| SON  | Self-Organizing Network  • Automatic Neighbor Relation (ANR)  • PCI confliction detection |
| Traffic Offload  | Local breakout |
| Maintenance  | • Local/Remote Web maintenance  • Online status management  • Performance statistics  • Fault management  • Local/Remote software upgrade  • Logging  • Connectivity diagnosis  • Auto startup |

**1.4.5 Link Budget** 

| Item  | Description |
| ----- | ----- |
| VSWR  | \<= 1.5 |
| EIRP  | Antenna gain \= 4 dBi   ERIP= (27+4)dBm/100MHz |
| Power Control  | UL Open-loop/Closed-loop Power Control, DL Power  Allocation (3GPP TS 38.213 compliant)\* |

\* Planned for future release 

**1.4.6 Physical**

| Item  | Description |
| ----- | ----- |
| Surge Suppression  | Yes |
| Power Interface   Lightning Protection | Differential mode: ±10 KA  Common mode: ±20 KA |
| MTBF  | ≥ 150000 hours |
| MTTR  | ≤ 1 hour |
| Ingress Protection  | IP30 |

5 

| Item  | Description |
| ----- | ----- |
| Rating |  |
| Operating Temperature  | \-5°C to 45°C |
| Storage Temperature  | \-20°C to 65°C |
| Humidity  | 15% to 85% RH |
| Atmospheric Pressure  | 70 kPa to 106 kPa |
| Power Consumption  | Maximum 30W |
| Weight  | \< 2.4 lbs/ 1.1kg |
| Dimensions (HxWxD)  | 7.9 x 7.9 x 1.9 inches / 200 x 200 x 49 millimeters  |
| Installation  | Ceiling or wall mount |

6

**2.Installation Preparation** 

Packing List  

Before opening the box, make sure the package is in good condition, undamaged and  not wet. During the unpacking, avoid potential damaging impacts from hits or excessive  force.  

Once unpacked, check the contents to see if they are consistent with the packing list. Support Materials  

In addition to industry standard tools, you will need the materials described in Table 2-1 during the installation.  

Table 2-1 Supporting Materials 

| Item  | Figure  | Description |
| ----- | :---: | ----- |
| Optical fiber |  | Optical fiber (armor)  It is suggested that the diameter of the cable is 7± 1mm. |
| Ethernet   cable |  | Outdoor CAT6, shorter than 100 meters (\~109 yards) It is suggested that the diameter of the cable is 7± 1mm. |

**NOTE:** Other accessories have been packed in the packing box. 

Installation Tools  

The following standard tools may be needed during the installation. 

|  |  |  |  |
| :---: | :---: | :---: | :---: |
| Marker pen  | Percussion drill  | Cross screw driver  | hammer |

**NOTE:** Other accessories have been packed in the packing box. 

Construction Safety  

1\. The installation personnel must master the basic safe operation knowledge, through  the training, and having the corresponding qualifications.

7 

2\. Before installation, the installation personnel must be prepared with safety protection,  such as: safety helmet, safety belt, reflective clothing, gloves, and safety shoes, etc.  

3\. Before installation, the installation personnel must cross-check each other to ensure  above preparations have done. 

Installation Environment  

To get the signal coverage effect best, please place the Neutrino base station in an  unobstructed space.

8 

**3.Installation** 

Ceiling or Wall Mounting  

**Attention:** 

• The thickness of ceiling is not less than 18mm, and bearing more than 5kgs. If the  strength is not suitable, the device maybe fall off. 

• If the ceiling is made of unstable material, such as gypsum, this ceiling installation is  not recommended. If the device must be installed on ceiling due to environment  restriction, add one layer better panel under screws to make sure the device is  fastness. 

Here take mounting on wall as an example, mounting on ceiling is the same as it. 

1\. Put the bracket against the wall and mark the position, and then drill three holes.  Later install expansion pipe, bracket and tighten with screws. 

2\. Install four screw bolts on the back of the gNB and tighten these screw bolts. 

3\. Install the bracket on the back of the gNB with screws and tighten these screws.

9 

4\. Put the gNB from top to bottom along the slot and push it to the bottom, and then  clamp the spring sheet. 

Connect Cables  

1\. Connect power adaptor to **PWR** port and the other end connects to AC power. 

2\. Connect Ethernet cable to **WAN/POE++** port and the other end connects to the  web client. 

When the installation site has POE switch, the POE++ supply can be adopted. 

The POE switch should meet the POE++ requirements for the BT protocol, with a  power of 30 watts or higher. 

3\. Connect optical fiber to **SFP** port and the other end connects to the gateway  device. 

4\. (optional) Connect **ANT0/ANT1** to external antenna with SMA connector. By default, the built-in antennas are used.

10 

Power on to Check LED Status  

Power on the gNB, and wait a few minutes while the gNB boots up. Per the previous Table 1-2 in “1.3 Appearance”, check that the LED indicators are lighting as expected. 

11 

[image1]: img/oficial_image1.png

[image2]: img/oficial_image2.png

[image3]: img/oficial_image3.png

[image4]: img/oficial_image4.png

[image5]: img/oficial_image5.png

[image6]: img/oficial_image6.png

[image7]: img/oficial_image7.png

[image8]: img/oficial_image8.png

[image9]: img/oficial_image9.png

[image10]: img/oficial_image10.png

[image11]: img/oficial_image11.png

[image12]: img/oficial_image12.png

[image13]: img/oficial_image13.png

[image14]: img/oficial_image14.png